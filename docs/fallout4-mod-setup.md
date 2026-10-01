# Fallout 4 Mod Setup: Settlement Building & Ultrawide

As of 2026-10-01. Target: a stable, modern Fallout 4 with extended settlement building
(Sim Settlements 2), a correct 21:9 HUD and better graphics – installed in six phases,
each only after the previous one has been tested.

**Starting point:** Steam version with all six DLCs, Anniversary update (1.11.x),
monitor 3440×1440.

**Ground rules:**

- Install everything through Mod Organizer 2, never directly into the game folder
  (exceptions: F4SE and ENB/ReShade).
- For every mod, check on Nexus that the file matches the current game version
  ("NG"/"Anniversary"). F4SE plugins (.dll) for the old 1.10.163 version do not work.
- After each phase, start the game and test briefly – a problem is found immediately
  instead of in a pile of 50 mods.
- Start a new game for SS2.

## Phase 0: Preparation

1. **Limit automatic updates:** Steam → Library → right-click Fallout 4 → Properties →
   Updates → "Only update this game when I launch it". A new Bethesda update breaks
   F4SE and all .dll mods until the modders catch up.
2. **Game folder:** if Steam is under `C:\Program Files (x86)\`, Windows may block
   writes. Better create a separate Steam library such as `D:\SteamLibrary\` and move
   Fallout 4 there (Properties → Installed Files → Move install folder).
3. **Backup:** copy the whole folder `Documents\My Games\Fallout4\` (saves and INIs).
4. **Run the launcher once:** start Fallout 4 normally via Steam, in the launcher
   options set 3440×1440 and **Weapon Debris to "Off"** (prevents crashes on NVIDIA
   cards). Go to the main menu once, then quit. This regenerates the INI files.
5. **Clean up old mods/Creations:** disable anything installed via the in-game
   Creations menu. From now on, everything goes through MO2.

## Phase 1: Tools

**Find your game version:** in the game folder, right-click `Fallout4.exe` →
Properties → Details → Product version. As of July 2026 this is **1.11.221** (update
of 27 May 2026); before that 1.11.191. This number decides which file you download for
every F4SE mod.

| # | Tool | Purpose | Installation |
| --- | --- | --- | --- |
| 1 | [Mod Organizer 2](https://www.nexusmods.com/skyrimspecialedition/mods/6194) | Mod manager, keeps the game folder clean, profiles | Portable instance e.g. `D:\Modding\MO2-FO4\`, not inside the game folder |
| 2 | [F4SE](https://f4se.silverlock.org) | Script extender, base for most larger mods | Version matching the game (July 2026: 0.7.8 for 1.11.221); copy `f4se_loader.exe`, `f4se_steam_loader.dll` and `f4se_1_11_xxx.dll` into the game folder, `Data\Scripts` as a mod via MO2 |
| 3 | [LOOT](https://loot.github.io) | Sorts the plugin load order | Add as executable in MO2 |
| 4 | Collective Modding Toolkit | Checks the installation, wrong files, archive limits | Add to MO2, run after each phase |
| 5 | BethINI Pie (optional) | Comfortable INI settings (resolution, shadows, FOV) | Always point it at the MO2 profile |
| 6 | FO4Edit / xEdit (optional) | Inspect conflicts, clean plugins | Only when needed |

**Set up MO2:**

1. Start MO2 → "Create a portable instance" → choose Fallout 4.
2. Settings → Nexus → "Connect to Nexus", so "Mod Manager Download" on Nexus loads
   straight into MO2.
3. "F4SE" must appear in the executable dropdown at the top right. From now on start
   the game **only** through it.
4. Test: start via F4SE, open the console (key below Esc), type `getf4seversion`. If a
   version number appears, F4SE is running.

## Phase 2: Foundation & stability

These mods come first: they prevent crashes, fix engine bugs and improve performance.
Important: **Buffout 4 no longer works on the Anniversary update** – its successor is
Addictol.

Install in this order via MO2:

| # | Mod | Purpose | Notes |
| --- | --- | --- | --- |
| 1 | Address Library for F4SE Plugins | Required by almost all .dll mods | Pick the AE file for your game version |
| 2 | [Addictol](https://github.com/Dear-Modding-FO4/Addictol) | Crash fixes + crash logs, successor of Buffout 4 / Buffout 4 AE | Crash logs go to `Documents\My Games\Fallout4\F4SE\` |
| 3 | High FPS Physics Fix | Physics, lip sync and loading times above 60 FPS | Set the FPS limit in its INI to your monitor refresh rate |
| 4 | Mod Configuration Menu (MCM) | Settings menu for mods in the pause menu | Many SS2 options use it |
| 5 | MCM Booster AE | Faster, more stable MCM | Optional, recommended |
| 6 | Unofficial Fallout 4 Patch (UFO4P) | Thousands of fixes for quests, objects, settlers | Requires all DLCs |
| 7 | Community Fixes Merged | Collection of small fixes in one plugin | Saves plugin slots |
| 8 | [Previsibines Repair Pack (PRP)](https://www.nexusmods.com/fallout4/mods/46403) | Repairs precombines/previs: noticeably more FPS, especially in Boston | Loads late; LOOT sorts it. Avoid mods that break precombines |

**Test after phase 2:** start via F4SE, new game until just outside the vault, save,
load. Then run the Collective Modding Toolkit.

Tip: for a ready-made, tested foundation, follow "The Midnight Ride" guide or the
[STEP Fallout 4 guide](https://stepmodifications.org/wiki/Fallout4:1.1/changelog)
instead, then add phases 3–5.

## Phase 3: Ultrawide 3440×1440

[Ultra Wide Interface (21x9)](https://www.nexusmods.com/fallout4/mods/65677) by Aigni
fixes the whole HUD and all menus for 21:9 and is tested at 3440×1440. Its F4SE plugin
"Aspect Ratio Fix.dll" removes the 16:9 lock introduced by the Anniversary update.

1. **Set the resolution:** MO2 → Tools → INI Editor → `Fallout4Prefs.ini` → under
   `[Display]` set `iSize W=3440` and `iSize H=1440`. MO2 keeps its own INI copies per
   profile, so edit them there, not in the Documents folder.
2. **Remove old ultrawide solutions:** stop using Flawless Widescreen, disable earlier
   ultrawide mods.
3. **Install HUDFramework first** (needed for SS2 anyway, see phase 4) so the installer
   offers the matching patch.
4. **Install the mod** with "Mod Manager Download". In the FOMOD installer:
    - Display: **Wide** (needs F4SE, uses the full width) or Centered (HUD in the middle).
    - UI size: Default or Smaller UI – at 3440×1440 Smaller is often more comfortable.
    - Only tick patches for mods you **actually have installed**, otherwise it may crash.
5. **Order:** in MO2 (left pane) put it **at the very bottom below all other UI mods**
   so the 21:9 files win. When adding UI mods later, run the installer again.
6. **Do not touch:** the mod sets `fDefaultFOV=80` in its INI. Set your own FOV via
   `fDefaultWorldFOV` and `fDefault1stPersonFOV`, otherwise scopes and shadows no
   longer fit.

**Test:** in game, check the Pip-Boy, the workshop menu and power armor. On problems,
see the log at `Documents\My Games\Fallout4\F4SE\Aspect Ratio Fix.log`.

## Phase 4: Settlement building

Core is Sim Settlements 2 with its two required frameworks; around it come build tools,
build parts and extra settlements.

**Core (exactly this order):**

| # | Mod | Purpose | Notes |
| --- | --- | --- | --- |
| 1 | Workshop Framework | Required for SS2 | Current version with F4SE part for your game version |
| 2 | HUDFramework | New SS2 HUD elements | Already installed in phase 3 |
| 3 | [Sim Settlements 2 – All Chapters Pack](https://wiki.simsettlements2.com/getting-started/requirements) | Plots, City Plans, three-chapter story | Includes SS2 Extended. City Plans included |
| 4 | Place Everywhere | Free placement without collision checks | F4SE plugin for your game version. Recommended by the SS2 team |
| 5 | Settlement Menu Manager | Stops build mods overwriting each other's menus | Install before any build-part mods |

**Settlement fixes:**

- Thaylar's Settlement Lighting Fixes – corrects lighting in settlements
- Settlement Dead Zone Fixes – makes unbuildable areas buildable

**Build parts (to taste):**

- Homemaker – hundreds of extra objects
- Snappy HouseKit – modular parts that snap cleanly
- OCDecorator – decorations stay where you put them
- Community City Plan packs (e.g. "City Plan Contest") – extra ready-made city plans for SS2

**Extra settlements (SS2 compatible):**

- [Fort Strong Settlement](https://www.nexusmods.com/fallout4/mods/76211) and
  [Bridgeport Settlement](https://www.nexusmods.com/fallout4/mods/76463) by Yagisan –
  choose the PRP-compatible version of each

**Deliberately leave out:**

- Sim Settlements 1 / Conqueror – cannot be combined with SS2
- Mods that replace the workshop script or skip the main quest
- Scrap Everything – breaks precombines and defeats PRP
- All Settlements Extended – not in settlements SS2 builds via City Plan
- Transfer Settlements – only for blueprints without SS2 plots

**Start:** begin a new game. SS2 starts after leaving the vault; the Chapter 1 story
begins shortly after on its own. Settings in MCM under "Sim Settlements 2".

## Phase 5: Graphics

Performance helpers first, then textures, then lighting and weather, ENB or ReShade
last. At 3440×1440, 2K textures are the best compromise.

| # | Area | Mod | Notes |
| --- | --- | --- | --- |
| 1 | Performance | Upscaling (DLSS / FSR / XeSS) | More FPS at 3440×1440; F4SE plugin |
| 2 | Performance | Shadow Boost FO4 | Adjusts shadow distance dynamically to an FPS target |
| 3 | Textures | Fallout 4 HD Overhaul 2k **or** PhyOp | Not both; HD Overhaul is broader, PhyOp lighter |
| 4 | Textures | Vivid Fallout – All in One (2K) | Rocks, ground, roads; load after HD Overhaul |
| 5 | Textures | Landscape Textures Overhaul | Ground and terrain |
| 6 | Textures | Enhanced Vanilla Water | Better water |
| 7 | Textures | Ultimate Window Overhaul Redone, Gloomy Glass | Windows and glass |
| 8 | Lighting | Ultra Interior Lighting | Realistic interior lighting, PRP-friendly |
| 9 | Weather | Vivid Weathers **or** True Storms | Only one of them |
| 10 | Night | Darker Nights | Truly dark nights; brightness adjustable in MCM |
| 11 | Post-processing | ENB (e.g. PRC ENB) **or** ReShade (e.g. NAC X) | Last, not via MO2: files go directly into the game folder |

**Notes:**

- **ENB vs. ReShade:** ENB looks best but costs noticeable FPS and does not work with
  every upscaler. ReShade is lighter. Play without either first and see whether you miss
  it.
- **Archive limit:** many texture mods ship .ba2 archives. The Collective Modding
  Toolkit warns when you exceed the limit.
- **After each larger texture mod:** check FPS briefly in Boston (Diamond City /
  Corvega).

## Phase 6: Load order, test, game start

MO2 has two orders: on the left the **install order** (who overwrites files), on the
right the **plugin load order** (.esp/.esm/.esl). Arrange the left side by hand
following the phases of this guide; LOOT sorts the right side.

**Left side (roughly top to bottom):** frameworks/F4SE plugins → fixes (UFO4P,
Community Fixes) → textures → lighting/weather → settlement building → PRP →
HUDFramework → Ultra Wide Interface at the very bottom.

**Final checklist:**

- [ ] Run LOOT and sort
- [ ] Collective Modding Toolkit: no red warnings
- [ ] Start via F4SE, console: `getf4seversion` shows a version
- [ ] New game, play to Sanctuary, open the workshop: HUD and menus fill the width correctly
- [ ] SS2 message appears, MCM shows "Sim Settlements 2"
- [ ] Travel to Diamond City once: FPS fine, no crash
- [ ] Saving and loading work
- [ ] Copy the MO2 profile ("Profiles" → Copy) as a backup of the working state

**Adding mods later:** add only one mod (or one package that belongs together) at a
time, run LOOT, test. Never remove mods with scripts (.pex) in the middle of a
playthrough.

## Troubleshooting

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Game does not start / closes immediately | F4SE plugin does not match the game version | Check `Documents\My Games\Fallout4\F4SE\f4se.log`: it lists which .dll failed to load. Get the matching version or disable it |
| Nothing works after a Steam update | Bethesda update, F4SE outdated | Wait for F4SE and Address Library updates, or roll the game back to the previous version with a downgrader |
| Crash in game | Mod conflict | Read the Addictol crash log in the F4SE folder; the Collective Modding community (Discord) helps reading them |
| HUD stretched or cut off | Ultra Wide Interface overwritten or game started without F4SE | Move it to the bottom in MO2, rerun the installer, start via F4SE |
| Settlements very slow / FPS drop | Broken precombines, too many objects | No Scrap Everything mods; use PRP-compatible settlement mods |
| SS2 quest stuck | Quest conflict or skipped quest | Check [SS2 Known Issues](https://wiki.simsettlements2.com/getting-started/known-issues) |

## Sources

- [STEP Fallout 4 guide – changelog for the Anniversary update](https://stepmodifications.org/wiki/Fallout4:1.1/changelog)
- [Ultra Wide Interface (21x9) – Nexus](https://www.nexusmods.com/fallout4/mods/65677)
- [Sim Settlements 2 wiki – requirements](https://wiki.simsettlements2.com/getting-started/requirements)
- [Sim Settlements 2 wiki – known issues](https://wiki.simsettlements2.com/getting-started/known-issues)
- [Buffout 4 AE → Addictol – Nexus](https://www.nexusmods.com/fallout4/mods/99911)
- [SUP F4SE AE – note on game version 1.11.221 / F4SE 0.7.8](https://www.nexusmods.com/fallout4/mods/107607)
