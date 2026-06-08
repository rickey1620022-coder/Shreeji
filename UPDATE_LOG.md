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
| Fixed `estGo` map | `grid:'grid'` (was `grid:'est'`) |
| Added Push/Pull buttons to `est-page-all` | Visible in Records tab |

### Result
Estimate sub-tabs now show all 5:
```
📝 Estimate | 📄 PI | 🖨 Print | 📋 Records | ⚡ Grid
```

- **⚡ Grid** → opens high-speed tabular data entry form
- **📋 Records** → shows "↑ Push to Sheet" and "↓ Pull from Sheet" buttons

### Products-Code.gs Fix (also included)
Field name mismatch fixed — app sends `custName/custContact/custGST/grand`
but script expected `customer/contact/gstin/grandTotal`. Both variants now accepted.
Customer names, contacts, and amounts will appear correctly in Google Sheet
after clicking ↑ Push to Sheet.

---

## How to Deploy
1. Upload `ver 123/files/index.html` to GitHub:
   `rickey1620022-coder/Shreeji` → `main/index.html`
2. App auto-detects v123 > v121 → downloads → prompts restart
3. Click "Restart & Update" → app relaunches with all fixes

---

## Previously Applied Patches
PATCH_v100 through PATCH_v121 — see ver 121 UPDATE_LOG.md
