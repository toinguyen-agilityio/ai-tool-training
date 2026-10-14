# 🐛 [bug] download: PNG file name drops non-Latin names

Bug found while analysing [super-board #4](https://github.com/toinguyen-agilityio/super-board/issues/4) (vague point Q1 in [issue-04.md](issue-04.md)), then reproduced in the running app (`npm run dev`, Chromium) by clicking through the UI. Written in super-board's ticket format (`docs/agents/issue-tracker.md`).

**Ticket:** https://github.com/toinguyen-agilityio/super-board/issues/11

## Problem
When the bride's or groom's name has no Latin letters (Chinese, Korean, emoji…), "Tải về" saves the PNG without that name. The preview shows `李华 & Trần Văn Đức`, but the file is called `thiep-cuoi--Tran-Van-Duc.png`, so the couple and their guests cannot tell whose invitation it is.

## Context
- **Where:** editor, `/tao?mau=co-dien`, "Tải về" button
- **Who:** a couple where at least one partner has a non-Latin name (e.g. mixed-nationality weddings)
- **Env:** `staging` @ `b2071a8`, `npm run dev` on `http://localhost:3000`, Chromium, desktop 1280×900
- **How it was found:** reproduced in the running app on 14/10/2026 by clicking through the UI, not by reading code

![editor with 李华 · desktop](evidence/issue-11-lihua-editor.png)

## Reproduce steps
1. Open `http://localhost:3000/`
2. Click the "Cổ điển" template card; the URL becomes `/tao?mau=co-dien`
3. Tên cô dâu: `李华`
4. Tên chú rể: `Trần Văn Đức`
5. Ngày giờ: `20/12/2026 18:00`
6. Địa điểm: `Nhà hàng Hoa Sen, Đà Nẵng`
7. Check the preview: it shows `李华 & Trần Văn Đức` correctly
8. Click "Tải về" and look at the saved file name

**Expected:** the file name contains the bride's name, e.g. `thiep-cuoi-李华-Tran-Van-Duc.png`
**Actual:** `thiep-cuoi--Tran-Van-Duc.png` (bride's name missing, double `-`)

Other inputs tried with the same steps:

| Tên cô dâu | Tên chú rể | Saved file name | Result |
|---|---|---|---|
| `李华` | `Trần Văn Đức` | `thiep-cuoi--Tran-Van-Duc.png` | ❌ bride missing |
| `김민지` | `Park Ji-hoon` | `thiep-cuoi--Park-Ji-hoon.png` | ❌ bride missing |
| `😀` | `🎉` | `thiep-cuoi--.png` | ❌ both missing |
| `Nguyễn Thị Hằng` | `Trần Văn Đức` | `thiep-cuoi-Nguyen-Thi-Hang-Tran-Van-Duc.png` | ✅ OK |

Each row was run once in the browser. The PNG content itself is fine; only the file name is wrong.

## Fix
Keep every name in the file name. Open question for the PO: keep non-Latin letters as typed (`thiep-cuoi-李华-...`) or fall back to a placeholder (`thiep-cuoi-co-dau-...`) when a name has no Latin letters? Likely cause: `slug()` in `lib/download.ts` deletes everything outside `[A-Za-z0-9-]`.

## Acceptance Criteria
- [ ] With bride `李华` and groom `Trần Văn Đức`, "Tải về" saves a file whose name has no empty part (no `--`)
- [ ] A name made only of emoji or symbols still produces a non-empty part in the file name
- [ ] Vietnamese names keep today's behaviour: `Nguyễn Thị Hằng` + `Trần Văn Đức` → `thiep-cuoi-Nguyen-Thi-Hang-Tran-Van-Duc.png`
- [ ] Characters unsafe in file names (`/ \ : * ? " < > |`) are still removed
- [ ] A unit test in `lib/download.test.ts` covers the non-Latin and emoji cases

## Risk
🟢 **Low** · only the download file name changes; the PNG content and the editor are untouched

## Blocked by
- None.
