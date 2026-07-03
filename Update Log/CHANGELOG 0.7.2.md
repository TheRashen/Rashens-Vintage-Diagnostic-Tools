CHANGELOG
=========


v0.7.2 - July 2, 2026
----------------------

Added "Clear Outdated Mods" to the Edit menu. After running a scan it checks
for duplicate mod IDs and moves the older ones to VintageStoryData/ToBeDeleted/
OutdatedMods/ so you can review before deleting. Nothing gets removed outright.

Cylinder Pack Builder - added Vorbis validation. It now rejects OGG files using
Opus encoding inside the container, which crashes VS's audio decoder when played.
Rejected files are listed in the output with a clear reason so you know what to
re-encode. (Working on getting it to strip the Opus encoder from files and some other new future implementations!)

Fixed the Jump To sidebar - expand/collapse was intermittently broken on Windows.
The sub-buttons would sometimes do nothing or sections would appear empty after a
scan. Root cause was pack positioning across sibling frames being fragile under
Tkinter's layout engine. Fixed by wrapping each header and its sub-buttons in a
container frame so ordering is always stable.

Fixed combobox dropdowns - they were opening with a white background instead of
matching the dark theme.


================================================================================

v0.7.1.1 - June 30, 2026
-------------------------

Cylinder Pack Builder fixes.

Fixed the lang key format for cylinder display names - without the right prefix
VS shows the raw key string instead of the name.

Fixed the modinfo.json game dependency format - was causing a version parse
warning on load.


================================================================================

v0.7.0.3 - June 29, 2026
-------------------------

Help text fix - "Scan Entity Spawns" was listed under the wrong tab.

Experimental tab log area removed - it was too small to be useful at most window
sizes. Output from all Experimental tools now goes to the Diagnostics tab log.

Custom Cylinder Pack Builder added to the Experimental tab. Point it at a folder
of OGG or MP3 files, give it a mod ID and pack name, and hit Build. Scans all
subfolders recursively, converts MP3 to OGG if ffmpeg is on your PATH, packages
everything into a mod zip with drifter drops and bell drops. Duplicate detection
via a local registry. MP3 files need ffmpeg on PATH to convert.

DLL Framework Check added - scans mod DLLs and reports which ones target old
.NET runtimes (pre-.NET 10 / pre-VS 1.22).


================================================================================

v0.7.0.1 - June 27, 2026
-------------------------

Minor fixes after v0.7.0. Nothing new.


================================================================================

v0.7.0 - June 27, 2026
-----------------------

Sub-navigation in the sidebar - sections that cover a lot of mods now show
individual jump buttons for each mod. Sub-buttons are smaller and indented.
Sidebar also scrolls now.

UI Scale setting added to Preferences - 75% through 150%, restart to apply.


================================================================================

v0.6.8 - June 25, 2026
-----------------------

Memory Watcher tab - attach to VS, watch RAM live on a graph, drop event
markers, check mod footprint estimates. Detach and graph stays frozen.

Loot Search tab - search mod zips for item/block code references. Shows which
files matched and on what line. "All" mode lists every JSON in scope.

Scan result additions - Ctrl+F search, Expand All / Collapse All, clickable
"...and N more" lines, dep version checker, null texture detection, reverse
dependency map.

Edit menu additions - Clear Unnecessary Configs, per-mod log export, CSV export.

Experimental Patcher additions - Repair JSON Errors, Language file stripper,
Spawn Override generator.

Overview ruler on the right side, section sidebar on the left.


================================================================================

v0.4.4 and earlier
-------------------

Initial release. Log scanner, basic diagnostics, mod dependency checker.
