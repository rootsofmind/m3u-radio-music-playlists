## Collection of m3u Radio Playlists, Updated daily (manually)
this repo now includes a `radio.m3u` station with various streams collected over time by many people, thanks to [ArnoldSchiller](https://github.com/ArnoldSchiller) for his pull request, this stream is not part of my usual stream updates and won't get updated as often but it's contents are getting included in my 2 own made streams listed below

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

### How do i push updates?
if you just want to listen to music you won't need to keep reading but if you are interested to know how i do this keep reading

at first this process was manuall but i finally got around to write a simple bash script to make this process fast and easy, i'll go over each step here one by one

1st step: we need to get the links from the website [here](https://www.radio.pervii.com/en/online-playlists-m3u.htm) these files are automatically updated and sorted by popularity but the links themselves never change so after this one line command we don't need to repeat this frist step ever again and we can save these links to a text file for future downloads
```
lynx --dump --listonly --nonumbers https://www.radio.pervii.com/en/online-playlists-m3u.htm | grep ".m3u" | grep "top_radio" > list.txt
```
now for the explanation of what we did: 

lynx is a terminal web browser that doesn't load any kind of media and only shows links, text and stylings, we use it's `--dump` flag to save all the text and links from the website

grep is a powerful program that takes strings of characters and grep them to assist us in finding the stuff we need we used a pipe `|` to take the information lynx gave us and send it to grep, we first look for every `.m3u` file in the page and then further filter these links by `top_radio` in the next grep command to only get the file links we need, finnaly use `>` to write all of these information to the `list.txt` in the current directory we are in

2nd step: we use aria2 to download these files to our preffered directory in our case `~/Music/bare_m3u/`
```
/usr/bin/aria2c -x 16 -j 4 -i ~/Music/list.txt -d ~/Music/bare_m3u/
```
note that every time we use a program in a script we want to avoid using `cd` (change directory) and always want to use the full path of every program we use, for finding where a program is just do which and then the name of the program like this: ``which aria2c`` which gives us this ``/usr/bin/aria2c``

the flags we used with aria2 is as follows: `-x 16` tells aria2 to use 16 connections to download every file (this makes the download faster), `-j 4` makes it that aria2 download 4 files at a time, `-i` takes our input txt file we made in the first step and `-d` tells aria2 to download to that specific directory

3rd step: remove the top_radio_ prefix from every file since it's not needed for our use case
```
for f in ~/Music/bare_m3u/*.m3u ; do mv "$f" "$(echo "$f" | sed -e 's/top_radio_//g')"; done
```

4rd step: make the ---everyhting.m3u out of our downloaded m3u files
```
ls ~/Music/bare_m3u/*.m3u -v | xargs cat | sed -n '/^#/!p' > ~/Music/bare_m3u/---everyhting.m3u
```
because `cat` doesn't list alphabetically we use `ls` in tandom with it, use `sed` to remove every line that starts with `#` to make the final file smaller and write everything to the final m3u stream

5rd step: make the ---randomized.m3u stream by shuffeling the contents of ---everyhting.m3u
```
cat ~/Music/bare_m3u/---everyhting.m3u | shuf > ~/Music/bare_m3u/---randomized.m3u
```
`shuf` does the shuffeling for us

6rd step: move everything to our repos git directory, all the git stuff happens here, the move command overwrites everything that was there before
```
mv ~/Music/bare_m3u/*.m3u ~/Music/m3u-radio-music-playlists
```

last step: add, commit and push to your repo
```
git -C ~/Music/m3u-radio-music-playlists add .
git -C ~/Music/m3u-radio-music-playlists commit -m "updating"
git -C ~/Music/m3u-radio-music-playlists push
```
you will need a personal access token for repeat pushes to your repo from the terminal, look [here](https://docs.github.com/en/get-started/getting-started-with-git/why-is-git-always-asking-for-my-password) for more information about it 

if you are the only person who uses your computer you can set git to always remember your username & password using this command on your repos local folder:
```
git config credential.helper store
```

now for the complete script, save it to a file and give it `.sh` extension and run ``chmod +x script.sh`` on it and it's ready to use, next time you want to push an update just do ``script.sh`` in your terminal
```
#!/bin/bash

/usr/bin/aria2c -i ~/Music/list.txt -d ~/Music/bare_m3u/
for f in ~/Music/bare_m3u/*.m3u ; do mv "$f" "$(echo "$f" | sed -e 's/top_radio_//g')"; done
ls ~/Music/bare_m3u/*.m3u -v | xargs cat | sed -n '/^#/!p' > ~/Music/bare_m3u/---everyhting.m3u
cat ~/Music/bare_m3u/---everyhting.m3u | shuf > ~/Music/bare_m3u/---randomized.m3u
mv ~/Music/bare_m3u/*.m3u ~/Music/m3u-radio-music-playlists
git -C ~/Music/m3u-radio-music-playlists add .
git -C ~/Music/m3u-radio-music-playlists commit -m "updating"
git -C ~/Music/m3u-radio-music-playlists push
```
