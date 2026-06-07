# Update Log

## v115 / SHJ-115 — 2026-06-07
### PATCH v111: Unfreeze Generate button + fix optional items + 10 rows
- FIX: Generate Estimate button intercepted by PATCH_v105 (🖨 emoji match)
  → cloned button to remove rogue listener, marked to skip future interception
- FIX: Previous Balance / Less Payment / Freight / Tax inputs non-interactable
  → reset CSS to clean state with pointer-events:auto, position:static
- FIX: 10 blank rows always on open (setTimeout 25ms after estNew)
- "+ Add Row" button label applied

## v114 / SHJ-114 — 2026-06-07
### PATCH v110: 10 rows + compact optional items (partial)

## v111 / SHJ-111 — 2026-06-07
### PATCH v107: Google Sheet sync
