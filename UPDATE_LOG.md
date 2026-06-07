# UPDATE LOG — ver 117 / v119 / SHJ-119

**Date:** 2026-06-07  
**Base:** ver 116 (v118 / SHJ-118)  
**Patch:** PATCH_v115

## Changes

### FIX — Print button not working (root cause fix)

**Root cause:**  
PATCH_v106 overrode `window.estPrintDoc` to wrap `window.open()` inside  
a `setTimeout(150ms)`. Browsers treat `window.open()` called from inside  
a setTimeout as *not user-initiated* and **silently block the popup**.  
Additionally, PATCH_v106's closure called its own local `shjPrintPopup`  
(not `window.shjPrintPopup`), so PATCH_v112's corrected print CSS was  
never reached.

**Fix:**  
PATCH_v115 overrides `window.estPrintDoc` to call `window.shjPrintPopup`  
(PATCH_v112's version) **synchronously** — no setTimeout, user-gesture  
chain intact, popup not blocked.  
This also ensures the correct A4 portrait / 10mm margin print CSS  
(defined in PATCH_v112) is used every time.

**Fallback:** If `window.shjPrintPopup` is unavailable for any reason,  
a self-contained inline popup with identical CSS opens instead.

## Build info
- Source: ver 116/files/index.html + PATCH_v115.js
- Output: ver 117/files/index.html
- Version stamp: v119 | SHJ-119-070626 | 2026-06-07
