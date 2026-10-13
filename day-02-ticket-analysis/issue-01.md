# #1 — ✨ app: Next.js scaffold + invitation template picker

Ticket: https://github.com/toinguyen-agilityio/super-board/issues/1 · Analysed from the ticket text only.

## What's asked

Scaffold a client-only Next.js (App Router) + TypeScript + Tailwind app with `typecheck`, `lint` and `test` scripts, and build `/` showing 3 template cards that link to the editor at `/tao?mau=<id>`, with a placeholder `/tao` page.

## What's vague (questions for the PO)

1. **Templates:** which 3 templates, with which Vietnamese names and ids? Who provides the thumbnails, and in what format and size?
2. **`mau` edge cases:** "an unknown `mau` redirects to `/`", but what about a missing `mau`, an empty one, a repeated one (`?mau=a&mau=b`) or a different case (`?mau=CO-DIEN`)?
3. **Redirect UX:** should the user see a message after the redirect, or land silently on `/`?
4. **"Fresh clone":** which Node and npm versions must the scripts pass on? Is that pinned anywhere (`.nvmrc`, `engines`)?
5. **Browser tests:** the stack note mentions Playwright, but no AC requires an e2e test. Is an e2e test part of done?
6. **Responsive:** only 375 px is specified. What layout is expected at tablet and desktop widths?
7. **Accessibility:** must the cards be keyboard-focusable links with alt text on the thumbnails?

## First step

Confirm the template list (ids, names, thumbnails) and the Node version, then scaffold the app and get `npm ci`, `typecheck`, `lint` and `test` green on a fresh clone before building the picker.
