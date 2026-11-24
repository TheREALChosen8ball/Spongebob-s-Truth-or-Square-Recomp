# SpongeBob's Truth or Square - Windows Recompilation Setup

Hey there! This package lets you play **SpongeBob's Truth or Square** (the Xbox 360 version) on Windows. It's a recompilation — meaning the game's original code has been translated to run natively on your PC, not emulated. That means way better performance, higher resolutions, and no emulation overhead.

---

## What's Different From the Original

- **1080p resolution** (1920×1080) instead of 720p
- **Unlimited framerate** — the game runs as fast as your hardware can push it (no 60/120 FPS cap)
- **2× internal resolution scaling** — the game renders at ~1440p internally and downscales to 1080p for a cleaner image
- **16× anisotropic filtering** — textures stay sharp at angles
- **Native 2× MSAA** — smoother edges without the performance hit of old-school MSAA
- **Shader caching** — shaders compile once, then load instantly on future runs (no more stutter!)
- **Cutscenes auto-skipped** — Bink videos currently stall the game, so they're temporarily disabled while playing

---

## ⚠️ Important Disclaimers (Please Read)

**This is not an official release.** This is a fan-made recompilation project using the [ReXGlue](https://github.com/rexglue/rexglue-sdk) runtime. It's provided as-is, for personal use only, with your own legally obtained game files.

**You need your own game dump.** This package does **not** include the game. You'll need an extracted Xbox 360 disc image with `DEFAULT.XEX` at the root. If you don't know how to get that, this project probably isn't for you — and that's okay!

**Cutscenes don't work right now.** The Bink video playback stalls the game engine. The launcher automatically renames `.bik` files to skip them while the game runs, and restores them when you quit. If the game crashes, just run the launcher again — it'll clean up.

**DirectX 12 only.** The Vulkan renderer was removed in this build because it had some graphics issues. The DirectX 12 path is solid.

**Antivirus might complain.** The build outputs an unsigned `.exe`. Windows Defender or other AV might flag it. You'll need to allow it.

**Save files.** Your saves go wherever the game expects them (usually in your user profile under `Saved Games` or similar). They're compatible with the original Xbox 360 save format if you ever move them back.

---

## Requirements

- **Windows 10 or 11 (64-bit)**
- **Visual Studio 2022 or later** with **Desktop development with C++** workload installed
- **Clang/LLVM tools component** in Visual Studio (the installer calls it "C++ Clang tools" or similar)
- **Your extracted game files** — a folder containing `DEFAULT.XEX` at the top level
- A GPU with **DirectX 12 support** (pretty much anything from the last 8+ years)

The ReXGlue 0.11.0 SDK, CMake, and Ninja are bundled — you don't need to install them separately.

---

## How to Build & Play

### 1. Pick a Good Folder
Extract this ZIP somewhere **short and simple**, like:
```
C:\Games\SpongeBobRecomp
```
Avoid paths with spaces, special characters, or deep nesting — the compiler hates those.

### 2. Run the Setup
Double-click **`setup.cmd`**. A PowerShell window will open.

- If you already put your extracted game files in the `extract` folder next to `setup.cmd`, it'll detect them automatically.
- Otherwise, it'll ask you to type the full path to your extracted game folder (the one with `DEFAULT.XEX` in it).

### 3. Wait for the Build
The first run takes a few minutes — it's translating the game's PowerPC code to x64 and compiling everything. Subsequent runs are way faster because of caching.

You'll see a bunch of compiler output. That's normal. Grab a coffee.

### 4. Play!
When it's done, you'll see a new shortcut on your desktop (or wherever you extracted the ZIP):
> **SpongeBob's Truth or Square RECOMPILED.lnk**

Double-click that to play. Or run `SpongeBobTruthOrSquare\launch_game.cmd` if you prefer.

---

## Switching Game Dumps

Want to use a different dump (like a different region or version)? Just run `setup.cmd` again and point it at the new folder. It'll update the config and rebuild.

---

## Folder Structure (If You're Curious)

```
SpongeBobTruthOrSquare/       # The actual project — source, build scripts, launchers
tools/
  ├─ llvm-msvc/               # LLVM linker (lld-link) for Windows
  └─ rexglue-sdk-binary/      # ReXGlue runtime DLLs (prebuilt)
licenses/                     # All the legal stuff (ReXGlue + dependencies)
setup.cmd / setup.ps1         # The build script (cmd launches ps1)
README.md                     # You're reading it
```

The ZIP **does not** include:
- The game image or extracted files
- Generated C++ code (created during build)
- Shader caches or build artifacts

---

## Extracting Your Xbox 360 Disc

If you have a physical disc or ISO, you'll need to extract it first. A tool called **Xbox 360 ISO Extract** works well:
🔗 https://xbox-360-iso-extract.en.lo4d.com/windows

Point it at your ISO, extract everything, then point `setup.cmd` at the folder that contains `DEFAULT.XEX`.

---

## Credits

This project exists because of **[ReXGlue](https://github.com/rexglue/rexglue-sdk)** — an incredible Xbox 360 recompilation runtime by Tom Clay and contributors. All the heavy lifting is theirs.

Bundled dependencies keep their own licenses (see the `licenses/` folder).

---

## AI Assistance Note

Claude (Anthropic) helped with the Windows setup workflow, build configuration, documentation, and some code tweaks. The recompilation itself is generated from your local game dump — no game code or assets were provided or generated by AI.

---

**Enjoy Bikini Bottom in 1080p!** 🧽🍍
