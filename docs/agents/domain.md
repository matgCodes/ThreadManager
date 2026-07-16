# Domain Docs

How the engineering skills should consume this repository's domain
documentation when exploring the codebase.

## Before exploring, read these

- `CONTEXT.md` at the repository root.
- Relevant records under `docs/adr/`.

If either location does not exist, proceed silently. The `domain-modeling`
skill, reached through workflows such as `grill-with-docs`, creates domain
context and ADRs lazily when terms or decisions are actually resolved.

## File structure

ThreadManager uses a single-context layout:

```text
/
├── CONTEXT.md
├── docs/
│   └── adr/
│       ├── ADR-0001-short-slug.md
│       └── ADR-0002-short-slug.md
└── src/
```

The directories and files shown above are conventions, not setup placeholders.
Create them only when the first real domain document or ADR is written.

## Use the glossary's vocabulary

When output names a domain concept in an issue title, proposal, hypothesis, test
name, or implementation, use the term as defined in `CONTEXT.md`. Do not drift
to synonyms the glossary explicitly avoids.

If a needed concept is not in the glossary, reconsider whether the project uses
that term or route the gap through `domain-modeling`.

## Flag ADR conflicts

If proposed work contradicts an existing ADR, surface the conflict explicitly
rather than silently overriding the recorded decision.
