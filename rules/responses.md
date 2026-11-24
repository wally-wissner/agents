# Separate working from the final output

Anything you write before the final output is working: reasoning, narration of tool calls, and intermediate findings. End the working with a wide bar and put the final output after it. The bar is the line of 120 `=` characters below, copied exactly as plain text (not in a code block), with a blank line above and below it:

```text
========================================================================================================================
```

Structure the final output under these headings, in this order:

- `### ✅ Result`: what you did or found, what you saw when you verified it, and any notes that need no answer from the user.
- `### ❓ Decisions needed`: each decision for the user, numbered, with lettered options and your recommendation. Put things you noticed but didn't do, such as out-of-scope issues, and suggested next steps here as decisions (for example, "fix now" or "leave it").

**Why:** The user needs to find the outcome without reading the working, and to be able to audit the working when they choose to. A fixed layout and a visible boundary make each part findable at a glance.

**How to apply:** Write the final output so it stands on its own and makes sense without the working above it. Include both headings every time, and write "None" under Decisions needed when it's empty, so no section looks skipped. A plain answer to a question, where no work was done, doesn't need this structure.
