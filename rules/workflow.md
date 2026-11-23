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
