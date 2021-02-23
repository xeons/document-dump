You can configure sudo not to require a password for specific commands, by adding a sudoers rule with the NOPASSWD: tag. Note that NOPASSWD rules must come after non-NOPASSWD rules that match the same command.

```
%admin: ALL = (ALL:ALL) ALL
%admin: ALL = (root) NOPASSWD: apt-get
```

Note that allowing apt-get is as dangerous as allowing any command, since the caller could pass options that cause apt-get to download packages from sources that they specify, that cause it to invoke hooks that they specify, etc.
