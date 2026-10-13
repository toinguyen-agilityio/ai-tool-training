# Pull request conventions

## When to open a PR

- Agents open a PR only when the user asks for one.
- Target `main`.
- Keep PRs small and single-purpose. Split unrelated changes into separate PRs.

## Title

Same format as a commit summary (see [commit.md](commit.md#format)):

```
<type>(<optional scope>): <summary>
```

## Description

Fill in [`.github/pull_request_template.md`](../../.github/pull_request_template.md):

- **Summary**: what the PR does and why, in 1–3 sentences.
- **Changes**: bullet list of notable changes.
- **How to review**: where to start, what to check, links to artifacts.
- **Checklist**: tick every item that applies.

Write the title and description in English.

## After opening

- Give the user the full PR link and offer to watch it (CI, review comments).
- Address review comments with new commits on the same branch, then reply on
  each thread.
- Do not merge your own PR. The user reviews and merges.
