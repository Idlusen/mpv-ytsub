# mpv-ytsub
This script lets you easily load the automatic captions generated by youtube for its videos,
either interactively or automatically with preconfigured languages.

It could work for other video providers as well as long as `youtube-dl` (or `yt-dlp`, depending on
your setup) populates the JSON it returns to `mpv` with the subtitles URLs.

## Dependencies
This script uses the Lua 5.1 `luasocket` and `luasec` modules to download the subtitles directly
from the youtube URL.

Alternatively, if either of these modules is missing, the script downloads the subtitles via `yt-dlp`.
Note that the `yt-dlp` solution is a bit slower.

For the time being should not work on systems other than Linux due to the method used to cache subs files.

## Installation
Just copy `ytsub.lua` in your mpv scripts directory.

## Usage

### Load subtitles for a language selected interactively
Hit `alt+y` to fire up the mpv console selector with the list
of available languages. The subtitles for the selected language are downloaded, added as a track
and the track is selected as primary subtitles.

### Load subtitles automatically
When hitting `alt+shift+y`, the script loads the subtitles
for the original language of the video as primary subtitle track and the subtitles for a source
language as secondary subtitle track.

## Options
- `load_autosub_binding`: key binding used to select a language and load subtitles. See `mpv` manual for the key bindings syntax.
- `autoload_autosub_binding`: key binding used to load subtitles with automatic language selection.
- `source_lang`: the source language used when loading subtitles automatically. 2-letter code as used by Youtube.
- `cache_dir`: path where the subtitles files are cached.

## `mpv` usage reminders
To set a script option, use the `--scripts-opts` (see `man mpv`) command-line argument, that can also
be set in `mpv.conf`.
For instance, use on the command-line:
```
mpv https://youtu.be/<ytid> --script-opts=ytsub-source_lang=en
```
And to set it permanently, add in your `mpv.conf` the line:
```
script-opts=ytsub-source_lang=en
```

As two simultaneous subtitles tracks can clutter the video a bit, remember you can set the subtitles font size,
with `shift+g` and `shift+f` by default.
