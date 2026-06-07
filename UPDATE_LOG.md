# UPDATE LOG — ver 116 / v118 / SHJ-118

**Date:** 2026-06-07  
**Base:** ver 115 (v117 / SHJ-117)  
**Patch:** PATCH_v114

## Changes

### FIX 1 — Blank rows: no qty / rate / total shown
When an item row has no description, the S.No, Qty, Rate ₹, and Total ₹ cells
are now cleared (blank). Previously they showed default values: qty=1, rate=0.00,
total=0.00, making blank filler rows visually noisy.

### FIX 2 — Party / Contact name in print
Party name and Contact were appearing as empty or box-like elements in the
generated estimate print/preview. Now:
- Spans are explicitly styled as plain text (no border, no background).
- If the span was empty (rec.custName not collected at generation time), the
  patch re-reads the value from the live form inputs and writes it in.
- If the Contact row was missing entirely, the patch injects it from the form.

## Build info
- Source: ver 115/files/index.html + PATCH_v114.js
- Output: ver 116/files/index.html
- Version stamp: v118 | SHJ-118-070626 | 2026-06-07
