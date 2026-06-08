# UPDATE LOG — ver 121
**Serial:** SHJ-121  
**Date:** 2026-06-08  
**Base:** ver 118 (SHJ-118) — actual running file  

---

## PATCH_v121 — Estimate Tab: ⚡ Grid Entry (4th Sub-Tab)

### Problem
- Estimate section had only 3 sub-tabs: New | Preview | Saved
- No high-speed tabular data-entry layout existed
- Previous patches (ver 119, ver 120) applied to wrong file — app was loading from `ver 118/files/index.html`

### Fix
Added **⚡ Grid Entry** as the 4th sub-tab inside the Estimate section, applied directly to `ver 118/files/index.html`.

### UI Layout
```
┌──────────────────────────────────────────────────────────────┐
│  📝 New  │  🖨 Preview  │  📋 Saved  │  ⚡ Grid Entry ←NEW  │
└──────────────────────────────────────────────────────────────┘

 [Est No.]  [Date]  [Party Name.................]  [GSTIN]

 ┌──────┬──────────────────────┬──────┬──────┬────────┬────────┬───┐
 │ S.No │ Item Description     │  Qty │  UOM │ Rate ₹ │ Total ₹│   │
 ├──────┼──────────────────────┼──────┼──────┼────────┼────────┼───┤
 │  1   │ [_________________]  │[___] │  kg  │[______]│   0.00 │ ✕ │
 │  2   │ [_________________]  │[___] │  pcs │[______]│   0.00 │ ✕ │
 └──────┴──────────────────────┴──────┴──────┴────────┴────────┴───┘
 [＋ Add Row (or press Enter)]

                          Sub Total           0.00
              ☐ + Previous Balance ₹  [______]
              ☐ + Freight ₹           [______]
                          Taxable Amt         0.00
              ☐ + Tax %               [  18  ]
                          Tax Amount          0.00
                      ─────────────────────────────
                          Grand Total ₹       0.00

 [🗑 Clear]    [↗ Send to New Tab]    [🖨 Print]
```

### Technical Changes Made to `ver 118/files/index.html`
| What | Detail |
|------|--------|
| Tab button | `id="est-tab-grid"` added to `#est-nav` |
| Page div | `id="est-page-grid"` added before Product Picker modal |
| estGo() | Pages array: `['new','view','list']` → `['new','view','list','grid']` |
| estGo() | Added `if(page==='grid') grdInit()` |
| JS functions | 11 new functions added (see below) |

### New JS Functions
| Function | Purpose |
|----------|---------|
| `grdInit()` | Seeds 5 rows on first open, syncs date & Est No |
| `grdFillParty()` | Auto-fills GSTIN from saved customers |
| `grdMakeRow(num)` | Builds one table row with inline inputs |
| `grdAddRow()` | Appends new row, focuses first input |
| `grdDelRow(num)` | Removes a row |
| `grdCalcRow(num)` | Qty × Rate → Total cell, `parseFloat(v\|\|0)` |
| `grdCalcFooter()` | Recalcs Sub Total, Taxable, Tax Amt, Grand Total |
| `grdKey(event,num)` | Enter key → add next row |
| `grdClear()` | Resets all rows and footer fields |
| `grdCopyToNew()` | Pushes all rows into main Estimate form |
| `grdPrint()` | Opens print-ready popup with forced borders |

### Files in ver 121
- `index.html` — ver 118 base + Grid Entry tab (12,856 lines)
- `Products-Code.gs` — improved version with date-coercion fix + SAVE_ESTIMATE handler
- `UPDATE_LOG.md` — this file

---

## Root Cause: Wrong File was Being Edited

Previous work (ver 119, ver 120) edited `ver 119/files/index.html` but the Electron app (`shreeji-desktop`) loads:

```
C:\shreeji data db\ver 118\files\index.html
```

This was confirmed by checking:
- `shreeji-desktop/main.js` → `win.loadFile(path.join(__dirname,'src','shreeji-full-system-v47.html'))`
- App title "Full System v118 PWA" matched only `ver 118/files/index.html`
- `pdbGetUrl`, `estGo`, `est-tab-new` all found at expected lines in ver 118

### Products-Code.gs Status
URL tested live: `https://script.google.com/macros/s/AKfycbw…/exec?action=GET_PRODUCTS`  
Response: `{"status":"ok","data":[4 products]}` ✅ — working correctly.  
App-side: ensure Product DB URL box shows this URL and tap **Test** to reconnect.

---

## Previously Applied Patches (ver 118 base)
PATCH_v106 through PATCH_v117 — see ver 118 UPDATE_LOG.md
