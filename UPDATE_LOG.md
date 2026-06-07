# UPDATE LOG — ver 118 / v120 / SHJ-120

**Date:** 2026-06-07  
**Base:** ver 117 (v119 / SHJ-119)  
**Patch:** PATCH_v116

## Changes

### Print Page UI Redesign

**New two-panel layout:**
- LEFT: Full document preview (takes all remaining width), scrollable
- RIGHT: 300px control panel (dark theme), sticky

**Control panel (top to bottom):**
- ✍ Add signature section checkbox (checked by default)
- Customer Copies input (default 1)
- Agent Copies input (default 0)
- Gate / Packing Copies input (default 0)
- 🖨 PRINT ALL COPIES (blue, full width)
- 📄 PDF (red)
- 🖼 JPG (green)
- 💾 SAVE (purple)
- ← Back to Edit (grey outline)

**Removed:** duplicate ← Edit / Print / PDF / JPG / Save button bar  
**Removed:** redundant dark PRINT COPIES banner from earlier patches

**PRINT ALL COPIES** now opens ONE popup window containing all copies
as separate print pages (page-break-after between each), instead of
multiple sequential popups. This is more reliable and avoids browser
popup-blocking on the 2nd+ window.

**Mobile (≤680px):** controls panel appears above the preview, stacked.

## Build info
- Source: ver 117/files/index.html + PATCH_v116.js
- Output: ver 118/files/index.html
- Version stamp: v120 | SHJ-120-070626 | 2026-06-07
