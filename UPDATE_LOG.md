# Update Log

## v116 / SHJ-116 — 2026-06-07
### PATCH v112: Estimate print format — final spec
- A4 paper, estimate compact at top (~A5 landscape block), blank space below — no stretching
- Company address: "Delhi, India" only (removed h-72, Gali No.1... full address)
- Party Name + Contact Person always grouped together
- Table columns: S.No | Qty | Item Description | Rate ₹ | Amount ₹
- Footer fully visible — page-break-inside:avoid, break-inside:avoid
- Margins: 10mm all sides via @page
- Disabled estScaleDoc() transform in print context (was breaking layout)
- Identical output: browser print = PDF popup = physical print
- Print popup carries self-contained PRINT_CSS — no dependency on page stylesheets

## v115 / SHJ-115 — 2026-06-07
### PATCH v111: Unfreeze Generate button + optional items + 10 rows

## v114 / SHJ-114 — 2026-06-07
### PATCH v110: 10 rows + compact optional items

## v111 / SHJ-111 — 2026-06-07
### PATCH v107: Google Sheet sync
