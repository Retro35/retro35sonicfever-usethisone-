# Sonic 1 Forever — Web Edition

Play **Sonic the Hedgehog (2013 / RSDKv4)** in any modern browser, with Xbox-style touch controls, mod support, and GitHub Pages hosting.

---

## 🎮 Play Online

> Open `web.html` on your deployed GitHub Pages URL.
> [► Deploy to GitHub Pages](#-github-pages-deployment)

---

## 📁 Repository Structure

```
sonic1-forever/
│
├── web.html              ← Main launcher — START HERE (Xbox touch controls, PWA)
├── directory.html        ← Mod manager, file browser, import tool
├── offline.html          ← Offline / service-worker fallback
├── index.html            ← Original grubbyplaya launcher (alternate entry)
│
├── index.js              ← ⬇ Download from grubbyplaya/Sonic-1-WASM
├── index.wasm            ← ⬇ Download from grubbyplaya/Sonic-1-WASM
│
├── Data.rsdk             ← Sonic 1 Forever v1.5.1 game data (38 MB — use Git LFS)
├── Forever.ini           ← Engine config
├── favicon.ico
├── manifest.webmanifest  ← PWA manifest
├── pwabuilder-sw.js      ← Service worker
├── _headers              ← Netlify / Cloudflare COOP/COEP headers
├── .gitattributes        ← Git LFS tracking for large files
│
├── Mods/
│   ├── modconfig.ini     ← Enable/disable mods here
│   └── Sonic 1 Forever/  ← Bundled mod (scripts & configs)
│
└── icon/                 ← PWA icons (svg, png)
```

---

## ⚡ Quick Start (Local)

```bash
# 1. Clone the repo
git clone https://github.com/YOUR_USERNAME/sonic1-forever.git
cd sonic1-forever

# 2. Download the WASM engine files from grubbyplaya/Sonic-1-WASM
#    and place index.js + index.wasm in this folder

# 3. Serve locally (file:// is blocked by browser security)
python3 -m http.server 8000
# Then open http://localhost:8000/web.html
```

---

## 🚀 GitHub Pages Deployment

### Option A — Git LFS (recommended)

GitHub free tier includes 1 GB LFS storage and 1 GB/month bandwidth.

```bash
# Install Git LFS (one time)
git lfs install

# Track large files (already set in .gitattributes)
git lfs track "*.rsdk" "*.wasm" "*.data"

# Commit everything
git add .
git commit -m "Initial deploy"
git push origin main
```

Then go to **Settings → Pages → Source: main branch, / (root)**.

### Option B — Compressed rsdk (smaller repo)

```bash
# Compress Data.rsdk to ~24 MB (requires zstd)
zstd -19 Data.rsdk -o Data.rsdk.zst

# Replace in repo — web.html will decompress via DecompressionStream API
```

### Required Headers for SharedArrayBuffer

Some features need these HTTP headers. Add a `_headers` file (Netlify/Cloudflare) or a GitHub Actions workflow:

```
/*
  Cross-Origin-Opener-Policy: same-origin
  Cross-Origin-Embedder-Policy: require-corp
```

For GitHub Pages, use the [coi-serviceworker](https://github.com/gzuidhof/coi-serviceworker) trick — already handled in `pwabuilder-sw.js`.

---

## 🎮 Controls

### Mobile — Xbox-Style Touch Controller
On-screen controller appears automatically on touch devices, styled like an Xbox gamepad:

| Button | Action |
|--------|--------|
| D-Pad ← → | Move |
| D-Pad ↑ | Look up |
| D-Pad ↓ | Crouch / Roll |
| **A** (green, bottom) | Jump |
| **X** (blue, left) | Spin Dash |
| **B** (red, right) | Spin Dash (alt) |
| **Y** (yellow, top) | — |
| **START** | Pause |
| **SELECT** | Back / Pause |
| **⊞ Guide** | Toggle Fullscreen |
| LT / RT / LB / RB | Mapped to Q/E/R/T |

### Keyboard
`← → ↑ ↓` Move &nbsp;·&nbsp; `Z` Jump &nbsp;·&nbsp; `X` Spin Dash &nbsp;·&nbsp; `Enter` Start &nbsp;·&nbsp; `Esc` Back &nbsp;·&nbsp; `F` Fullscreen

### Gamepad (Xbox / USB / Bluetooth)
Detected automatically via the Web Gamepad API. Left stick and all face buttons + D-pad are mapped.

---

## 🗜️ Adding Mods

1. Download an **RSDKv4-compatible** Sonic 1 mod (e.g. from [GameBanana](https://gamebanana.com/games/8688)).
2. **Browser storage** (easiest): Go to `directory.html` → Import Mods section → drop the mod zip → click **Apply & Save**.
3. **Server-side**: Drop the mod folder into `Mods/`, then edit `Mods/modconfig.ini`:
   ```ini
   [mods]
   Sonic 1 Forever=true
   Your Mod Name=true
   ```

---

## 🔧 File Size Guide for GitHub

| File | Size | Method |
|------|------|--------|
| `Data.rsdk` | 38 MB | **Git LFS** (required) |
| `index.wasm` | ~3 MB | Git LFS or regular commit |
| `index.js` | ~1 MB | Regular commit |
| `web.html` | ~50 KB | Regular commit |
| `Mods/Sonic 1 Forever/` | ~2 MB scripts | Regular commit |
| `SonLVLObjDefs/` | ~5 MB | **Exclude** — not needed to play |
| `SDL2.dll` | 2 MB | **Exclude** — Windows only |

**Tip:** Add `SonLVLObjDefs/` and `SDL2.dll` / `glew32.dll` to `.gitignore` to keep the repo under GitHub's 100 MB file limit.

---

## 📜 Credits

| | |
|---|---|
| **Original game** | Sonic the Hedgehog (2013) — SEGA |
| **Retro Engine** | Christian Whitehead |
| **Sonic 1 Forever** | MainMemory & the S1F team |
| **RSDKv4 Decompilation** | [RubberDuckyCooly](https://github.com/Rubberduckycooly) |
| **WASM Port** | [MattConn / grubbyplaya](https://github.com/grubbyplaya/Sonic-1-WASM) |
