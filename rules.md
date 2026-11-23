# Meta

## Don't repeat rules

Don't mention in replies that you're following a rule from this file. Just follow it silently.

**Why:** The user already knows these rules exist; restating them every time is noise.

**How to apply:** Report what was done, not which rule shaped it. Mention a rule only when you deviate from it or when it's genuinely ambiguous how it applies.

# Workflow

## Ask when unsure

Don't guess how to proceed when you're unsure how to implement a request. If you don't fully understand a request, or it requires major implementation decisions that aren't settled, ask clarifying questions before you start implementing.

**Why:** A wrong guess means redoing the work, which costs the user more than answering a short question.

**How to apply:** If a request could have more than one interpretation, ask the user which one they want before you start. The same goes for ambiguity or contradictions that surface mid-task, such as a change that collides with existing behavior, reads one way but does another, or has more than one sensible resolution. Report it as a judgment call with a concrete example instead of silently picking a reading or working around it.

## Push back

Be willing to push back on an instruction if you don't understand its meaning or purpose, if you have a solution with a better architecture, or if the existing solution violates best practices. Say so and explain, rather than silently complying or silently doing something different.

**Why:** A concern raised before the work costs far less than one found after it, and the user wants the best result, not literal compliance.

**How to apply:** Raise the concern before you implement, along with the alternative you'd propose, and let the user decide. If they confirm the original instruction, follow it.

## Plan before large changes

When a task touches many files or involves design decisions, outline the approach and get the user's approval before you implement it.

**Why:** A disagreement about approach is cheapest to resolve before any code exists. A large change built on the wrong approach is expensive to redo and to review.

**How to apply:** Summarize the files you expect to change, the approach, and any open decisions, then wait for a go-ahead. Small, clear tasks don't need a plan.

## Verify before calling it done

Before saying a change works or a bug is fixed, run the real thing and look at the result. Passing unit tests, or a check in a throwaway script, don't count on their own.

**Why:** A fix can pass its tests and still not work, because the tests and the throwaway check may not exercise the path that was actually broken.

**How to apply:** Reproduce the bug first, so the check can fail. After the change, run the actual program or command and say what you saw. If you can't run the check, say so instead of reporting the work as done.

## Fix root causes, not symptoms

When a test, check, hook, or build fails, find out why and fix the cause. Don't skip hooks (`--no-verify`), disable or loosen a test, or catch and swallow an error just to get a passing result.

**Why:** A passing result that hides the failure leaves the bug in place and makes every later check less trustworthy.

**How to apply:** Reproduce the failure, identify the cause, and fix it. If you can't, report the work as blocked and say what you found instead of working around it.

## Number choices

When asking the user to make a choice among a set of options, number the options so that the user can refer to them easily.

# Code style

## Code quality

When writing code, focus on code quality. Use the most appropriate design patterns and data structures.

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

# Git

## Don't commit without permission

Never commit changes without the user's explicit permission, even if a task otherwise seems complete. When committing, stage the specific files you changed instead of using `git add -A` or `git add .`.

**Why:** What goes into a commit, and when, is the user's call. Staging everything sweeps in unrelated changes, local-only files, and work the user hasn't reviewed.

**How to apply:** Finish the work, report it, and wait to be told to commit. Name each file when staging.

## Make individual commits

When told to commit, split the work into separate commits, one per logical change, instead of lumping everything into a single commit.

**Why:** Unrelated work in one commit makes the history harder to read, review, revert, and bisect.

**How to apply:** Group the changes by purpose, then stage and commit each group on its own, naming the files in each. If a single file holds changes for more than one purpose, stage the hunks separately (`git add -p`). Write each commit message about only the change in that commit.

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
