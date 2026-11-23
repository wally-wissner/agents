# agents

My agentic workflow: markdown files that agents read at the start of a session — rules, instructions, and reference material. There is no code in this repo.

## Layout

`rules/` holds behavioral rules, one file per topic:

- `meta.md`: how the rules themselves are handled.
- `responses.md`: how replies are structured.
- `workflow.md`: how to approach, verify, and report work.
- `code-style.md`: code quality.
- `documentation.md`: comments and docs.
- `git.md`: commits, branches, and merges.

## Using the rules

Claude Code loads `CLAUDE.md` files automatically and follows `@path` imports inside them. To apply these rules in every project, import each file from the user-level `~/.claude/CLAUDE.md`:

```markdown
@~/Repos/agents/rules/meta.md
@~/Repos/agents/rules/responses.md
@~/Repos/agents/rules/workflow.md
@~/Repos/agents/rules/code-style.md
@~/Repos/agents/rules/documentation.md
@~/Repos/agents/rules/git.md
```

Change the path if you cloned the repo somewhere else. To apply the rules to a single project instead, put the same lines in that project's `CLAUDE.md`. To use only some topics, import only those files.

Imports are read when a session starts, so edits to a rule take effect in the next session. To check what a session loaded, start one and ask which rules it has.

## Writing rules

Each file starts with a `#` heading naming its topic. Each rule is a `##` section in this shape:

```markdown
## Rule title

What to do, in a sentence or two.

**Why:** The reason, so the agent can judge edge cases.

**How to apply:** Concrete steps or boundaries.
```

Describe the current behavior only. Put the history of a change in the commit message.

To add a new topic, create a file in `rules/`, add it to the list above, and add its import line wherever the rules are imported.

Format markdown after editing it, using the command in `CLAUDE.md`.
