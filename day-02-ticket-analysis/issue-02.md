# #2 — ✨ editor: invitation details form + live preview

Ticket: https://github.com/toinguyen-agilityio/super-board/issues/2 · Analysed from the ticket text only.

## What's asked

On `/tao`, add a 5-field form (bride, groom, date and time, venue, message) with a preview that updates as the user types, Vietnamese error messages for empty required fields on blur, a 300-character cap with a counter on the message, and a side-by-side or stacked layout depending on width.

## What's vague (questions for the PO)

1. **Date and time:** what input type and display format (e.g. `18:00 · 20/12/2026`)? Which timezone? Is a past date allowed?
2. **"Empty":** does a name made only of spaces count as filled?
3. **Error text:** what is the exact Vietnamese wording for each field? Does the error clear as soon as the user types?
4. **300 characters:** counted how? Emoji and Vietnamese diacritics can be one or several code units (composed vs decomposed). On paste over the limit, truncate or block?
5. **Other limits:** is there a max length for names and venue? How should very long text look in the preview (wrap, shrink, cut)?
6. **Preview per template:** does each of the 3 templates have its own layout, or one layout with different styling?
7. **Breakpoints:** layout is defined at ≥ 1024 px and 375 px only. What about 376–1023 px?
8. **Persistence:** should typed values survive a reload or a template change?

## First step

Ask the PO to settle the date format and timezone, the whitespace rule and how the 300 characters are counted, then write component tests for validation and the counter before building the preview.

## Reproduce result (14/10, running app)

Checked every acceptance criterion on `staging` @ `7a5094a` with `npm run dev` and Chromium (Playwright):

| Acceptance criterion | Result |
|---|---|
| 5 labelled fields | ✅ |
| Preview updates while typing | ✅ |
| Vietnamese error on blur for empty required fields | ✅ also for names made only of spaces |
| Lời mời capped at 300 with a counter | ❌ counts UTF-16 units: each emoji uses 2, decomposed Vietnamese up to 2 per letter; 150 emoji already show `Còn 0 ký tự` |
| Side by side at ≥ 1024 px, stacked at 375 px | ✅ switches at 1024 px |

Bug filed: [#15 🐛 editor: message counter counts each emoji as 2 characters](https://github.com/toinguyen-agilityio/super-board/issues/15). This is vague question 4 above showing up as a real bug.
