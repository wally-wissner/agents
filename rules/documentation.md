# Documentation

## Sparse comments

Comment sparingly. Don't write comments that merely restate what the code says. High-level architectural documentation should live in consolidated documentation files. Restrict comments about code behavior to code that is complex or otherwise non-intuitive.

**Why:** Comments that explain simple code waste the reader's time and risk becoming stale or incorrect.

**How to apply:** When creating new features or changing existing ones, update the dedicated documentation files. Small implementation changes don't need code comments.

## Comments describe the current design only

Never narrate the previous solution in comments, docstrings, or documentation. No "this replaces an earlier design that…", "the port used to be fixed at 8731", "this was not always true". Describe only what the code does now and why.

**Why:** Git history already records what changed and why — the commit message is the right place for it. In the source it is dead weight that ages badly: it grows with every revision, and a reader who never saw the old design has to parse a comparison against something that no longer exists just to learn the current behavior.

**How to apply:** Write each comment as if the current design were the only one there has ever been. Rationale that justifies the present code is good and should stay; the line to avoid is contrasting it with a prior implementation. Put the before/after story in the commit message instead. This applies to prose docs and skill files as well as code.

## Keep docs in sync

Documentation describes current behavior. When a change makes a doc passage, docstring, or comment stale, or you find one that's already stale, fix it in the same change instead of only noting it.

**Why:** Stale docs mislead the next reader, and a note about a stale passage is easily forgotten while the passage stays wrong.

**How to apply:** After a behavior change, search the docs and nearby docstrings for the old behavior and rewrite those passages to describe the current behavior only.

## Developer-facing notes go in docs, not memory

Memory holds only what agents need. A rule or note that every developer should see (conventions, architecture, gotchas, how to verify a change) goes in the project's tracked documentation, not in agent memory.

**Why:** Developers look in the project's documentation, not in agent memory, so a note that lives only in memory never reaches them.

**How to apply:** Before saving a memory, ask whether a developer would need it too. If so, write it in the tracked docs.
