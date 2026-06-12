VER 129 — SHJ-129-120626 — 2026-06-12
======================================
Version bump only (no feature change). Upload this index.html to
GitHub to push the desktop exe auto-update.

WHY THE EXE SAID "v127 IS LATEST":
GitHub already has your v128 upload, complete and correct.
But raw.githubusercontent.com (which the exe checks) caches files
for ~5 minutes — your exe checked before the cache refreshed.

WHAT TO DO:
1. Upload this index.html to GitHub (replace the old one).
2. Wait 5 minutes.
3. In the exe: File -> Check for Updates. It should now offer v129.
4. After upload, open this link in a browser and check the file
   ends with </html> :
   https://raw.githubusercontent.com/rickey1620022-coder/Shreeji/main/index.html

Next version when making new changes: v130
