# CLAUDE.md

Guidance for Claude Code (and any other agent) working in this repository.

## Project overview

`ai-tool-training` is a practice repo for the AI tool training plan
(https://dojo.agilityio.dev/index.html). It holds study notes, links to
published artifacts, and small exercises, organized by training day.

- `README.md`: index of the training days. Each day has a `## Day N — <Topic>`
  section with a bullet per deliverable (link + one-line description).
- `docs/conventions/`: branch, commit, and pull request conventions.
- `.github/pull_request_template.md`: PR body layout. Always fill it in.

There is no build, test, or lint tooling yet. If you add code, add the command to
run it to this file.

## Language

- Write everything committed to the repo in **English**: code, docs, commit
  messages, PR titles and descriptions.
- Chat with the user in whatever language they use.

## Git and GitHub conventions

Read the matching file before you create a branch, commit, or open a PR, and
follow it exactly:

| Topic         | File                                                               |
| ------------- | ------------------------------------------------------------------ |
| Branches      | [docs/conventions/branch.md](docs/conventions/branch.md)             |
| Commits       | [docs/conventions/commit.md](docs/conventions/commit.md)             |
| Pull requests | [docs/conventions/pull-request.md](docs/conventions/pull-request.md) |

Key rules at a glance:
- Never commit directly to `main`; every change goes through a PR.
- Branch: `<type>/<short-kebab-description>`.
- Commit and PR title: `<type>(<scope>): <imperative summary>`.
- Open a PR only when the user asks, and never merge your own PR.
- No "🤖 Generated with Claude Code" footer in PR descriptions.

## Adding training content

When adding notes for a new day:
1. Add a `## Day N — <Topic>` section to `README.md`, in chronological order.
2. One bullet per deliverable: `- [Title](link): what it covers.`
3. Branch `docs/dayN-<topic>`, commit `docs(dayN): ...`, PR to `main`
   (see the conventions above).
