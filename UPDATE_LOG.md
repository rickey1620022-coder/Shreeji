# UPDATE LOG — ver 129
**Serial:** SHJ-129-120626
**Date:** 2026-06-12
**Base:** ver 128 (SHJ-128)

---

## RELEASE_v129 — version bump to push exe auto-update

No functional change. v128 was uploaded to GitHub correctly (verified complete, ends with `</html>`), but the desktop exe reported "v127 is latest" — raw.githubusercontent.com caches the file ~5 minutes, so the exe checked a stale copy. v129 gives a clean newer marker for the updater. Pairs with **product.gs v2** on the Google Sheet side (unified actions, serial numbers, date+time stamps, ARCHIVE sheet).

---

# UPDATE LOG — ver 128
**Serial:** SHJ-128-120626
**Date:** 2026-06-12
**Base:** ver 127 (SHJ-127) — *note: a v127 entry was never written to this log; v127 existed only in index.html*

---

## PATCH_v128 — ThermalSync A5 Print System + file-corruption repair

### 0. CRITICAL FIX — file truncation since v123
Every `index.html` uploaded to GitHub from v123 through v127 was **cut off mid-file**: it ended inside the PATCH v116 comment with an unclosed `<script>` and **no `</body></html>`**. (Last intact upload was v121.) The dangling dead fragment has been removed and the document is properly closed again. Nothing functional was lost — the truncated PATCH v116 print UI had already been replaced by v124, and is now replaced again by v128.

### 1. NEW — A5 print layout engine
| Item | Spec |
|------|------|
| Sheet | A4 portrait 210 × 297 mm, `@page` margin 0 |
| Copies | **2 identical A5-landscape copies** per sheet (cut line dashed) |
| Master box | **195 mm × 133 mm, 2 px solid black border**, drawn first — everything fits inside |
| Strips | 20 mm header · 15 mm party detail · product area (auto-fit) · 15 mm footer |
| Auto-fit | product table font shrinks (9.5 → 6 px) until no overflow / no hidden text |
| Removed | "for Shreeji Industries / Authorised Signatory" — **gone completely** from estimate |
| Optional | `Received By | Signature | Date` row — only when checkbox ticked |

### 2. CHANGE — PRINT tab UI
Preview on top (largest area) → **☑ Add Signature Section** → counters **Customer Copy / Agent Copy / Gate Pass** (blank = 0, negatives blocked, max 99) → centered **PDF | JPG | PRINT ALL** buttons. Preview updates live as quantities change (shows the first copy type with a count, with its column rules). Copy column rules kept from v124: Customer = Rate+Qty+Total · Agent = Qty+Total · Gate Pass = Qty only.

Counts → sheets: N copies of a type = ceil(N/2) full sheets (each sheet always carries 2 identical documents). All counters 0 → one default sheet of 2 customer copies.

### 3. UNIFY — PDF = JPG = PRINT
All three exports render from the **same HTML, same CSS, same mm dimensions** (single layout engine; no separate PDF template). PDF: html2canvas → jsPDF A4 portrait, one page per sheet. JPG: one file per sheet. Print: synchronous popup (user-gesture preserved — v115 lesson).

### 4. RETIRED
`#shj-print-panel-v101`, `#shj-print-setup`, `#shj-copy-panel-v124`, `#shj-sticky-bar-v124` — hidden by CSS and removed on sight (they produced the old, non-matching formats).

### Version stamps (all 4 verified)
`<title>` v128 · `shj-build` v128|SHJ-128-120626|2026-06-12 · SW cache `shreeji-v128` · PIN footer S/N SHJ-128-120626

---

# UPDATE LOG — ver 126
**Serial:** SHJ-126-110626
**Date:** 2026-06-11
**Base:** ver 125 (SHJ-125)

---

## PATCH_v126 — PDF ALL fix + unified product.gs

### 1. FIX — "PDF libraries not loaded." on 📄 PDF ALL

**Root cause:** index.html loaded html2canvas + html2pdf via script tags, but **jsPDF was never loaded**. `pdfAllCopies()` requires `window.jspdf` → it always alerted "PDF libraries not loaded."

**Fixes:**
| # | Fix | Detail |
|---|-----|--------|
| 1 | Static script tag added | `jspdf/2.5.1/jspdf.umd.min.js` now loads at startup (next to html2canvas) |
| 2 | Lazy-load fallback | `shjLoadPdfLibs()` — if libs are still missing when PDF ALL is clicked, they're loaded on demand and the export retries automatically. Alert only shows if the CDN truly can't be reached (offline). |

### 2. FIX — product.gs not working (DEEP CHECK)

**Root cause:** the app calls the web app from TWO modules with DIFFERENT expectations:
| Module | Actions used | Expected reply key |
|--------|--------------|--------------------|
| Product DB tab | GET_PRODUCTS, SAVE_PRODUCT, DELETE_PRODUCT, SAVE_ESTIMATE | `data` |
| Estimate auto-sync (PATCH_v107) | PULL_DATA, PUSH_ESTIMATE | `products` / `estimates` / `purgeKeys` |

- Old **product.gs v1** answered GET_PRODUCTS with key `products` → Product DB tab showed "reply looks wrong" and Pull failed.
- Old **Products-Code.gs (v125)** did not know PUSH_ESTIMATE / PULL_DATA → estimate auto-sync silently failed; estimates never pulled back to other devices.

**Fix: NEW unified `product.gs` v2 (Serial SHJ-126-110626)** — replaces BOTH old files:
| # | Change | Detail |
|---|--------|--------|
| 1 | All actions supported | PULL_DATA, GET_PRODUCTS, GET_ESTIMATES, SAVE/DELETE/SYNC_PRODUCT(S), SAVE/PUSH/DELETE/SYNC_ESTIMATE(S) |
| 2 | Dual reply keys | GET replies carry BOTH `data` and `products`/`estimates` → both app modules work |
| 3 | One estimate handler | SAVE_ESTIMATE and PUSH_ESTIMATE share one upsert (dedup by estNo) — payload shapes of both modules accepted |
| 4 | Sheet header upgrade | Existing v125 ESTIMATES sheet keeps its 14 columns; `purgeDate` + `data` (full JSON) are auto-appended — no data loss |
| 5 | 20-day purge kept | 30-min cron: purge old estimates + dedup PRODUCTS/ESTIMATES. Old rows without purgeDate fall back to date+20 |
| 6 | Serial in replies | Every reply carries `serial: SHJ-126-110626` so you can verify which version is deployed |

**Deploy:** paste `product.gs` into the Apps Script of the Products sheet (delete ALL old code) → Save → Deploy → Manage deployments → ✏ → New version → Deploy. Do NOT create a new deployment (URL must stay the same).

### 3. Version stamps synced
title `v126 PWA` · meta `shj-build v126|SHJ-126-110626|2026-06-11` · SW cache `shreeji-v126` · footer S/N `SHJ-126-110626`

---

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