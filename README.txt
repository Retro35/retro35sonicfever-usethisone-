╔══════════════════════════════════════════════════════╗
║        SONIC 1 FOREVER — WEB EDITION                ║
║              Ready-to-host folder                   ║
╚══════════════════════════════════════════════════════╝

WHAT'S HERE
───────────
  index.html      ← Web launcher (open this in a browser)
  Data.rsdk       ← Game data (38 MB, already included)
  index.js        ← ⚠ DROP IN: WASM engine glue (see below)
  index.wasm      ← ⚠ DROP IN: WASM engine binary (see below)
  Forever.ini     ← Game config
  Mods/           ← Sonic 1 Forever mod files
  SonLVLObjDefs/  ← Level object definitions


HOW TO ADD THE MISSING FILES
─────────────────────────────
  1. Go to: https://github.com/grubbyplaya/Sonic-1-WASM
  2. Click "Code" → "Download ZIP"
  3. From the ZIP, copy:
       index.js   → into THIS folder (replace the empty file)
       index.wasm → into THIS folder (replace the empty file)
  (You do NOT need index.data or index.html from that repo)


HOW TO RUN
───────────
  Option A — Python (quickest):
    Open a terminal in this folder and run:
      python3 -m http.server 8000
    Then open: http://localhost:8000

  Option B — VS Code Live Server:
    Right-click index.html → "Open with Live Server"

  Option C — Host online:
    Upload this entire folder to GitHub Pages, Netlify,
    or any static HTTPS host.

  ⚠ IMPORTANT: Must be served via http:// or https://.
    Double-clicking index.html (file://) will NOT work.


CONTROLS
─────────
  Mobile  : On-screen D-pad + buttons (appear automatically)
  Keyboard: Arrow keys, Z = Jump, X = Spin Dash,
            Enter = Start, Esc = Pause, F = Fullscreen
  Gamepad : Any USB or Bluetooth controller works


CREDITS
────────
  Sonic 1 Forever      — Team Forever
  RSDKv4 Decompilation — RSDKModding / Rubberduckycooly
  WASM build           — grubbyplaya / mattConn
  Web launcher         — generated for this release
