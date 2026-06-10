# UPDATE LOG — ver 125
**Serial:** SHJ-125
**Date:** 2026-06-10
**Base:** ver 124 (SHJ-124)

---

## PATCH_v125 — PDF ALL button (all copies in one PDF)

### Change
Added **📄 PDF ALL** button left of PRINT ALL on the Print tab.

Clicking PDF ALL combines all selected copies (Customer Copy + Agent Copy + Gate Pass) into **one PDF file** and downloads it as `[EstNo]-ALL.pdf`.

Each copy respects the same column rules as print: Customer = Rate+Qty+Total, Agent = Qty+Total, Gate Pass = Qty only. Signature section included if checkbox is ticked.

---

# UPDATE LOG — ver 124
**Serial:** SHJ-124
**Date:** 2026-06-10
**Base:** ver 123 (SHJ-123)

---

## PATCH_v124 — Print Tab UI Redesign v2 + Sticky Bottom Toolbar

### Changes

| # | Change | Detail |
|---|--------|--------|
| 1 | Preview first | Print preview (`#est-doc`) shown at top, full-width, before copy controls |
| 2 | Copy defaults = 0 | Customer Copy, Agent Copy, Gate Pass all default to 0; blank auto-corrects to 0 |
| 3 | Renamed Packing → Gate Pass | `id:'gatepass'`, label `🏷 Gate Pass` |
| 4 | Single PRINT ALL button | Right-aligned, removed old 3-button row (PRINT ALL COPIES / PDF / JPG) |
| 5 | Sticky bottom toolbar | Fixed bar on all tabs: ✏ Edit · 🖨 Print · 🖼 JPG · 📄 PDF · 💾 Save |
| 6 | Version stamps synced | title, shj-build meta, SW cache (shreeji-v124), footer S/N all updated |

### Result
Print tab layout: preview on top → copy count controls below → right-aligned Print All button.
Sticky bar always visible at bottom on all tabs (mobile + desktop).

---

# UPDATE LOG — ver 123
**Serial:** SHJ-123
**Date:** 2026-06-08
**Base:** ver 121 (SHJ-121)

---

## PATCH_v123 — Fix: ⚡ Grid Entry Tab + ↑ Push to Sheet Button

### Problem
PATCH_v104 (already in the file) was rebuilding `est-nav` at runtime via JavaScript,
destroying the Grid Entry tab added in v121. It also mapped `grid → 'est'` (wrong),
so clicking Grid Entry opened the New Estimate form instead.

The "↑ Push to Sheet" button was unreachable because the RECORDS tab shows
`est-page-all` (PATCH_v103 combined view), not `est-page-list` where the button lived.

### Fixes Applied to PATCH_v104

| Fix | Detail |
|-----|--------|
| Added `⚡ Grid` to `buildNav()` | 5th tab now rendered at runtime |
| Added `'grid'` to `setActive()` | Tab highlights correctly when active |
| Added `grid` case in `shjTab()` | Shows `est-page-grid`, calls `grdInit()` |
| Fixed `estGo` map | `grid:'g