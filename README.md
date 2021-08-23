## Collection of m3u Radio Playlists, Updated Weekly (manually)

### How to use these?
in the terminal, do this:
```
mpv https://raw.githubusercontent.com/junguler/m3u-radio-music-playlists/main/trance.m3u
```
or add/change m3u file association in your os to mpv and double click on any of .m3u files in your file manager

### Mpv only shows a black window when listening to music, how to make it pretty?
download the [visualizer](https://raw.githubusercontent.com/mfcc64/mpv-scripts/master/visualizer.lua) script for mpv and put it in your scripts folder either on ~/.config/mpv on *nix systems 

or C:\users\USERNAME\AppData\Roaming\mpv\ on windows

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
make a file called input.conf either at the folder your mpv.exe is or on ~/.config/mpv/ if you are *nix systems, put these inside it for using page-up and page-down for changing radio stations
```
PGUP playlist-prev ; show-text "${playlist-pos-1}/${playlist-count}"
PGDWN playlist-next ; show-text "${playlist-pos-1}/${playlist-count}"
```
### How to download all of the files?
use the [auto-generated zip](https://github.com/junguler/m3u-radio-music-playlists/archive/refs/heads/main.zip)

### Where did you find these?
from [this page](https://www.radio.pervii.com/en/online-playlists-m3u.htm)

### The websites mentions these being automatically updated
it's true but i only update this repo once every week as it's enough for me, you can use the links from the website instead if you are only interested in a few of those music genres
```
mpv https://www.radio.pervii.com/top_radio_trance.m3u
```
if you want to download those playlist files yourself more frequently and don't want the the top_radio_ prefix behind every file use this command on bash or zsh in the folder you have downloaded them
```
for filename in ./*; do mv "./$filename" "./$(echo "$filename" | sed -e 's/top_radio_//g')";  done
```
