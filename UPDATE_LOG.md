# UPDATE LOG — ver 119
**Serial:** SHJ-119  
**Date:** 2026-06-07  
**Base:** ver 118 (SHJ-118)

---

## PATCH_v117 — Print Page Layout Redesign (Correct)

### Problem
PATCH_v116 (ver 118) produced a broken layout:
- Left side showed 5 huge vertical colored strips (buttons stretched full-height)
- Preview area was too small
- Sidebar was wrong direction

### Fix — Single vertical-column layout

```
┌─────────────────────────────────────────────┐
│      DOCUMENT PREVIEW (full width)          │
│      max-width: 1000px, centered            │
│      background: #9ba3b2                    │
└─────────────────────────────────────────────┘
  ☑  Add Signature Section
  Customer Copy        [ 1 ]
  Agent Copy           [ 0 ]
  Gate Pass Copy       [ 0 ]
            [ PRINT ]         ← 300px, centred, blue
  [ JPG ]  [ PDF ]  [ SAVE ]  [ EDIT ]
```

### Changes
- `#est-page-view` rebuilt as vertical scroll container (no sidebar)
- All PATCH_v116 panels hidden/removed
- Preview band: full-width, max-width 1000px, centred, grey background
- Signature checkbox row below preview
- 3 copy count inputs (Customer / Agent / Gate Pass)
- Single large PRINT button (300px, dark blue)
- Bottom row: JPG | PDF | SAVE | EDIT equal flex buttons
- Print opens single popup with all copies as separate pages
- window.open() called synchronously — no popup blocking

---

## Previously applied patches (ver 118 base)
PATCH_v106 through PATCH_v116 — see ver 118 UPDATE_LOG.md
