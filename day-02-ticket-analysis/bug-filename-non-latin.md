# 🐛 [bug] download: PNG file name drops non-Latin names

Bug found while analysing [super-board #4](https://github.com/toinguyen-agilityio/super-board/issues/4) (vague point Q1 in [issue-04.md](issue-04.md)). Written in super-board's ticket format (`docs/agents/issue-tracker.md`) so it can be filed as an issue there.

## Problem
When the bride's or groom's name has no Latin letters (Chinese, Korean, emoji…), the downloaded PNG loses that name: the file is called `thiep-cuoi--Tran-Van-Duc.png`. Guests and couples cannot tell whose invitation the file is, and a name made only of emoji gives `thiep-cuoi--.png`.

## Context
- **Where:** editor, `/tao?mau=co-dien`, "Tải về" button
  - a. Open `/tao?mau=co-dien`
  - b. Tên cô dâu: `李华`
  - c. Tên chú rể: `Trần Văn Đức`
  - d. Fill in Ngày giờ and Địa điểm with any valid value
  - e. Click "Tải về"
- **Expected:** the file name keeps the bride's name in some form, e.g. `thiep-cuoi-李华-Tran-Van-Duc.png`
- **Actual:** the file is saved as `thiep-cuoi--Tran-Van-Duc.png` (note the double `-`)
- **Who:** a couple where at least one partner has a non-Latin name (mixed-nationality weddings)
- **Env:** `staging` @ `b2071a8` (same `lib/` and `app/` as `main` @ `4469d6c`), any browser

## Root cause
`lib/download.ts` line 10, inside `slug()`:

```ts
.map((word) => word.replace(/[^A-Za-z0-9-]/g, ""))
```

After stripping diacritics, every character outside `A-Z a-z 0-9 -` is deleted. A word made only of non-Latin characters becomes an empty string and is filtered out, so `slug("李华")` returns `""`.

## Reproduce without the UI (fast)
The bug lives in a pure function, so it reproduces in Node 22 with no install:

```bash
git clone https://github.com/toinguyen-agilityio/super-board && cd super-board
git checkout staging
cat > /tmp/run.ts <<'TS'
import { invitationFileName } from "./lib/download.ts";
for (const [b, g] of [["李华", "Trần Văn Đức"], ["김민지", "Park Ji-hoon"], ["😀", "🎉"], ["Nguyễn Thị Hằng", "Trần Văn Đức"]])
  console.log(JSON.stringify([b, g]), "->", invitationFileName(b, g));
TS
cp /tmp/run.ts ./run.ts && node --experimental-strip-types run.ts && rm run.ts
```

Output (run on 13/10/2026):

```text
["李华","Trần Văn Đức"] -> thiep-cuoi--Tran-Van-Duc.png
["김민지","Park Ji-hoon"] -> thiep-cuoi--Park-Ji-hoon.png
["😀","🎉"] -> thiep-cuoi--.png
["Nguyễn Thị Hằng","Trần Văn Đức"] -> thiep-cuoi-Nguyen-Thi-Hang-Tran-Van-Duc.png
```

The last line is the happy path from the existing test, which still passes. The current tests in `lib/download.test.ts` only cover Vietnamese names and ASCII punctuation, so they never hit this case.

## Failing test (to add before the fix)

```ts
it("keeps names that have no Latin letters", () => {
  expect(invitationFileName("李华", "Trần Văn Đức")).not.toContain("--");
});
```

Run with `npm test -- lib/download.test.ts`: it should go red on `staging` today.

## Fix
Open question for the PO first: keep non-Latin letters in the file name (`thiep-cuoi-李华-...`), or fall back to a placeholder (`thiep-cuoi-co-dau-...`) when a name slugs to empty? Either way, `slug()` must never return an empty segment.

## Acceptance Criteria
- [ ] `invitationFileName("李华", "Trần Văn Đức")` returns a name with no empty segment (no `--`)
- [ ] A name made only of emoji or symbols still gives a non-empty segment
- [ ] Existing cases keep passing: `Nguyễn Thị Hằng` → `Nguyen-Thi-Hang`, `Minh/Quân?` → `MinhQuan`
- [ ] Characters unsafe in file names (`/ \ : * ? " < > |`) are still removed

## Risk
🟢 **Low** · one pure function in `lib/download.ts`, covered by unit tests; only the download file name changes

## Blocked by
- None.
