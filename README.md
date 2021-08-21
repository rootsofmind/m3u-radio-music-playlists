# Collection of m3u Radio Playlists, Updated Weekly (manually)

if you don't know how to use these, use mpv in the terminal

>mpv https://raw.githubusercontent.com/junguler/m3u-radio-music-playlists/main/trance.m3u

or add/change m3u file association in your os to mpv and double click on any of these in your file manager

in your mpv's input.conf file add these lines to be able to go back and forward in the playlist using page up and page down:

>PGUP playlist-prev ; show-text "${playlist-pos-1}/${playlist-count}"
>
>PGDWN playlist-next ; show-text "${playlist-pos-1}/${playlist-count}"

to download the whole repo use the [auto-generated zip](https://github.com/junguler/m3u-radio-music-playlists/archive/refs/heads/main.zip)

these are downloaded from [this page](https://www.radio.pervii.com/en/online-playlists-m3u.htm)
