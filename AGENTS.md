# agents

My agentic workflow: markdown files — rules, instructions, reference material — that future agent sessions read. There is no code in this repo.

Format markdown with [mdformat](https://mdformat.readthedocs.io/) after editing it:

```sh
uvx --with mdformat-gfm --with mdformat-frontmatter mdformat .
```

Add `--check` to verify without rewriting.
