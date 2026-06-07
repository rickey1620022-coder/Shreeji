# Shreeji Industries App — Update Log

## v111 / SHJ-111 — 2026-06-07
### PATCH v107: Google Sheet Sync for Estimate tab
- **Live URL hardcoded**: https://script.google.com/macros/.../exec (user's live GAS deployment)
- **Push**: Every estimate/PI save automatically POSTs PUSH_ESTIMATE to the sheet (silent, no alert)
- **Pull**: On app load + every 30 min, pulls products + estimates from sheet
  - Products merged into localStorage `shj_products` (sheet is authoritative — always latest version)
  - Estimates cross-checked by estNo — already-local records skipped (zero doubling)
  - `purgeKeys` from sheet applied to localStorage (20-day server-side rule)
- **20-day local purge**: Client-side also purges records older than 20 days on every pull
- **Backward compatible**: Works with old Products-Code.gs `{"status":"ok","data":[...]}` AND new product.gs format
- **Status dot**: Small colour dot (bottom-right) — orange=syncing, green=ok, red=error
- **Settings row**: ☁ SHEET SYNC row in Estimate tab — change URL, force re-sync
- **Helpers**: `shjGetProduct(code)` returns product object; `shjAllProductCodes()` returns sorted code list

## v110 / SHJ-110 — 2026-06-07
### PATCH v106: Fix all 3 Print tab issues
- Print popup carries full CSS, calls estRenderPreview() first so doc is never blank
- PDF uses window.html2pdf (CDN already loaded) — no more JPG fallback
- Customer/Agent/Packing copy panel injected directly into #est-page-view

## v109 / SHJ-109 — 2026-06-07
### PATCH v105: Fix PWA print

## v108 / SHJ-108 — 2026-06-07
### PATCH v103 + v104: 4-tab nav + All Records

## v107 — 2026-06-06 (internal)

## v104–v106 — 2026-06-06
### Core patches: Estimate + PI, WhatsApp, Audit, Roles, Records
