# CLAUDE.md

Guidance for Claude Code (and any other agent) working in this repository.

## Project overview

`ai-tool-training` is a practice repo for the AI tool training plan
(https://dojo.agilityio.dev/index.html). It holds study notes, links to
published artifacts, and small exercises, organized by training day.

- `README.md`: index of the training days. Each day has a `## Day N — <Topic>`
  section with a bullet per deliverable (link + one-line description).
- `.github/pull_request_template.md`: PR body layout. Always fill it in.

There is no build, test, or lint tooling yet. If you add code, add the command to
run it to this file.

## Language

- Write everything committed to the repo in **English**: code, docs, commit
  messages, PR titles and descriptions.
- Chat with the user in whatever language they use.

## Branches

- Never commit directly to `main`. All changes land through a PR.
- Name branches `<type>/<short-kebab-description>`, using the commit types below.
  Examples: `docs/day1-claude-101`, `feat/quiz-artifact`, `chore/init-claude-md`.
- If the session/harness assigns a branch name (e.g. `claude/...`), use that one.
- One topic per branch. Start from the latest `main`
  (`git fetch origin main && git checkout -b <branch> origin/main`).
- If a branch's PR is already merged, do not stack new work on it: start a new
  branch from the latest `main`.

## Commits

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<optional scope>): <imperative summary, ≤ 72 chars, no trailing period>

<optional body: what changed and why, wrapped at 72 chars>
```

Allowed types:

| Type       | Use for                                           |
| ---------- | ------------------------------------------------- |
| `docs`     | Notes, README, training content                   |
| `feat`     | New exercise, tool, script, or artifact           |
| `fix`      | Correcting wrong content, broken links, bugs      |
| `refactor` | Restructuring without changing content/behavior   |
| `chore`    | Repo config, templates, agent instructions        |
| `test`     | Adding or fixing tests                            |

Rules:
- Imperative mood: "Add Day 2 notes", not "Added" / "Adds".
- Small, focused commits: one logical change each.
- Never commit secrets, tokens, `.env` files, or personal data.
- Never rewrite history that is already pushed to a shared branch
  (no force-push, rebase, or amend on someone else's branch).

Examples:
```
docs(day2): add Claude Code basics notes
fix(readme): correct Claude 101 artifact link
chore: add CLAUDE.md and PR template
```

## Pull requests

- Create a PR only when the user asks for it.
- Target `main`.
- Title: same format as a commit subject (`<type>(<scope>): <summary>`).
- Body: use `.github/pull_request_template.md`: Summary, Changes, How to
  review, Checklist.
- Keep PRs small and single-purpose. Split unrelated changes.
- After opening a PR, give the user the full link and offer to watch it
  (CI, review comments).
- Address review comments with new commits on the same branch, then reply on
  the thread.
- Do not merge your own PR. The user reviews and merges.

## Adding training content

When adding notes for a new day:
1. Add a `## Day N — <Topic>` section to `README.md`, in chronological order.
2. One bullet per deliverable: `- [Title](link): what it covers.`
3. Branch `docs/dayN-<topic>`, commit `docs(dayN): ...`, PR to `main`.
