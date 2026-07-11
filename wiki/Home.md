Rashen's Vintage Diagnostic Tools - Wiki
=========================================

Quick reference for a few things


Where to find things
--------------------

All tool output to a folder: "output\"" next to the exe
Scan results: shown in the Diagnostics tab, exportable to CSV
Cylinder mod zips: output\{modid}_1.0.0.zip


Common questions
----------------

Q: The scan is slow on first run.
A: It's reading every JSON in every mod zip. 100+ mod packs take a minute
   the first time. Subsequent scans are faster.
   You can watch the progress at the bottom bar it counts up using ###/###

Q: What does "missing dependency" mean?
A: A mod in your folder lists another mod as a dependency in its modinfo.json,
   but that dependency isn't installed or is the wrong version.

Q: Is this safe to run on my live server/client mods folder?
A: Yes. The tool only reads your mods folder. It won't move or delete anything
   without your confirmation.

Q: MP3s or some OGG files are being skipped in the cylinder builder.
A: ffmpeg needs to be on your PATH. MP3s need it to convert, and OGGs with
   non-Vorbis content (Opus, Theora, etc.) need it to strip and re-encode.
   Without ffmpeg, all of those are silently skipped. Get ffmpeg from
   ffmpeg.org and make sure it's on PATH, then restart the tool.

Q: An OGG file was skipped even though it plays fine.
A: VS only handles Vorbis-encoded OGGs. Some OGGs - especially from YouTube
   rips or video files - have Opus or Theora inside instead. The builder
   strips those and re-encodes to Vorbis automatically using ffmpeg. If your
   file was skipped, ffmpeg probably isn't on your PATH. Install it from
   ffmpeg.org and restart the tool.
