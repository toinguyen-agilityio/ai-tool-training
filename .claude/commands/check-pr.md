---
description: Check the current branch's PR against this repo's PR conventions
argument-hint: [pr-number]
# TODO(Toi): limit tools if you want, e.g. allowed-tools: Bash(git fetch:*), Bash(git show:*)
---

Check pull request $ARGUMENTS (or the PR for the current branch if none is
given) against the conventions on `origin/main`.

1. Run `git fetch origin main` and read
   `origin/main:.github/pull_request_template.md` and
   `origin/main:docs/conventions/pull-request.md`.
2. Check the title matches `<type>(<scope>): <summary>`.
3. Check the description fills every template section.
4. Check there is no "Generated with Claude Code" footer or session link.
5. TODO(Toi): more checks (branch name, commit messages, English only, ...).

Report a pass/fail table, one row per check, with a fix for each fail.
Do not edit the PR yourself.
