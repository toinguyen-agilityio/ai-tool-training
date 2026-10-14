# Day 2 — Ticket analysis

Ticket analysis for the closed feature tickets in the practice repo [super-board](https://github.com/toinguyen-agilityio/super-board) (wedding-invitation app: Next.js 16, Vitest, Playwright, base branch `staging`).

## Method ("time-travel" mode)

1. Read the ticket only, not the code. Write down:
   - **What's asked:** one or two sentences
   - **What's vague:** each point written as a question for the PO
   - **First step:** the first thing to do if the ticket landed today
2. Ask Claude Code the same thing and compare the two lists.
3. Then open the code, tests and QA reports (`docs/super-board/runs/issue-<n>-*`) and check each vague point: which reading did the dev choose, and is it tested? An unanswered point is a bug candidate.

Why closed tickets: they come with an answer key (code, tests, QA reports), so you can check whether your "vague" radar was right. Done does not mean correct: vague spots are where bugs hide.

## Tickets

| Ticket | Title | Analysis | Step 3 (check vs code) |
|---|---|---|---|
| [#1](https://github.com/toinguyen-agilityio/super-board/issues/1) | ✨ app: Next.js scaffold + invitation template picker | [issue-01.md](issue-01.md) | To do |
| [#2](https://github.com/toinguyen-agilityio/super-board/issues/2) | ✨ editor: invitation details form + live preview | [issue-02.md](issue-02.md) | To do |
| [#3](https://github.com/toinguyen-agilityio/super-board/issues/3) | ✨ editor: customise colours, font and background | [issue-03.md](issue-03.md) | To do |
| [#4](https://github.com/toinguyen-agilityio/super-board/issues/4) | ✨ editor: full-screen preview + PNG download | [issue-04.md](issue-04.md) | Started: 2 findings |

## Bugs found

| Bug | From | Status |
|---|---|---|
| [🐛 download: PNG file name drops non-Latin names](bug-filename-non-latin.md) | #4, Q1 | Reproduced, filed as [super-board #11](https://github.com/toinguyen-agilityio/super-board/issues/11) |

## Next (Day 2 remaining)

- [ ] Compare my own list with Claude's for each ticket
- [ ] Step 3: check each vague point against the code and QA reports
- [x] Pick one bug, write a bug ticket in super-board's format (`docs/agents/issue-tracker.md`)
- [ ] Add a failing test for it (fix comes on Day 3)
