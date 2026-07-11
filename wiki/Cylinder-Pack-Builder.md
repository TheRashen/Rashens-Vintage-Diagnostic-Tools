Cylinder Pack Builder
=====================

Builds a Vintage Story tuning cylinder mod from a folder of your own audio
files. Output is a .zip you drop in your mods folder that adds new cylinder
items, playable on a resonator block or the Temporal Portable Resonator.

Found in the Custom Mod Builders tab.


How to use it
-------------

1. Click "Browse Audio Folder" and pick a folder of OGG or MP3 files.
   The status line shows how many files were found and whether ffmpeg is
   available for MP3 conversion.

2. Fill in the fields:
   - Mod ID: short lowercase alphanumeric ID for your pack, e.g. "myjams".
     This becomes the mod domain and can't have spaces or capitals.
   - Pack Name: display name shown in the VS mod manager.
   - Author: your name.
   - Item Desc: optional description that shows on each cylinder's tooltip.

3. Choose naming mode:
   - Generic: all cylinders named "{prefix} 1", "{prefix} 2", etc.
   - Custom: opens a dialog to name each track individually. Pre-fills with
     the filenames so you can just edit what you want changed.

4. Click "Build Cylinder Pack". The result and any skip reasons show in the
   Diagnostics tab. Output zip is in the output\ folder next to the exe.

5. Drop the zip in your VS mods folder and reload.


What it generates
-----------------

{modid}_1.0.0.zip with:
- modinfo.json
- assets/{modid}/itemtypes/cylinder.json  (one item variant per track)
- assets/{modid}/lang/en.json             (names and descriptions)
- assets/{modid}/patches/drifterdrops.json (all cylinders added to drifter drops)
- assets/{modid}/patches/belldrops.json   (added to bell/stack drops at 0.5 chance)
- assets/{modid}/music/{stem}.ogg         (one audio file per track)

Cylinders drop from all 6 drifter tiers at 1-5% depending on tier.
You may edit the drop rates by simply opening up the zip and going into the "modname.zip\assets\modname\patches\{Bell}{Drifter}drops.jsons"


Audio format requirements
--------------------------

VS's audio decoder only handles Vorbis-encoded OGG. OGG files with Opus,
Theora, embedded album art, or other non-Vorbis content inside (common from
YouTube rips, video files, and some music players) are automatically stripped
and re-encoded to Vorbis by the builder using ffmpeg. You don't have to
manually re-encode your collection first - the builder handles it.

MP3 files and non-Vorbis OGGs both require ffmpeg. If ffmpeg isn't on your
PATH, those files are skipped instead of converted. Install ffmpeg from
ffmpeg.org, add it to PATH, and restart the tool.

To check what's inside an OGG manually:
  ffprobe -v quiet -show_streams yourfile.ogg

To manually re-encode if you prefer to do it yourself first:
  ffmpeg -i input.ogg -c:a libvorbis -q:a 4 output.ogg

Conversion quality is libvorbis q4, which is 128-160 kbps average - fine
for game audio. Pure Vorbis OGGs aren't re-encoded, they go in as-is.

There's no file size or duration limit. VS handles long tracks fine.


Track naming and stems
-----------------------

Each audio file gets a "stem" - the filename with special characters replaced
by underscores and the whole thing lowercased. This stem becomes the asset
path for the audio file inside the mod zip (e.g. "OoT Gerudo Valley.mp3"
becomes "oot_gerudo_valley.ogg" inside the zip).

If two files normalize to the same stem, the second one gets _2 appended,
the third gets _3, etc.

Stem names are tracked in output\cylinder_registry.json so if you build two
packs from the same folder, duplicate stems across packs show a yellow warning.
This is just a heads-up - duplicates don't break anything, they just mean two
different cylinder mods share an internal asset name.


Rebuilding
-----------

The builder always outputs {modid}_1.0.0.zip regardless of how many times you
rebuild. If you need to update an existing installed pack, just overwrite the installed
zip with the new build. However if you're uploading this to the moddb, then update the modinfo.json and zip accordingly to match. As you would normally with any other mod.


(Currently looking for a way to do this differently. As it stands, The reason it is like this is because not all cylinder packs will be the same data-size and if it were to create seperate version'd packs then you'd quickly eat through your storage space fast)


Using with the Temporal Portable Resonator (Coming soon along side Albumable Resonators!)
-------------------------------------------
TBD