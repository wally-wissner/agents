# Sparse comments

Comment sparingly. Don't write comments that merely restate what the code says. High-level architectural documentation should live in consolidated documentation files. Restrict comments about code behavior to code that is complex or otherwise non-intuitive.

Sparse is not the same as undocumented. Every module, class, and function still gets a short doc comment saying what it is for and how it works: its purpose, its contract, and any mechanism a reader couldn't guess from the signature. Write each one modularly and DRY. Describe only the unit itself, and refer to other units by name instead of restating what they do, so a change to one unit only ever forces an edit to its own doc.

**Why:** Comments that explain simple code waste the reader's time and risk becoming stale or incorrect. Having no statement of purpose is just as costly, because the reader has to reverse-engineer intent from the implementation. Docs that repeat what is written elsewhere drift out of sync as soon as one copy is updated and the other isn't.

**How to apply:** When creating new features or changing existing ones, update the dedicated documentation files. Small implementation changes don't need code comments. Give each new module, class, and function a doc comment covering what it is for and how it works, scoped to that unit alone. A unit whose name and signature already make its purpose obvious can stay short. Don't copy details from a caller, a callee, or the architecture docs into it; name the other unit instead.

# Comments describe the current design only

Never narrate the previous solution in comments, docstrings, or documentation. No "this replaces an earlier design that…", "the port used to be fixed at 8731", "this was not always true". Describe only what the code does now and why.

**Why:** Version-control history already records what changed and why — the commit message is the right place for it. In the source it is dead weight that ages badly: it grows with every revision, and a reader who never saw the old design has to parse a comparison against something that no longer exists just to learn the current behavior.

**How to apply:** Write each comment as if the current design were the only one there has ever been. Rationale that justifies the present code is good and should stay; the line to avoid is contrasting it with a prior implementation. Put the before/after story in the commit message instead. This applies to prose docs and skill files as well as code.

# Keep docs in sync

Documentation describes current behavior. When a change makes a doc passage, docstring, or comment stale, or you find one that's already stale, fix it in the same change instead of only noting it.

**Why:** Stale docs mislead the next reader, and a note about a stale passage is easily forgotten while the passage stays wrong.

**How to apply:** After a behavior change, search the docs and nearby docstrings for the old behavior and rewrite those passages to describe the current behavior only.

# Developer-facing notes go in docs, not memory

Memory holds only what agents need. A rule or note that every developer should see (conventions, architecture, gotchas, how to verify a change) goes in the project's tracked documentation, not in agent memory.

**Why:** Developers look in the project's documentation, not in agent memory, so a note that lives only in memory never reaches them.

**How to apply:** Before saving a memory, ask whether a developer would need it too. If so, write it in the tracked docs.
