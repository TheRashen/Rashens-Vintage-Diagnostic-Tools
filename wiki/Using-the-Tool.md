Using the Tool
==============


Diagnostics tab
---------------

The main scan. Reads your mods folder, cross-references everything, and tells you what's wrong.

What it checks:
- Missing dependencies (mod A needs mod B, mod B isn't installed)
- Version mismatches (mod A needs mod B ≥ 1.5, you have 1.3)
- Duplicate mods (two versions of the same mod in the folder)
- Conflicting patches (two mods patch the same thing differently)
- Broken recipes (item codes that don't exist, missing shape refs, etc.)
- Entity spawns (spawn rate sanity checks, missing entity codes)
- Deep scan: reads every JSON in every mod and flags syntax errors,
  missing asset references, and known VS pitfalls

Results are color-coded. Red = problem that will probably break things.
Yellow = warning, might be fine. Green = all clear.

Ctrl+F to search the output. The sidebar on the right lets you jump
between sections directly.

Edit menu has Export to CSV if you want to sort or filter the results
in a spreadsheet. (W.I.P.) 
{If you can use this function to collab a new list (googledocs/community accessible) of compatible mods that'd be awesome}


Startup Mem Watcher tab
-----------------------

Attach to a running VS process and watch RAM usage on a graph.

1. Start VS (server or client).
2. Switch to the Startup Mem Watcher tab.
3. Click "Find VS Process" - the tool finds VintagestoryServer.exe or
   Vintagestory.exe automatically.
4. The graph starts filling. Cyan line = working set, purple dashed = private.
5. Click "Mark Event" at any time to drop a named label on the graph.
   Useful for things like "entered cave", "broke leaf pile", "bought from trader".
6. Detach whenever - graph freezes, samples stay visible so you can look at it.
7. Export CSV dumps all samples as a spreadsheet if you want to crunch numbers.
-Export is a WIP, in the future I'm aiming for it to actually dump tickrates for you classified by mod.

The graph shows up to the last hour of data (1800 samples at 2s per sample).
When the process ends, the tool detects it and detaches automatically.


Modded Json Search tab
----------------------

Find which mods touch a specific item or block.

Type a code (e.g. "gear-temporal" or "game:gear-temporal") and hit Search.
The tool scans every mod zip for any JSON file that references that code
and shows you where.

Useful for finding:
- Which mod drops a specific item
- Which mods modify a particular block's behavior
- Where an item code is defined

"All" mode lists everything without a search filter, which is slow on big
packs but useful for a full inventory of what's in your mod folder.


Experimental Patcher tab
-------------------------

A collection of utility tools for fixing and inspecting mods.

  Build Patch Mod - generates a compatibility bridge mod from your scan
  results. Drop it in your mods folder to resolve asset conflicts, missing
  dependency stubs, and duplicate ID conflicts. Run a scan first so the
  tool has results to work from.

  Repair JSON Errors - finds and fixes malformed modinfo.json files inside
  mod zips. Backs them up before changing anything.

  Fix Dep Versions - bulk-updates the game dependency version in a folder
  of mod zips. Useful when VS releases a new minor version and half your
  mods complain about the version string.

  Strip Non-Matching Languages - removes lang files from mod zips that
  don't match your chosen language code. Useful for reducing mod zip size
  or cleaning up mods that ship many language files you don't need. 
  -(This usually doesn't cause issues with any mods but some may be setup in a way that requires all their localizations)

  DLL Framework Check - reports which DLLs in your mods folder are compiled
  against older .NET runtimes. Useful for spotting mods built for older VS
  versions that may behave unexpectedly on VS 1.22+.


Recipe Diff tab
---------------

Shows which mods are patching or shadowing vanilla recipes.

Runs a scan of all mod zips and cross-references them against the vanilla
recipe list. Highlights mods that override or add-to the same recipe slot.
Useful for tracking down broken crafting when you have a lot of mods that
touch the same materials.


Custom Mod Builders tab
------------------------

Tools for generating your own content mods without writing JSON by hand.

  Cylinder Pack Builder - builds a cylinder mod from your own audio files.
  See the Cylinder Pack Builder wiki page for the full walkthrough.

  Ruins Packager - import a VS schematic export, configure spawn conditions,
  and output a deployable ruin/structure content mod.

  Lorebook Builder - generates a VS lorebook mod from a simple text input.
  Adds readable in-game books/scrolls with your own lore text.

  Trader Builder - write trader dialogue and shop inventory in a plain-text
  format and output a working VS trader entity mod. No C# needed.


Edit menu
---------

Find (Ctrl+F) - search the Diagnostics output.

Export to CSV - full scan results as a spreadsheet.

Export Per-Mod Log - filter the scan results to one specific mod ID and save
as a .txt file. Useful for sharing a specific mod's issues.

*Any of the 'Clear' Functions will ALWAYS ask for a confirmation and list the upcoming changes before you proceed*

Clear Unnecessary Configs - finds orphan config files in your VS data folder
from mods you've removed. Backs them up and moves them out.
  (This is still a Work in progress as it may not attach mods to their correct subfolder configs or
  if the config is named differently than the modID then it will attempt to move the config out of your active configs!)


Clear Cache - moves the VS cache folder to a holding folder so VS regenerates
it clean on next launch. Does not delete - just moves.
(As it stands it will NOT overwrite previously moved Cache automatically, at this time; I may make it merge in the future)

Clear Outdated Mods - after a scan, moves older duplicate mod versions to a
holding folder so you can review what got cleared.



Update menu
-----------

Click Update in the menu bar to check for a newer release on GitHub. If one
is found, you can download it and the tool will restart and apply the update
automatically after closing.

Preferences
-----------

UI Scale - 75%, 90%, 100%, 110%, 125%, 150%. Restart the tool to apply.

Font Size - dropdown in the top-right corner of the window, next to the
Theme selector. Applies immediately without a restart.

Theme - a handful of color themes. Rhath's Picks is a teal/orange theme,
others are variations on dark themes. Applies live.

Mods Folder / VS Install Path - set these if the auto-detect doesn't find
the right locations. Normally auto-detects from the registry and common paths.


Keyboard shortcuts
------------------

Ctrl+F - open search in Diagnostics tab
Ctrl+A - select all text in active field
Escape - close find bar or dialog
