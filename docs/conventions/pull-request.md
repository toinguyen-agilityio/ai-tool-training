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

## Before you open or edit a PR

Your branch may be older than `main`, and then it does not have the latest
template or conventions. Before you write a title or description:

```sh
git fetch origin main
git show origin/main:.github/pull_request_template.md
git show origin/main:docs/conventions/pull-request.md
```

Follow what `origin/main` says, not the copy on your branch. If your branch is
behind `main`, merge `main` into it first (see [branch.md](branch.md#rules)).

## Description

Fill in [`.github/pull_request_template.md`](../../.github/pull_request_template.md):

- **Summary**: answer **why** this change is needed (the problem, goal, or
  motivation), briefly, in 1–3 sentences. Do not list the changes here.
- **Changes**: a short summary of **what** changed, a few bullets at a high
  level. Skip implementation details; reviewers read those in the diff.
- **How to review**: where to start, what to check, links to artifacts.
- **Checklist**: tick every item that applies.

Write the title and description in English.

### Example

Reference: [PR #3](https://github.com/toinguyen-agilityio/ai-tool-training/pull/3).
Note how Summary gives only the reason and Changes gives only the result:

```markdown
## Summary

Day 2 (ticket analysis, reproduce and understand) produced notes and a bug
report that only lived in chat. Keeping them in the repo lets me pick up from
them on the next training day and shows the CP1 "reproduce + repro steps"
evidence.

## Changes

- Add `day-02-ticket-analysis/` with one analysis file per super-board ticket
  (#1–#4): what's asked, what's vague as PO questions, first step.
- Add a bug write-up for non-Latin names in the PNG file name, with
  screenshots in `evidence/`.
- Link Day 2 from `README.md`.

## How to review

- Start with `day-02-ticket-analysis/README.md`, then
  `bug-filename-non-latin.md`.
- Squash-merge: older commits on this branch predate the commit conventions.
```

Do not add a tool signature or footer to the description, such as
`🤖 Generated with [Claude Code](https://claude.com/claude-code)` or a
session link. Remove it if your tooling adds one.

## After opening

- Give the user the full PR link and offer to watch it (CI, review comments).
- Address review comments with new commits on the same branch, then reply on
  each thread.
- Do not merge your own PR. The user reviews and merges.
