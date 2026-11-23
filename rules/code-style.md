# Code quality

When writing code, focus on code quality. Use the most appropriate design patterns and data structures.

# Suggest established packages over custom solutions

When a problem is common and well understood, look for an industry-standard or widely used package before writing your own solution, and suggest it to the user. Don't install or download a package without the user's approval.

**Why:** Mature packages have been tested against edge cases a hand-rolled solution will miss, and other developers already know them. A custom solution to a solved problem is more code to maintain and review. A new dependency is still the user's call, because it brings third-party code, supply-chain risk, and weight into the project. A package that is obscure, unmaintained, or far larger than the job adds that risk without the benefit.

**How to apply:** Before building something for a common problem, check whether the project already depends on a package that solves it (using one it already has needs no approval), then check what the ecosystem's standard or most-used option is. If a new package fits, suggest it: name it, say what it replaces, and say why it beats custom code. Wait for approval before installing it. Judge a package by adoption, maintenance, and fit to the task. Don't suggest packages with little use, and don't suggest any package when the need is small enough that a few lines of code do the job.
