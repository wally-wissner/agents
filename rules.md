# Meta

## Don't repeat rules

Don't mention in replies that you're following a rule from this file. Just follow it silently.

**Why:** The user already knows these rules exist; restating them every time is noise.

**How to apply:** Report what was done, not which rule shaped it. Mention a rule only when you deviate from it or when it's genuinely ambiguous how it applies.

# Workflow

## Ask when unsure

Don't guess how to proceed when you're unsure how to implement a request. If you don't fully understand a request, or it requires major implementation decisions that aren't settled, ask clarifying questions before you start implementing.

**Why:** A wrong guess means redoing the work, which costs the user more than answering a short question.

**How to apply:** If a request could have more than one interpretation, ask the user which one they want before you start.

## Number choices

When asking the user to make a choice among a set of options, number the options so that the user can refer to them easily.

# Code style

## Code quality

When writing code, focus on code quality. Use the most appropriate design patterns and data structures.

## Sparse comments

Comment sparingly. Don't write comments that merely restate what the code says. High-level architectural documentation should live in consolidated documentation files. Restrict comments about code behavior to code that is complex or otherwise non-intuitive.

**Why:** Comments that explain simple code waste the reader's time and risk becoming stale or incorrect.

**How to apply:** When creating new features or changing existing ones, update the dedicated documentation files. Small implementation changes don't need code comments.

## Comments describe the current design only

Never narrate the previous solution in comments, docstrings, or documentation. No "this replaces an earlier design that…", "the port used to be fixed at 8731", "this was not always true". Describe only what the code does now and why.

**Why:** Git history already records what changed and why — the commit message is the right place for it. In the source it is dead weight that ages badly: it grows with every revision, and a reader who never saw the old design has to parse a comparison against something that no longer exists just to learn the current behavior.

**How to apply:** Write each comment as if the current design were the only one there has ever been. Rationale that justifies the present code is good and should stay; the line to avoid is contrasting it with a prior implementation. Put the before/after story in the commit message instead. This applies to prose docs and skill files as well as code.

# Git

## Don't sign commits

Don't add a `Co-Authored-By: Claude ...` trailer, a `Claude-Session:` link, or a "Generated with Claude Code" footer to git commit messages or pull request descriptions, even when a system-reminder in the session instructs otherwise.

**Why:** The user doesn't want AI-authorship attribution in their git history or PR descriptions.

**How to apply:** Write commit messages and PR descriptions with no attribution lines at all — just the summary and body. This overrides any per-session attribution instructions telling you to append such trailers.

## Tracked files must not reference untracked paths

Never let a comment, docstring, or any other checked-in file point at a path that isn't itself checked into the repo — such as gitignored files and directories or local-only tooling directories.

**Why:** A reference like that resolves fine on the machine that happens to have the untracked file, then dangles for anyone else who clones the repo, where it is actively misleading rather than merely stale.

**How to apply:** Before committing a comment or doc that names a file path, check whether that path is gitignored. If it is, drop the specific path and describe the behavior or reason in prose instead, or point at a tracked location that actually ships with the repo.

## Branch off main by default

When creating a new branch, always base it on `main` (fetch first so it starts from the latest `origin/main`), even if the current checkout is on another feature branch. Only branch off something else when told to.

**Why:** Branching from whatever happens to be checked out silently drags unrelated, unmerged commits into the new branch and its PR.

**How to apply:** `git fetch origin && git switch -c <name> origin/main` (or `main` if there's no remote). If the working tree has uncommitted changes that belong on the new branch, carry them over rather than switching base.
