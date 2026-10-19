---
name: new-training-day
description: Add a new training day to this repo (README section, branch, commit, PR). Use when the user says "add Day N", "log today's training" or "thêm Day N".
# TODO(Toi): tune the description. Claude decides when to load this skill
# from the description alone, so list the phrases you actually type.
---

# New training day

Adds the notes for one training day, following `CLAUDE.md` and
`docs/conventions/`.

## Inputs

<!-- TODO(Toi): what must Claude ask for before it starts? -->
- Day number `N` and topic
- Deliverables: title, link, one-line description each
- TODO

## Steps

1. Branch from the latest `main`: `git fetch origin main`, then
   `git checkout -b docs/dayN-<topic> origin/main`.
2. Add a `## Day N — <Topic>` section to `README.md` in chronological order,
   using [assets/day-section.md](assets/day-section.md).
3. TODO(Toi): extra notes files? Where do they go (`day-0N-<topic>/`)?
4. Commit: `docs(dayN): <imperative summary>`.
5. Open a PR only if the user asks. Follow `docs/conventions/pull-request.md`.

## Rules

- Everything committed is in English.
- TODO(Toi): add your own never-do rules (e.g. no client code or secrets).

## Example

<!-- TODO(Toi): paste a real Day section from README.md as a good example. -->
