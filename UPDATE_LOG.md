# Update Log

## v117 / SHJ-117 — 2026-06-07
### PATCH v113: Definitive 10-row fix
- ROOT CAUSE found: `let estItems` (line 6173) does NOT create window.estItems
  in ES6. All previous patches wrote to window.estItems (a separate, unused
  variable). The app's closures always used the local `let estItems`.
- FIX: Count actual <tr> rows in #est-items-tbody, call window.estAddItem()
  for each missing row. estAddItem() is a function declaration so
  window.estAddItem === local estAddItem — it pushes to the correct
  closure variable and calls the correct estRenderItems().
- Init retries at 200ms, 600ms, 1500ms to handle late app initialization
- estNew / estLoad / estRemoveItem hooks also use ensureTenRows via DOM count

## v116 / SHJ-116 — 2026-06-07
### PATCH v112: Estimate print format (A4, compact, Delhi India, footer fix)

## v115 / SHJ-115 — 2026-06-07
### PATCH v111: Unfreeze Generate button + fix optional items
