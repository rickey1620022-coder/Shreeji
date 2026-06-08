# UPDATE LOG — ver 120
**Serial:** SHJ-120  
**Date:** 2026-06-07  
**Base:** ver 119 (SHJ-119)

---

## PATCH_v119 — Estimate Tab: ⚡ Grid Entry (4th Sub-Tab)

### Problem
Estimate tab had only 3 sub-tabs (New / Preview / Saved).
Report (Shreeji_System_Report.pdf + UI_Manual_v2.pdf) required a
high-speed tabular "Data Entry Boy" grid layout for rapid keyboard entry.

### Fix
Added **⚡ Grid Entry** as the 4th sub-tab inside the Estimate section.

### UI Layout
```
┌─────────────────────────────────────────────────────────┐
│  📝 New  |  🖨 Preview  |  📋 Saved  |  ⚡ Grid Entry  │
└─────────────────────────────────────────────────────────┘

 [Estimate No.]  [Date]  [Party Name............]  [GSTIN]

 ┌──────┬──────────────────────┬──────┬──────┬────────┬────────┬───┐
 │ S.No │ Item Description     │  Qty │  UOM │ Rate ₹ │ Total ₹│   │
 ├──────┼──────────────────────┼──────┼──────┼────────┼────────┼───┤
 │  1   │ [___________________]│[____]│  kg  │[______]│   0.00 │ ✕ │
 │  2   │ [___________________]│[____]│  pcs │[______]│   0.00 │ ✕ │
 └──────┴──────────────────────┴──────┴──────┴────────┴────────┴───┘
 [＋ Add Row]

                              Sub Total       ₹ 0.00
                  ☐ Previous Balance ₹  [______]
                  ☐ Freight ₹          [______]
                              Taxable         ₹ 0.00
                  ☐ Tax %              [  18  ]
                              Tax Amt         ₹ 0.00
                          ─────────────────────────
                              Grand Total     ₹ 0.00

 [🗑 Clear]    [↗ Send to New Tab]    [🖨 Print]
```

### Technical Changes
- `#est-nav` — 4th tab button `id="est-tab-grid"` added
- `#est-page-grid` — new page div with full tabular grid UI
- `estGo()` — pages array updated to `['new','view','list','grid']`
- `grdInit()` called on first open; seeds 5 blank rows, syncs date & Est No.
- `parseFloat(value || 0)` on all inputs — prevents NaN totals
- Checkbox-gated footer: Previous Balance, Freight, Tax %
- **Print** — opens separate popup, forced borders + footer totals
- **Send to New Tab** — copies all rows into main Estimate form

### New JS Functions
`grdInit` · `grdFillParty` · `grdMakeRow` · `grdAddRow` · `grdDelRow`  
`grdCalcRow` · `grdCalcFooter` · `grdKey` · `grdClear` · `grdCopyToNew` · `grdPrint`

### Files Changed
- `files/index.html`
- `files/Products-Code.gs` (improved — date coercion fix, SAVE_ESTIMATE handler added)

---

## Products-Code.gs Improvements (same patch)

### Bug Fixes
- `readSheet()` — Google Sheets returns Date objects, not strings.
  Now coerced: `v instanceof Date → v.toISOString().slice(0,10)`
  This was causing broken `updatedOn` values in the app.
- `getSS()` — wrapped in try/catch so standalone deployment doesn't throw.

### New Features
- `SAVE_ESTIMATE` / `GET_ESTIMATES` actions — estimates can sync to
  a separate `ESTIMATES` tab in the same Products spreadsheet.
- `testSetup()` — run from Apps Script editor to verify sheet connection
  before deploying.

### Verified Working
URL tested live via browser on 2026-06-07:  
`https://script.google.com/macros/s/AKfycby…/exec?action=GET_PRODUCTS`  
Response: `{"status":"ok","data":[4 products]}` ✅

---

## Previously applied patches (ver 119 base)
PATCH_v106 through PATCH_v117 — see ver 119 UPDATE_LOG.md
