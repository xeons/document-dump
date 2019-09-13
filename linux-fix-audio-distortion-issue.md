## Stop audio distortion issue on Linux Mint 19.2 (could affect other ubuntu flavors as well)

1. Open pulse audio configuration file.

```
nano /etc/pulse/default.pa
```

2. find a line containing:

```
load-module module-udev-detect
```

3. modify this to become:

```
load-module module-udev-detect tsched=0
```

4. then run this to kill existing pulseaudio

```
pulseaudio -k
```

### Why this works?

This disables something called "Glitch-free audio" which doesn't seem to play nice with my sound chip (ALC1220). 

Ironic given the name, since it's causing me glitches!
