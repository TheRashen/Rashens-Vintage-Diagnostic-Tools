Rashen's Vintage Diagnostic Tools - v0.7.2.x
==========================================

Mod scanner for Vintage Story. Point it at your mods folder, hit Scan,
and it tells you what's broken - missing deps, conflicts, bad recipes,
log spam sources, whatever.

Works fine on big packs (100+ mods). Runs local, no internet, no install.

I have attempted to include an all-rounded HELP menu embedded inside of the application itself at the bottom left corner "Help" button.. Before you post to my issues tab on my github please look over that first.


Requirements
------------

Windows
Vintage Story installed (needed for save file and cache operations - the
tool doesn't run VS, just needs to know where it is)
It doesn't necessarily HAVE to have VS installed, it can actually be ran just as a log checker to make things a little easier to parse if you merely use it to 'scan runtime logs' and point at a log location or add files to it. Otherwise, yes it needs a VS data location.


How to run
----------

Double-click the exe. Nothing else needed. 
(Unless you want to use the Cylinder Pack Builder, then you need to make sure you follow the instructions below)


Tabs
----

Diagnostics
  The main scanner. Runs dep checks, conflict detection, broken recipe
  detection, entity spawn inspection, and a deep scan that reads every
  JSON in every mod. Results have Ctrl+F, expand/collapse, and a sidebar
  for jumping between sections.



Memory Watcher
  Attach to a running VS process and watch RAM live on a graph. Drop named
  event markers at any point so you know what was happening at each spike.
  Detach whenever - the graph stays frozen so you can still look at it.

  -I Personally run this attached to my server as soon as it gets done caching.. After about the first hour I close it off. But it allows me to get an idea (It can also export the memory data but its a WIP) of what is using the most RAM on startup. I aim to get this to attach to tickrates and other specific information later on in development for use like VisualVM is for MC etc..



Loot Search
  Type an item or block code and it scans every mod zip for references to
  it. Shows which JSON files matched and on what line. "All" mode lists
  everything in scope without a search term..



Experimental Patcher
  Extra tools: patch mod builder, JSON error fixer, dep version fixer,
  language file stripper, spawn rate override generator, DLL framework
  checker, and the Custom Cylinder Pack Builder.



  Cylinder Pack Builder - format notes:
    - OGG files must be Vorbis-encoded. OGG containers with Opus or FLAC
      inside are rejected - VS's audio decoder only handles Vorbis. This
      is common with OGGs downloaded from certain sites (YouTube rips, etc).
      Re-encode with ffmpeg: ffmpeg -i input.ogg -c:a libvorbis output.ogg
    - MP3 files require ffmpeg on your (installed on your system and enabled in your enviroment variables) PATH. If ffmpeg isn't installed, MP3s are silently skipped. Get it at ffmpeg.org (add to PATH during or after install). Once on PATH, restart the tool and rebuild.
    - Conversion uses libvorbis quality 4, which is fine for game audio.
    - Subfolder structure is preserved in track names if you organize by
      album/game. All subfolders are scanned recursively.
    - When you run the pack builder please note that all the features may not currently work as expected and it will continuesly open ffmpeg and close it in a shell window until it is done with the current task. That being said, it will output an error if it messes up at anypoint but it will attempt to still make the 'mod' regardless if 99% of the tracks are unable to be added properly.
    - It adds loot table drops to Drifters & Bells at a low drop-rate, default is 0.05 you are free to change these values by opening up the cylinder pack zip and going to the "assets/name/patches/" and selecting one of the two jsons that handles the different drops. I have tested this and it works with even multiple of these packs installed.


Edit menu
---------

Find (Ctrl+F) - search the scan output (sometimes the scroll bar may not show a proper highlight in the right spot, I'm currently redesigning the entire interface layout)
Export to CSV - full scan results as a spreadsheet
Export Per-Mod Log - filter to one mod ID and save as .txt
Clear Unnecessary Configs - finds orphan config files from removed mods,
  backs them up and moves them out
Clear Cache - moves VS cache to a holding folder so VS recreates it clean
Clear Outdated Mods - after a scan, moves older duplicate mod versions to
  a holding folder for review

The "Clear" functions do not delete them, it simply moves these things to a standalone folder within the "\VintagestoryData\"" location named "ToBeDeleted" so it is outside of your server/client's data folders and will not be ran on startup anymore, please be sure to delete these when you want to delete them. I did it this way incase it errors out and deletes things you may not want to be deleted..
"Clear" for configs still does not work 100% as intended It is hard for me to "wildcard" for all config types when configs aren't always named the same thing the mod is.


Preferences
-----------

UI Scale - 75% / 90% / 100% / 110% / 125% / 150% (restart to apply)
Theme - multiple color themes


Output
------

Everything the tool generates goes into an output\ folder next to the exe.
Nothing is written to your VS installation or mods folder directly.





------

The only other location that may be written is in your %appdata% location, you can see this by going into Preferences>Theme Manager/Theme Folder. That location is where the themes are handled outside of the standard. Again the interface is still a WIP so not all of it may work correctly or as intended. 

But it will never alter or disrupt your system and it uses a very very low overhead hardware cost to run. (I run it on my windows 7/linux old pc for testing on different OS and it works fine)


------

PLEASE NOTE: This is a ONE-FILE compiled software made entirely within PYTHON, as that's the language I'm best with. 



Absolutely NO LLMs('Ai') were used during the creation of this, if something 'seems' 'ai' it is merely a happenstance due to what popular llms were used to train on was more than likely the same, or similar, sources i learned all coding from over the past 2-in-a-half-decades.

I also study user interfaces, aswell as other nuanced everyday things and features that modern technology has for optimal user functionality, as a Game Dev and systems architect I use my knowledge to attempt to make things as visually pleasing as possible to our eyes as no one want to be hunched over scanning lines all day, especially folks who are *not* coders or in tech fields.



This program as it is a ONE-FILE compilation **will** be flagged by antivirus' because it isn't, *bear with me here....*, "digitally signed" by some archaic system that gatekeeps software development.   This is a **clean** file.
