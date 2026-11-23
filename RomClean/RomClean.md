# RomClean

**English** | [한국어](RomClean-ko.md)

A desktop app for managing MAME ROMs and building romsets (Linux · macOS · Windows).

**[⬇ Download the latest release](https://github.com/airplanez/AppsRepo/releases/tag/RomClean)**

> RomClean does not provide any ROMs. It only manages files you already own.

## Contents

- [Features](#features)
- [Download & install](#download--install)
- [Quick start](#quick-start)
- [Run games from RomClean](#run-games-from-romclean)
- [Where is the MAME executable?](#where-is-the-mame-executable)
- [MAME Software Lists](#mame-software-lists)
- [Genre files (catver.ini · mature.ini)](#genre-files-catverini--matureini)
- [Where RomClean keeps its data](#where-romclean-keeps-its-data)
- [Reset RomClean](#reset-romclean)
- [Uninstall](#uninstall)
- [Version history](#version-history)

## Features

- Scans your ROM folders (zip · 7z · CHD · samples) **without changing them** and records what you have.
- Register a MAME Dat (`mame -listxml`, or pick the MAME executable) to see which machines are complete, partial, or missing.
- Exports romsets in `split`, `merged`, or `non-merged` format as zip or 7z — always TorrentZip / Torrent7z, and only the files that changed since the last export. CHDs are exported as hard links when possible, so they take no extra space.
- Runs exported games in MAME straight from the list.
- MAME Software Lists (consoles and computers) — including ROMs made for other emulators, such as `.nes` files.
- Filters by genre (catver.ini · mature.ini), year, manufacturer, screen, players, and "Arcade games only".
- Cleanup tools: **Remove duplicates** (deletes extra copies) and **Move unmatched** (moves files no target set needs — never deletes).
- English and Korean, Light and Dark themes.
- RomClean does not collect or send any data.

## Download & install

Download the package for your platform from the **[RomClean release page](https://github.com/airplanez/AppsRepo/releases/tag/RomClean)**.

No installer. Extract and run. Replace `0.5.3` with the version you downloaded.

### Linux (x64) — `romclean_v0.5.3_linux.tar.gz`

```bash
tar -xzf romclean_v0.5.3_linux.tar.gz
./romclean_v0.5.3_linux/romclean
```

- Requires the GTK 3 runtime (installed by default on most desktop distributions).
- To add RomClean to the app list with its icon (optional):
  `./romclean_v0.5.3_linux/install-desktop-entry.sh` (remove with `--uninstall`).
  Run it again if you move the folder.

### macOS (12 or later, Apple Silicon · Intel) — `romclean_v0.5.3_macos.zip`

1. Double-click the zip to extract `romclean.app`.
2. Move it to `Applications` (optional) and open it.

The app is signed and notarized by Apple.

### Windows (x64) — `romclean_v0.5.3_windows.zip`

1. Right-click the zip → **Extract All**.
2. Open the `romclean_v0.5.3_windows` folder and run `romclean.exe`.

- Keep all files in the folder together — `romclean.exe` does not run on its own.
- The app is not code-signed. If Windows shows "Windows protected your PC", click **More info → Run anyway**.

## Quick start

1. **Source sets** → **Add directory** → pick your ROM folder → **Scan**.
2. **Target sets** → **Add target set** → pick a MAME Dat file or the MAME executable.
3. Open the target set to see each machine's status, then **Export** to a new folder.
4. Click the ▶ status of a complete machine to run it in MAME (see below).

## Run games from RomClean

After you export a target set and RomClean knows your MAME executable, you can start games from RomClean.

1. **Set the MAME executable** — automatic if you created the target set from the MAME executable. Otherwise use the target set menu (⋮) → **Choose MAME…**, or pick it the first time you run a game. RomClean checks it with `mame -version`.
2. **Export** the target set. Complete machines that were actually exported get a clickable ▶ status chip. The machine details page also has **Run in MAME**.
3. Click it and confirm — RomClean starts the game in MAME. For Software List items, choose the system (for example `nes`) in the dialog.

- Games run from the **last export folder**, not from your source folders.
- If MAME stops with an error (for example a missing file), RomClean shows MAME's full error output.
- The target set card shows the last export folder and the MAME executable. **Open export folder** in the menu opens it in your file manager.

## Where is the MAME executable?

| OS | How MAME was installed | MAME executable | Software List `hash` folder |
| --- | --- | --- | --- |
| Linux (Debian · Ubuntu) | `sudo apt install mame` | `/usr/games/mame` | `/usr/share/games/mame/hash` (package `mame-data`) |
| Linux (other distributions) | distribution package | usually `/usr/bin/mame` | usually `/usr/share/mame/hash` |
| Linux | `sudo snap install mame` | `/snap/bin/mame` | none in the package (see note) |
| macOS (Apple Silicon) | `brew install mame` | `/opt/homebrew/bin/mame` | `/opt/homebrew/share/mame/hash` |
| macOS (Intel) | `brew install mame` | `/usr/local/bin/mame` | `/usr/local/share/mame/hash` |
| Windows | official package from [mamedev.org](https://www.mamedev.org/release.html), extracted to a folder you choose | `<that folder>\mame.exe` (for example `C:\mame\mame.exe`) | `<that folder>\hash` |

- If you are not sure, run `command -v mame` (Linux · macOS) in a terminal.
- RomClean looks for the `hash` folder next to the MAME executable, then in MAME's `hashpath` setting (`mame -showconfig`), then in the locations above. If none is found, choose it yourself.
- **Snap MAME**: the snap package has no `hash` folder, and a snap can only read folders it is allowed to (usually your home folder). Software Lists may not run with it. Use the apt package for Software Lists, and keep export folders inside your home folder.

## MAME Software Lists

**What they are.** Besides arcade machines, MAME emulates consoles and computers (NES, Super NES, Mega Drive, PC Engine…). Their games are described by **Software Lists** — XML files in MAME's `hash` folder, one per system (`hash/nes.xml`, `hash/snes.xml`, …). Each entry names a cartridge or disk and the exact ROM dumps it needs (name, size, CRC, SHA-1), much like a Dat file for arcade games. MAME expects them as `roms/<list>/<software>.zip` and runs them as `mame nes smb` (system + software).

**How they differ from dedicated emulators.** A dedicated emulator (for example Mesen or Nestopia for NES) loads one file such as `Super Mario Bros.nes`. That file starts with a small **header** (16 bytes for iNES) that tells the emulator how the cartridge is wired. MAME does not use headers: it takes the board information from the Software List and wants the **raw chip data**, often split by chip — a NES cartridge becomes separate PRG and CHR ROMs inside `nes/smb.zip`. So the same game is stored differently, and a `.nes` file does not match MAME as it is.

**What RomClean does.**

- Import the lists you want: target set menu (⋮) → **Software Lists…** (or **Include Software Lists** when you add a target set). Then switch between **Machines | Software Lists** on the target set page.
- When it scans headered files — `.nes` (NES), `.fds` (Famicom Disk System), `.a78` (Atari 7800), `.lnx` (Lynx), `.smc` · `.sfc` · `.swc` · `.fig` (Super NES), `.pce` (PC Engine) — RomClean also records the part **without the header**. Those files then match the Software List, and **Export** (with **Include Software Lists**) writes them in MAME's layout: one `.nes` file becomes `nes/<software>.zip` with its PRG and CHR ROMs. Your original files are not changed.
- Not supported: cartridges that must be split into several chips beyond PRG / CHR (for example ColecoVision, some Super NES and multi-PRG NES carts), and byte-swapped formats (`.smd` for Mega Drive, `.v64` for N64). Those files stay unmatched.
- Target sets created with versions before Software List support cannot add Software Lists — create the target set again.

## Genre files (catver.ini · mature.ini)

Genre filters, the Genre column, "Exclude mature" and "Arcade games only" need these files. They are not part of MAME or RomClean — download them yourself.

1. Download the latest package from **[Progetto-SNAPS CatVer](https://www.progettosnaps.net/catver/)** (for example `pS_CatVer_289.zip` for MAME 0.289). Pick the version closest to your MAME.
2. Extract it. `catver.ini` is in the top folder, `mature.ini` is in `UI_files/`.
3. In RomClean: target set menu (⋮) → **Genre files…** → **Choose…** for each file.

- RomClean copies the contents into its database, so you can delete or move the files afterwards.
- A clone that is not in the file uses its parent's genre.
- Machine attributes (year, manufacturer, screen, players) come from the Dat. For target sets made before v0.5.3, use target set menu → **Reload Dat…** to fill them in.

## Where RomClean keeps its data

| OS | Database and data folder | Settings (language · theme) |
| --- | --- | --- |
| Linux | `~/.local/share/net.airplanez.flutter.romclean/` | `shared_preferences.json` in the same folder |
| macOS | `~/Library/Application Support/net.airplanez.flutter.romclean/` | `~/Library/Preferences/net.airplanez.flutter.romclean.plist` |
| Windows | `%APPDATA%\net.airplanez.flutter\romclean\` | `shared_preferences.json` in the same folder |

- `romclean2.sqlite` — the database: source folders and scan results, target sets, filters, export settings, MAME executable, genre data.
- `romclean.sqlite` — the database of v0.5.0. Later versions do not use it; you can delete it.
- Linux only, if you ran `install-desktop-entry.sh`: `~/.local/share/applications/net.airplanez.flutter.romclean.desktop` and `~/.local/share/icons/hicolor/256x256/apps/net.airplanez.flutter.romclean.png`.
- On Windows, paste `%APPDATA%\net.airplanez.flutter` into the File Explorer address bar to open the folder.

## Reset RomClean

**Quit RomClean first.** Your ROM folders, exported romsets and moved files are never touched by a reset.

- **Start over with an empty database** — delete `romclean2.sqlite` from the data folder above. You will need to add source folders, scan, and add target sets again. Language and theme stay.
- **Reset settings** (language, theme, filter panel) — delete the settings file above. On macOS run this instead of deleting the file:

  ```bash
  defaults delete net.airplanez.flutter.romclean
  ```

- **Reset everything** — delete both.

  ```bash
  # Linux
  rm -rf ~/.local/share/net.airplanez.flutter.romclean
  # macOS
  rm -rf ~/Library/Application\ Support/net.airplanez.flutter.romclean
  defaults delete net.airplanez.flutter.romclean
  ```

  Windows: delete the folder `%APPDATA%\net.airplanez.flutter\romclean`.

## Uninstall

Quit RomClean, then:

- **Linux** — if you added the app list entry, run `./romclean_v<version>_linux/install-desktop-entry.sh --uninstall` first. Delete the `romclean_v<version>_linux` folder and `~/.local/share/net.airplanez.flutter.romclean`.
- **macOS** — move `romclean.app` to the Trash, delete `~/Library/Application Support/net.airplanez.flutter.romclean`, and run `defaults delete net.airplanez.flutter.romclean`.
- **Windows** — delete the `romclean_v<version>_windows` folder and `%APPDATA%\net.airplanez.flutter\romclean` (and `%APPDATA%\net.airplanez.flutter` if it is empty).

RomClean writes nothing else on your system. Your ROMs, exported romsets and moved unmatched files stay where they are.

## Version history

### v0.5.3
- MAME Software List support (import, completeness check, export, run), recognizes headered ROMs (`.nes`, `.smc`, etc.)
- Improved machine filters (basic row + advanced filters), genre filter (`catver.ini`, `mature.ini`), year / manufacturer / screen / players filters
- Move files that match no target set to another folder (nothing is deleted), shows duplicate and unmatched file sizes
- CHDs exported as hard links (saves disk space), confirmation before removing a directory, clear buttons in text fields

### v0.5.2
- 7z read and write support, exports always use TorrentZip / Torrent7z format
- Run exported machines in MAME straight from the list, open the export folder
- Incremental scan and export, export folder cleanup, source change detection
- "System" language by default, clone status now matches MAME, starts with a new database (includes v0.5.1 changes)

### v0.5.0
- First public release (Linux, macOS, Windows)
- Source set scan and duplicate removal, target sets from a Dat or MAME executable with completeness check
- Machine list, details and filters, split / merged / non-merged romset export
- Light / Dark theme, English and Korean, About tab
