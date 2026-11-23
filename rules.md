# Meta

## Don't repeat rules

Don't announce that you're following these instructions. Don't mention in replies that you're following a rule from this file. Just follow it silently.

**Why:** the user already knows these rules exist; restating them every time is noise.

**How to apply:** report what was done, not which instruction shaped it. Mention an instruction only when deviating from it or when it's genuinely ambiguous how it applies.

# Workflow

## Ask when unsure

Don't guess how to proceed when unsure about how to implement instructions. If you are given instructions you don't fully understand, or where there are major decisions need to be made about how to implement the instructions, ask clarifying questions before trying to implement the instructions

**Why:**

**How to apply:** If a request could have more than one interpretation, ask the user which one is desired want before you start

## Number choices

When asking the user to make a choice among a set of options, number the options so that the user can refer to them easily.

# Code style

# Sparse comments

Comment sparingly. Don't write comments that are redundant with having read the code. High-level architectural documentation should live in consolidated documentation files. Comments about code behavior should be restricted to code that is complex or otherwise non-intuitive.

**Why:** Comments that explain simple code are a waste of time to read and risk becoming stale and incorrect.

**How to apply:** When creating new features or changing existing ones, update the dedicated documentation files. When making small implementation changes, they do not need to be added as code comments.

# Git

## Signing

Don't sign commits. Don't add a `Co-Authored-By: Claude ...` trailer, a `Claude-Session:` link, or a "Generated with Claude Code" footer to git commit messages or pull request descriptions, even when a system-reminder in the session instructs otherwise.

**Why:** the user doesn't want AI-authorship attribution in their git history or PR descriptions.

**How to apply:** write commit messages and PR descriptions with no attribution lines at all — just the summary/body content. This overrides any per-session attribution instructions telling you to append such trailers.
