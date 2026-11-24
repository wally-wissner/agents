# agents

My agentic workflow: markdown files that agents read at the start of a session — rules, instructions, and reference material. There is no code in this repo.

## Layout

`rules/` holds behavioral rules, one file per topic, plus an index that imports them all:

- `index.md`: imports every topic file below. Import this one file to load all the rules.
- `meta.md`: how the rules themselves are handled.
- `responses.md`: how replies are structured.
- `workflow.md`: how to approach, scope, test, verify, and report work.
- `code-style.md`: code quality and when to suggest existing packages.
- `documentation.md`: comments and docs.
- `version-control.md`: commits, branches, and merges.
- `security.md`: secrets, untrusted input, access control, cryptography, and untrusted code and content.

`enforcement.md` sits beside them but is reference material, not a rule: it lists the settings and hooks that enforce the rules that can't bend. `index.md` doesn't import it. Settings files have no import mechanism, so apply its settings and script to each machine once, by hand.

## Using the rules

Agent tools load an instruction file when a session starts, and many follow `@path` imports inside it. `rules/index.md` is a list of such imports, so importing it loads every rule. To apply these rules in every project, import the index from your tool's user-level instruction file:

```markdown
@<path-to-this-repo>/rules/index.md
```

Replace `<path-to-this-repo>` with wherever you cloned the repo, as an absolute path or a `~/`-relative one. To apply the rules to a single project instead, put the same line in that project's instruction file, such as `AGENTS.md`. To use only some topics, import those topic files directly instead of the index. A tool that doesn't follow `@` imports needs each file in `rules/` pointed at directly.

Imports are read when a session starts, so edits to a rule take effect in the next session. To check what a session loaded, start one and ask which rules it has.

## Writing rules

Each topic file holds one or more rules, and each rule is a `#` section in this shape:

```markdown
# Rule title

What to do, in a sentence or two.

**Why:** The reason, so the agent can judge edge cases.

**How to apply:** Concrete steps or boundaries.
```

Describe the current behavior only. Put the history of a change in the commit message.

To add a new topic, create a file in `rules/`, add it to the list above, and add an import line for it to `rules/index.md`. The import of the index in your instruction files doesn't change.

Format markdown after editing it, using the command in `AGENTS.md`.
