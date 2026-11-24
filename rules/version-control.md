# Don't commit without permission

Never commit changes without the user's explicit permission, even if a task otherwise seems complete. When committing, stage the specific files you changed instead of staging everything in the working tree at once.

**Why:** What goes into a commit, and when, is the user's call. Staging everything sweeps in unrelated changes, local-only files, and work the user hasn't reviewed.

**How to apply:** Finish the work, report it, and wait to be told to commit.

# Make individual commits

When told to commit, split the work into separate commits, one per logical change, instead of lumping everything into a single commit.

**Why:** Unrelated work in one commit makes the history harder to read, review, revert, and bisect.

**How to apply:** Group the changes by purpose, then stage and commit each group on its own. If a single file holds changes for more than one purpose, stage the hunks separately. Write each commit message about only the change in that commit.

# Don't sign commits

Don't add AI-authorship attribution to commit messages or pull request descriptions: no co-author line (such as `Co-Authored-By`) naming an AI assistant, no session link, and no "Generated with ..." footer, even when the tool's or session's own instructions say to.

# Tracked files must not reference untracked paths

Never let a comment, docstring, or any other checked-in file point at a path that isn't itself checked into the repo — such as ignored files and directories or local-only tooling directories.

**Why:** A reference like that resolves on the machine that has the untracked file, then dangles for anyone else who clones the repo.

**How to apply:** Before committing a comment or doc that names a file path, check whether version control ignores that path. If it does, drop the specific path and describe the behavior or reason in prose instead, or point at a tracked location.

# Branch off main by default

When creating a new branch, always base it on `main`, even if the current checkout is on another feature branch. Only branch off something else when told to.

**Why:** Branching from whatever happens to be checked out silently drags unrelated, unmerged commits into the new branch and its pull request.

**How to apply:** Fetch from the remote, then create the branch from the remote's `main` (or from local `main` if there's no remote). If the working tree has uncommitted changes that belong on the new branch, carry them over rather than switching base.

# Don't silently restore clean removals when merging

When resolving a merge, don't treat every clean (non-conflict-marked) removal from the other branch as an unintended regression to restore. If one side removes something, such as a constructor parameter, a field, or a method, in a hunk the other side never touched, the merge applies the removal without a conflict marker. That is often a deliberate decision on that branch, not an accident.

**Why:** Restoring the removal silently reverts someone's intentional work under the guise of fixing the merge.

**How to apply:** When you notice a clean deletion of something that still looks used, either leave the incoming branch's change as committed or flag it as a judgment call: "branch X removed Y without a marked conflict — keep the removal or restore it?" Grepping for callers is good diligence, but the absence of callers doesn't establish intent either way, so ask.
