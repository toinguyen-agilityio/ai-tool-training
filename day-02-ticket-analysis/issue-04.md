# #4 — ✨ editor: full-screen preview + PNG download

Ticket: https://github.com/toinguyen-agilityio/super-board/issues/4 · Analysed from the ticket text only.

## What's asked

In the editor `/tao?mau=<id>`, add a "Xem trước" button that opens the invitation full screen (closed with Esc or a close button, all input kept), and a "Tải về" button that exports a PNG at least 1080 px wide that matches the preview. "Tải về" is disabled, with a Vietnamese hint, while the form is invalid.

## What's vague (questions for the PO)

1. **File name:** what if a name has non-Latin characters (`李华`), special characters (`O'Brien`, emoji), or is empty after stripping diacritics? Is there a length limit?
2. **Name order:** always bride then groom, or the order shown on the invitation?
3. **"Same background":** when no image is uploaded, should the PNG use the template's default background or a transparent one?
4. **"At least 1080 px wide":** what aspect ratio and height? Larger on retina screens?
5. **"Empty or invalid":** what counts as invalid? A past date? A message over 300 characters?
6. **Hint text:** exact Vietnamese wording, and where is it shown (tooltip or text under the button)?
7. **Full screen:** an in-page overlay or the browser Fullscreen API? On mobile, is "Tải về" available inside the full-screen view?
8. **Export failure:** if `html-to-image` fails (font or image not loaded yet), what does the user see? Is there a retry?
9. **Browser support:** iOS Safari often opens the image in a new tab instead of downloading. Is that acceptable?

## First step

Get the PO to settle questions 1, 3 and 5 first, because they change the test assertions directly. Then write tests for `invitationFileName` with a table of awkward inputs (diacritics, non-Latin, empty, special characters) before touching the UI.

## Findings so far (step 3, checked against the repo)

- **Q1 is a real bug candidate:** `lib/download.ts` keeps only `[A-Za-z0-9-]` after stripping diacritics, so bride `李华` + groom `Trần Văn Đức` gives `thiep-cuoi--Tran-Van-Duc.png` (bride's name lost). Verified by running the slug logic in Node. Full write-up: [bug-filename-non-latin.md](bug-filename-non-latin.md).
- **Q3 caused a rebuild:** the ticket has the label `loop:rebuild-1`, and the first QA run has `docs/super-board/runs/issue-4-qa-v1/ac3-fail-transparent-on-dark.png`, so the first build exported a transparent background and failed AC3.
