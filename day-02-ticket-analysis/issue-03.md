# #3 — ✨ editor: customise colours, font and background

Ticket: https://github.com/toinguyen-agilityio/super-board/issues/3 · Analysed from the ticket text only.

## What's asked

Add a customise panel to the editor with 5 colour palettes, 3 fonts that render Vietnamese diacritics, and a JPG/PNG background upload (≤ 5 MB, Vietnamese error otherwise) with a "Xoá ảnh nền" reset button. The preview updates immediately and typed form values are kept.

## What's vague (questions for the PO)

1. **Palettes and fonts:** which 5 palettes (names, text and accent colours) and which 3 fonts? Who decides?
2. **Template defaults:** before the user picks anything, does the preview use the template's own colours and font? Does picking a palette override them for every template?
3. **"No fallback glyphs":** how do we verify that? A visual check, a screenshot test, or a list of characters to test?
4. **5 MB:** 5,000,000 bytes or 5 MiB (5,242,880)? Exactly 5 MB passes?
5. **File types:** JPG and PNG only. What about WebP or HEIC from iPhones? Is the check by MIME type or extension?
6. **Error text:** what is the exact Vietnamese wording for "too big" and "wrong type"? When does the message disappear?
7. **Image fit:** cover, contain or tile? Can the user move or zoom it?
8. **"Xoá ảnh nền":** hidden or disabled when there is no custom background?
9. **Persistence:** do customisations survive a reload or switching template?

## First step

Get the palette and font lists and the exact 5 MB rule from the PO, then write unit tests for the background validation (type, size boundary) before building the panel.
