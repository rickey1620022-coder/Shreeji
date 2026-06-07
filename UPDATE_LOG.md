# Update Log

## v113 / SHJ-113 — 2026-06-07
### PATCH v109: Unfreeze + compact optional items
- FIX: MutationObserver from PATCH_v108 was changing button textContent which re-triggered
  the observer infinitely → froze Previous Balance input + Generate Estimate button
- FIX: 10 blank rows now correctly initialized without infinite render loop
- NEW: Optional items (Previous Balance / Less Payment / Freight / Tax) text boxes
  are now compact (90px wide), right-aligned, smaller padding — cleaner look

## v112 / SHJ-112 — 2026-06-07
### PATCH v108: Always 10 rows in estimate form (had freeze bug — fixed in v113)

## v111 / SHJ-111 — 2026-06-07
### PATCH v107: Google Sheet sync (live URL wired in)

## v110 / SHJ-110 — 2026-06-07
### PATCH v106: Print / PDF / Copy panel fixes
