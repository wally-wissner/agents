# agents

My agentic workflow: markdown files that agents read at the start of a session — rules, instructions, and reference material. There is no code in this repo.

## Layout

`rules/` holds behavioral rules, one file per topic, plus an index that imports them all:

- `index.md`: imports every topic file below. Import this one file to load all the rules.
- `meta.md`: how the rules themselves are handled.
- `responses.md`: how replies are structured.
- `workflow.md`: how to approach, verify, and report work.
- `code-style.md`: code quality.
- `documentation.md`: comments and docs.
- `git.md`: commits, branches, and merges.

## Using the rules

Claude Code loads `CLAUDE.md` files automatically and follows `@path` imports inside them. To apply these rules in every project, import the index from the user-level `~/.claude/CLAUDE.md`:

```markdown
@~/Repos/agents/rules/index.md
```

Change the path if you cloned the repo somewhere else. To apply the rules to a single project instead, put the same line in that project's `CLAUDE.md`. To use only some topics, import those topic files directly instead of the index.

Imports are read when a session starts, so edits to a rule take effect in the next session. To check what a session loaded, start one and ask which rules it has.

## Writing rules

Each topic file starts with a `#` heading naming its topic. Each rule is a `##` section in this shape:

```markdown
## Rule title

What to do, in a sentence or two.

**Why:** The reason, so the agent can judge edge cases.

**How to apply:** Concrete steps or boundaries.
```

Describe the current behavior only. Put the history of a change in the commit message.

To add a new topic, create a file in `rules/`, add it to the list above, and add an import line for it to `rules/index.md`. The imports in `CLAUDE.md` files don't change.

Format markdown after editing it, using the command in `CLAUDE.md`.
