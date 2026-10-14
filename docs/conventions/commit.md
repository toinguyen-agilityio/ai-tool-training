# Commit conventions

Follow [Conventional Commits](https://www.conventionalcommits.org/).

## Format

```
<type>(<optional scope>): <summary>

<optional body>
```

- **Summary**: imperative mood ("Add", not "Added" / "Adds"), at most 72
  characters, no trailing period.
- **Scope** (optional): the area touched, e.g. `day2`, `readme`, `template`.
- **Body** (optional): what changed and why, wrapped at 72 characters.
  Leave a blank line between the summary and the body.

## Types

| Type       | Use for                                         |
| ---------- | ----------------------------------------------- |
| `docs`     | Notes, README, training content                 |
| `feat`     | New exercise, tool, script, or artifact         |
| `fix`      | Correcting wrong content, broken links, bugs    |
| `refactor` | Restructuring without changing content/behavior |
| `chore`    | Repo config, templates, agent instructions      |
| `test`     | Adding or fixing tests                          |

## Rules

- Small, focused commits: one logical change each.
- Write commit messages in English.
- Never commit secrets, tokens, `.env` files, or personal data.

## Examples

```
docs(day2): add Claude Code basics notes
fix(readme): correct Claude 101 artifact link
chore: add CLAUDE.md and PR template
```
