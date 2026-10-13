# Branch conventions

## Rules

- Never commit directly to `main`. All changes land through a pull request.
- One topic per branch.
- Start every branch from the latest `main`:

  ```sh
  git fetch origin main
  git checkout -b <branch> origin/main
  ```

- If a branch's PR is already merged, do not stack new work on it. Start a new
  branch from the latest `main`.
- Never rewrite history on a branch someone else works on (no force-push,
  rebase, or amend). Bring in `main` with a merge commit instead.

## Naming

```
<type>/<short-kebab-description>
```

- `<type>` is one of the commit types in [commit.md](commit.md#types).
- The description is lowercase, kebab-case, and a few words long.

| Example                 | When                          |
| ----------------------- | ----------------------------- |
| `docs/day1-claude-101`  | Training notes for a day      |
| `feat/quiz-artifact`    | A new exercise or artifact    |
| `fix/readme-links`      | Correcting broken content     |
| `chore/init-claude-md`  | Repo config, agent rules      |

**Exception:** if the session or harness assigns a branch name (for example
`claude/...` in Claude Code cloud sessions), use that name.
