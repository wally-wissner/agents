# Enforcing rules with settings and hooks

Rules are instructions the model can miss. Claude Code's permission rules, attribution setting, and hooks are enforced by the tool, so the rules that can't bend are backed by them. This file is reference material for those settings. `index.md` does not import it, so it adds nothing to a session's context.

| Rule                                          | Enforced by                        |
| --------------------------------------------- | ---------------------------------- |
| Don't commit without permission               | An `ask` rule on `git commit`      |
| Don't sign commits                            | The `attribution` setting, emptied |
| Keep secrets and private details out          | `deny` rules on `.env` files       |
| Don't weaken a security control               | A `PreToolUse` hook on Bash        |
| Fix root causes, not symptoms (`--no-verify`) | The same hook                      |

## Settings

Add these to Claude Code's user-level `settings.json`:

```json
{
  "attribution": { "commit": "", "pr": "", "sessionUrl": false },
  "permissions": {
    "ask": ["Bash(git commit *)"],
    "deny": ["Read(**/.env)", "Read(**/.env.*)"]
  },
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "$HOME/.claude/hooks/block-unsafe-bash.sh"
          }
        ]
      }
    ]
  }
}
```

## Hook script

Save this where the hook command points, such as `$HOME/.claude/hooks/block-unsafe-bash.sh`, and make it executable. It needs `jq`.

```bash
#!/bin/bash
# PreToolUse hook for Bash. Reads the tool call as JSON on stdin and exits 2,
# which blocks the call and sends stderr back to the agent, when the command
# text turns off a security control or skips a repository's checks.
command=$(jq -r '.tool_input.command // empty')

block() {
  echo "Blocked: $1. Find and fix the underlying cause instead." >&2
  exit 2
}

grep -Eq -- '--no-verify' <<<"$command" &&
  block "--no-verify skips the repository's checks"
grep -Eq -- '(^|[[:space:];&|])curl[[:space:]]([^;&|]*[[:space:]])?(--insecure|-[a-zA-Z]*k[a-zA-Z]*)([[:space:]]|$)' <<<"$command" &&
  block "curl without TLS verification"
grep -Eq -- 'NODE_TLS_REJECT_UNAUTHORIZED=0' <<<"$command" &&
  block "TLS verification disabled"
grep -Eq -- '(^|[[:space:];&|])chmod[[:space:]]([^;&|]*[[:space:]])?0?777([[:space:]]|$)' <<<"$command" &&
  block "chmod 777"
exit 0
```

## Limits

- Bash rules and the hook match the command text. They miss a different program path (`/usr/bin/curl`), `sh -c '...'`, variable indirection, and an option placed before the subcommand, so `git -C dir commit` does not trigger the `ask` rule. The hook also blocks any command that merely contains one of its patterns, such as a commit message that mentions `--no-verify`.
- `Read` deny rules cover Claude Code's file tools and Bash commands that name the file, such as `cat .env`. They don't cover a script that opens the file itself; the sandbox is the OS-level control for that. `Read(**/.env.*)` also blocks `.env.example`.
- Code-level controls such as `verify=False` or a wildcard CORS origin are not visible to a Bash hook, so the written rule is the only guard for them.
