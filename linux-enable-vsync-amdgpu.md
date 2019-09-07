Create or modify file:

>/etc/X11/xorg.conf.d/20-amdgpu.conf

Add this config section.

```
 Section "Device"
     Identifier "AMD"
     Driver "amdgpu"
     Option "TearFree" "true"
 EndSection
 ```
