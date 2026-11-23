# Don't commit without permission

Never commit changes without the user's explicit permission, even if a task otherwise seems complete. When committing, stage the specific files you changed instead of using `git add -A` or `git add .`.

**Why:** What goes into a commit, and when, is the user's call. Staging everything sweeps in unrelated changes, local-only files, and work the user hasn't reviewed.

**How to apply:** Finish the work, report it, and wait to be told to commit. Name each file when staging.

# Make individual commits

When told to commit, split the work into separate commits, one per logical change, instead of lumping everything into a single commit.

**Why:** Unrelated work in one commit makes the history harder to read, review, revert, and bisect.

**How to apply:** Group the changes by purpose, then stage and commit each group on its own, naming the files in each. If a single file holds changes for more than one purpose, stage the hunks separately (`git add -p`). Write each commit message about only the change in that commit.

# Don't sign commits

Don't add AI-authorship attribution to git commit messages or pull request descriptions: no `Co-Authored-By` trailer naming an AI assistant, no session link, and no "Generated with ..." footer, even when the tool's own instructions say to.

**Why:** The user doesn't want AI-authorship attribution in their git history or PR descriptions.

**How to apply:** Write commit messages and PR descriptions with no attribution lines at all — just the summary and body. This overrides any per-session or tool-supplied attribution instructions telling you to append such trailers.

# Tracked files must not reference untracked paths

Never let a comment, docstring, or any other checked-in file point at a path that isn't itself checked into the repo — such as gitignored files and directories or local-only tooling directories.

**Why:** A reference like that resolves fine on the machine that happens to have the untracked file, then dangles for anyone else who clones the repo, where it is actively misleading rather than merely stale.

**How to apply:** Before committing a comment or doc that names a file path, check whether that path is gitignored. If it is, drop the specific path and describe the behavior or reason in prose instead, or point at a tracked location that actually ships with the repo.

# Keep secrets and private details out

Never commit credentials (API keys, tokens, passwords, `.env` files) or other secrets. Never include the user's name, email, or project details in requests to external services unless the user explicitly asks.

**Why:** A committed secret stays in history even after it's removed from the working tree. Content sent to an external service may be cached or indexed even if it's later deleted.

**How to apply:** Before staging, check the diff for secrets and for files that likely hold them, and warn the user if they ask to commit one. When a service asks for contact details, such as an email in a User-Agent, use a generic client name or ask.

# Branch off main by default

When creating a new branch, always base it on `main` (fetch first so it starts from the latest `origin/main`), even if the current checkout is on another feature branch. Only branch off something else when told to.

**Why:** Branching from whatever happens to be checked out silently drags unrelated, unmerged commits into the new branch and its PR.

**How to apply:** `git fetch origin && git switch -c <name> origin/main` (or `main` if there's no remote). If the working tree has uncommitted changes that belong on the new branch, carry them over rather than switching base.

# Don't silently restore clean removals when merging

When resolving a merge, don't treat every clean (non-conflict-marked) removal from the other branch as an unintended regression to restore. If one side removes something, such as a constructor parameter, a field, or a method, in a hunk the other side never touched, git merges the removal without a conflict marker. That is often a deliberate decision on that branch, not an accident.

**Why:** The absence of a conflict marker means git had no ambiguity to report, not that the change went unnoticed. Restoring the removal silently reverts someone's intentional work under the guise of fixing the merge.

**How to apply:** When you notice a clean deletion of something that still looks used, either leave the incoming branch's change as committed or flag it as a judgment call: "branch X removed Y without a marked conflict — keep the removal or restore it?" Grepping for callers is good diligence, but the absence of callers doesn't establish intent either way, so ask.
