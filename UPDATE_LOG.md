## v106 — 2026-06-06 | S/N: SHJ-106-060626

**Files changed:** `index.html`

### FIX — JS source code visible as page text ("file freeze")
All patch script blocks contained `/* </script> */` and `/* <script> */` marker lines.
The HTML parser terminates a `<script>` element on the first raw `</script>` it sees,
regardless of surrounding JS comment syntax. This caused the browser to exit the
script block early and render the remaining JS as visible page text.

**Fix:** Removed all four marker lines globally from every patch block (v100 / v101 / v102 / v103).

**Verified:** 0 `/* </script> */` patterns · 0 script leaks · 0 stray `-->` · CLEAN ✓

### FIX — Est sub-tab bar invisible (carried from v105)
`#est-nav` had no CSS. Injected scoped styles for blue bar + gold active underline.

### NEW — 📊 All Records 5th sub-tab (carried from v105)
EST + PI combined table, date-sorted, inline-editable party name, search/filter,
Open · Reprint · PDF actions per row.

---

## v105 — 2026-06-06 | S/N: SHJ-105-060626

**Files changed:** `index.html` (add PATCH_v103.js block before `</body>`)

### FIX — Est sub-tab bar invisible (white text on white background)
`#est-nav` used class `inv-nav` which had no CSS definition.
Injected scoped CSS for `#est-nav .inv-tab`:
- Blue background (`#1a3a6b`), white text, gold active underline (`#ffd700`)
- All 4 buttons (New / Preview / Saved / Grid Entry) now clearly visible

### NEW — "All Records" 5th sub-tab (EST + PI combined table)
A new 📊 **All Records** tab added to the Estimate section sub-nav.

| Column | Notes |
|--------|-------|
| Date | Formatted DD/MM/YY, newest first |
| Type | EST (blue badge) / PI (amber badge) |
| Number | EST-YYYY-XXXX or PI-2026-XXXX |
| Party Name | **Inline editable** — click to edit, saves to localStorage |
| Amount | Grand total in ₹ |
| Actions | 👁 Open · 🖨 Reprint · ⬇ PDF |

- Search bar filters by party name or document number
- Type dropdown: All / Estimate / Proforma Invoice
- Party name edit saves directly back to `shj_estimates` or `shj_pi`
- Reprint opens the preview + print-setup panel
- PDF triggers download JPG / piPDF depending on type

---

## v104 — 2026-06-06 | S/N: SHJ-104-060626

**Files changed:** `index.html`

### FIX — Stray HTML comment close rendering as visible print text

A bare `-->` text node sat outside any HTML comment block between the estimate section
closing `</div>` and the Money Flow `<script>` tag. Browsers rendered it as visible
page content — appearing in print preview as a line of `════...════ -->`.

**Fix:** Removed the orphaned line. No content or functionality affected.

**Verified:** 0 stray `-->` nodes · 0 `</script>` leaks · CLEAN ✓

---

# Shreeji Industries — Full System Update Log

---

## v103 — 2026-06-05 | S/N: SHJ-103-050626

**Files changed:** `index.html`

### FIX — Script injection error (</script> leak)
Stripped HOW-TO-APPLY block comments from all 3 embedded patch scripts.
Verified: 0 bare </script> tokens inside any script block.

### CLEAN — Version stamps unified
Title, shj-build meta, service-worker cache, PIN footer all stamped v103/SHJ-103-050626.

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
