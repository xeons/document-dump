# Linux - Enable VSync for AMDGPU driver.

1. Create or modify file:

```
/etc/X11/xorg.conf.d/20-amdgpu.conf
```

 2. Add this config section.

```
 Section "Device"
     Identifier "AMD"
     Driver "amdgpu"
     Option "TearFree" "true"
 EndSection
 ```
