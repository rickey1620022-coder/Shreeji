## v109 — 2026-06-07 | S/N: SHJ-109-070626

**Files changed:** `index.html` (add PATCH_v105.js before `</body>`)

### FIX — PWA print: "This app doesn't support print preview"

Windows PWA apps cannot show browser print preview inline.
PATCH_v105 overrides `estPrintDoc()` and all print buttons to open the
estimate / PI document in a **new browser window** and call `window.print()`
from there. The new window is a normal browser tab — full print preview works.

- If popup is blocked, falls back to `window.print()` in the PWA
- Also patches PATCH_v101's copy-type print buttons
- MutationObserver re-patches any print buttons injected lazily

---
## v108 — 2026-06-07 | S/N: SHJ-108-070626

**Files changed:** `index.html`

### REBUILD — Clean injection fix (root cause of all "file freeze" bugs)

All previous versions (ver 103–105) injected patches at the first `</body>` tag,
which is inside a JavaScript print-template string in PATCH_v100, not the HTML
closing tag. This placed new patches inside the main `<script>` block, where the
injected `</script>` terminates it early — causing all subsequent JS to render
as visible page text.

**Fix:** Rebuilt from ver 100 (last clean base). Patches v103 and v104 are now
injected before the real standalone `</body>` at the end of the file.
Also removed `/* </script> */` / `/* <script> */` markers from all patch blocks,
and removed the stray `-->` text node.

**Verified:** 0 script leaks · 0 stray `-->` · CLEAN ✓

### FEATURE — 4-tab Estimate nav (from PATCH_v104)
📝 ESTIMATE | 📄 PI | 🖨 PRINT | 📋 RECORDS
All tabs built with inline styles — always visible, blue bar, gold active underline.

### FEATURE — All Records combined table (from PATCH_v103)
📊 RECORDS tab: EST + PI combined, date-sorted, inline-editable party name,
search/type filter, Open · Reprint · PDF per row.

---
# Shreeji Industries — Full System Update Log

---

## v102 — 2026-06-05 | S/N: SHJ-102-050626  ★ SPEC COMPLETE

- PI WhatsApp PDF + PDF+Text buttons
- PI Records Save action
- Download JPG (html2canvas)
- WhatsApp JPG real image (Web Share API)
- Audit trail (auto-log all saves/edits)
- Permissions: Admin/Agent roles, Agent hides Rate

---

## v101 — 2026-06-05 | S/N: SHJ-101-050626

- Customer/Agent/Packing copy-type print modes
- Copy count selector + multi-print
- Signature section checkbox
- PI Records screen with filters + actions
- Estimate Records UI + Reprint flow

---

## v100 — 2026-06-05 | S/N: SHJ-100-050626

- Rate-history dropdown (selectable, last 10)
- Share & Print auto-opens after save
- WhatsApp actions wired to Estimate

---

## v99 — 2026-06-05 22:00 | S/N: SHJ-99-050626

**Files changed:** `index.html`

### FIX — Version metadata cleanup
All version stamps unified to v99:
- `<title>` updated v98 → v99
- `shj-build` meta updated v98 → v99 / SHJ-98 → SHJ-99
- Service-worker `CACHE_NAME` updated `shreeji-v98` → `shreeji-v99`
- PIN footer serial updated SHJ-96 → SHJ-99

### CONFIRM — Estimate tab
Estimate tab confirmed working as designed:
- **ESTIMATE** mode: no tax, subtotal = total
- **PROFORMA INVOICE** mode: GST + freight shown
- Editable row numbers: 1, 2, 3, 2a, 3a etc.

---

## v95 — 2026-06-05 18:00 | S/N: SHJ-95-050626

**Files changed:** `index.html`, `Products-Code.gs`

### NEW — Estimate Tab: 2 document types
| Toggle | Behaviour |
|--------|-----------|
| **📝 ESTIMATE** | No tax. Items → Subtotal = Total |
| **📄 PROFORMA INVOICE (PI)** | Items → Subtotal + Freight = Taxable Amount + GST % = Grand Total |

- Customer auto-fill from Customer DB  
- Product code lookup from Product DB  
- Row numbering editable per line: 1, 2, 3, 2a, 3a  
- Document numbers: `EST-YYYY-XXXX` / `PI-YYYY-XXXX` (auto-switch on type toggle)  

### NEW — A5 Landscape print format
- Document size: 794 × 560 px (A5 landscape at 96 dpi)
- Compact slip style: centered header → party/doc row → table → totals → footer
- PDF export uses landscape orientation
- Freight + GST rows visible only on PI type

### FIX — Duplicate JS block removed
- Stale EST engine copy from v94 caused a script parse error
- All 6 `<script>` blocks now validate clean (0 errors)

### UPDATE — Products-Code.gs ESTIMATES sheet
- Added columns: `type`, `freight`, `gstPct`, `gstAmt`, `grand`  
- **Action:** paste new `Products-Code.gs` → Deploy → New Version → same URL

---

## v94 — 2026-06-05 00:00 | S/N: SHJ-94-050626

**Files changed:** `index.html`, `Products-Code.gs`

- NEW 4th main tab `📝 Estimate`
- EST-YYYY-XXXX auto-numbering, customer from Customer DB, product lookup, PDF/JPG export
- Products-Code.gs: SAVE_ESTIMATE / DELETE_ESTIMATE / GET_ESTIMATES handlers

---

## v93 — 2026-06-04 | S/N: SHJ-93-040626

- Product name format: plain lowercase space-separated with code appended  
  e.g. `45mm 18line 4mos white tapping c450`

---

## v92 — 2026-06-04 | S/N: SHJ-92-040626

- Product DB pre-linked to Products sheet URL; 🔌 Test button; auto-connection check on tab open

---

## v91 — 2026-06-04 | S/N: SHJ-91-040626

- Product DB uses its own separate Google Sheet / URL

---

## v90 — 2026-06-04 | S/N: SHJ-90-040626

- NEW Product DB tab (in Invoice & Quotes)

---

## v89 — 2026-06-03 | S/N: SHJ-89-030626

- FIX Desktop window close; `will-prevent-unload` handler in `main.js`

---

## v88 — 2026-06-03 | S/N: SHJ-88-030626

- FIX parseNum comma parsing (`1,000` now correctly = 1000)

---
