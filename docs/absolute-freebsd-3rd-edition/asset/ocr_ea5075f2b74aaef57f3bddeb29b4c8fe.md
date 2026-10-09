the library instead. These global overrides must appear first in `libmap.conf`:

libGL.so          libGL-NVIDIA.so
libGL.so.1        libGL-NVIDIA.so.1

“May I have libGL.so.1?”

“Certainly, here’s libGL-NVIDIA.so.1.”

Globally remapping libraries is a rather bold step that might get you talked about by other sysadmins, but remapping libraries on a program-by-program basis is much less ambitious and more likely to solve more problems than it creates. Simply specify the desired program in square brackets before the remapping statements. If you specify the program by its full path, the remap will work only if you call the program by its full path. If you give only the name, the remap will work whenever you run any program of that name. For example, here we remap emacs(1) so that it uses Nvidia’s library instead of the system library when called by its full path:

```
[/usr/local/bin/emacs]
libGL.so        libGL-NVIDIA.so
libGL.so.1      libGL-NVIDIA.so.1
```

How can you prove this worked? Well, check `ldd(1)`:

```
# ldd /usr/local/bin/emacs | grep libGL
          libGL.so.1 => /usr/local/lib/libGL-NVIDIA.so.1 (0x80ad60000)
```

You can see that when `/usr/local/bin/emacs` requests libGL.so.1, rldd(1) attaches it to libGL-NVIDIA.so.1 instead. We specified the full path to the Emacs binary, however, so we need to call the program by its full path. Try to use `ldd(1)` on Emacs without calling it by its full path:

```
# cd /usr/local/bin
# ldd emacs | grep libGL
          libGL.so.1 => /usr/local/lib/libGL.so.1 (0x8056fa000)
```

By going to `/usr/local/bin` and running `ldd(1)` directly on Emacs without having to specify the full path, rldd doesn’t see the full path to the emacs(1) binary. `/etc/libmap.conf` says to use Nvidia’s library only for