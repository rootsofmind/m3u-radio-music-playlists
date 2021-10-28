## Collection of m3u Radio Playlists, Updated daily (manually)
this repo now includes two extra streams made by me, `---everyhting.m3u` and `---randomized.m3u`

`---everyhting.m3u` combines all of the streams sorted by name

`---randomized.m3u` is exactly like the everything stream but every line was shuffled and randomized

both files have had extra info and cover art links removed to make them smaller and easier to download and load into a player, every time i push an update these two files will also get updated and the randomized stream will also get shuffled again

### How to listen to these?
in the terminal, do this:
```
mpv https://raw.githubusercontent.com/junguler/m3u-radio-music-playlists/main/trance.m3u
```
or add/change `m3u` file association in your os to mpv and double click on any of `.m3u` files in your file manager

### Mpv only shows a black window when listening to music, how to make it pretty?
download the [visualizer](https://raw.githubusercontent.com/mfcc64/mpv-scripts/master/visualizer.lua) script for mpv and put it in your scripts folder either on `~/.config/mpv/scripts` on *nix systems 

or `C:\users\USERNAME\AppData\Roaming\mpv\scripts\` on windows

put these in your mpv.conf, this is a auto-profile for all audio files
```
[audio-only]
profile-cond=(get('estimated-frame-count',math.huge)<2)
profile-restore=copy
vf-add=drawbox=w=iw:h=ih:color=00FFFF@0.5
vf-add=drawbox=x=3:y=3:w=iw-6:h=ih-6:color=00FF00@0.5
vf-add=drawbox=x=6:y=6:w=iw-12:h=ih-12:color=FFFF00@0.5
vf-add=hue=H=0.1*PI*t
```
### I really like mpv, how do i customize keybinds?
make a file called input.conf either at the folder your mpv.exe is on windows or on ~/.config/mpv/ if you are *nix systems, put these inside it for using page-up and page-down for changing radio stations
```
PGUP playlist-prev ; show-text "${playlist-pos-1}/${playlist-count}"
PGDWN playlist-next ; show-text "${playlist-pos-1}/${playlist-count}"
```
### Isn't there an easier way to use and control these using mpv?
yes there is, use the [IPTV script](https://github.com/gthreepw00d/mpv-iptv) which comes with fuzzy finding stations, better keybinds and ...

### How to download all of the files?
use the [auto-generated zip](https://github.com/junguler/m3u-radio-music-playlists/archive/refs/heads/main.zip)

### Where did you find these?
from [this page](https://www.radio.pervii.com/en/online-playlists-m3u.htm)

### why did i stopped the automatic updates?
i did a two week test run of updating this repo automatically every 6 hours but from the git stats i've seen it didn't get enough clones to warrant such updating frequency, i will keep the updates to once or twice every day for the time being and see what happenes.
