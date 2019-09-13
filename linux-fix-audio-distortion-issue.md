## Stop audio distortion issue on Linux Mint 19.2 (could affect other ubuntu flavors as well)

`nano /etc/pulse/default.pa`

then find a line containing:

`load-module module-udev-detect`

modify this to become:

`load-module module-udev-detect tsched=0`

then run this to kill existing pulseaudio

`pulseaudio -k`
