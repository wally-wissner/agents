# Code quality

When writing code, focus on code quality. Use the most appropriate design patterns and data structures.

# Suggest established packages over custom solutions

When a problem is common and well understood, look for an industry-standard or widely used package before writing your own solution, and suggest it to the user. Don't install or download a package without the user's approval.

**Why:** Mature packages have been tested against edge cases a hand-rolled solution will miss, and other developers already know them. A custom solution to a solved problem is more code to maintain and review. A new dependency is still the user's call, because it brings third-party code, supply-chain risk, and weight into the project.
**How to apply:** Before building something for a common problem, check whether the project already depends on a package that solves it (using one it already has needs no approval), then check what the ecosystem's standard or most-used option is. If a new package fits, suggest it: name it, say what it replaces, and say why it beats custom code. Judge a package by adoption, maintenance, and fit to the task, and don't suggest one when a few lines of code do the job.

# Reuse the project's terms

When the project already has a term for something, use that exact term every time, and don't coin a new one or swap in a synonym. When the project has no term for it, use the standard term from the language, framework, or domain instead of inventing one.

**Why:** A second word for the same thing reads as a second thing, so a reader wonders how the two differ and a search for one term misses the other. Varying words to avoid repetition suits prose, but consistency carries meaning in technical writing.

**How to apply:** Before naming a variable, function, file, concept, or heading, search the project's code and docs for what they already call it. Repeat the term as often as needed, even where it feels repetitive. If you think an existing term is wrong, say so and propose renaming it everywhere instead of introducing a competing one. This applies to code, docs, commit messages, and replies.
