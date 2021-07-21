if you don't know how to use these use mpv in the terminal

mpv https://raw.githubusercontent.com/junguler/m3u-radio-music-playlists/main/top_radio_trance.m3u

or add/change m3u file association in your os to mpv and double click on any of these in your file manager

in your mpv's input.conf file add these lines to be able to go back and forward in the playlist using page up and page down:

PGUP playlist-prev ; show-text "${playlist-pos-1}/${playlist-count}"

PGDWN playlist-next ; show-text "${playlist-pos-1}/${playlist-count}"

these are downloaded from this page https://www.radio.pervii.com/en/online-playlists-m3u.htm i removed things like talk and news and only left music playlists
