# SuSE 6.1 749

S - Single user 4 - not used
1 - Multiuser without network 5 - not used
2 - Multiuser with network (default) 6 - Reboot

The rc scripts are located in /sbin/init.d. This has the advantage that the /etc directory effectively contains only configuration files, while all executable-programs are located in /sbin.

# rc.config / SuSEConfig

SuSE uses /etc/rc.config together with the files in the /etc/rc.config.d subdirectory as central configuration files. Both yast and the Init-V process access this file. Even manual changes are possible. However, you may subsequently execute SuSEConfig to transfer the settings to other system files as well. If you modify rc.config via, SuSEConfig is executed automatically.

# lib compatibility

With version 6, SuSE was changed over to the new libc library. If you still want to execute lib programs, you need to install the optional lib compatibility package, which is hidden in the series under the name of shlibs5.
The libraries are installed here. Here, in the /usr/i486-linux-libc5/lib directory and linked to /etc/ld.so.conf. The space requirement of this package is quite considerable - more than 40 Mbytes! The reason is that it contains not only the base library but also the X libraries derived from it. Even the Qt library for old KDE programs are present.

# Problems with the Ctrl key

In the default configuration, SuSE swallows key combinations with the right-hand Ctrl key. If, for example, in XEm you enter Ctrl+- twice, the cursor is moved by one word to the left.

The cause lies in /usr/X11R/lib/X11/Xmodmap or in the local file /.Xmodmap. Here, the Ctrl key (code 109 or hexadecimal 0xD6) is defined as the Multi_key symbol. If you want the Ctrl to work without problems, you need to comment this out by means of an exclamation mark and assign 109 to Control_R instead.

```
! modification in /usr/X11R6/lib/X11/Xmodmap or in /.Xmodmap
! keycode 109 = Multi_key
keycode 109 = Control_R
```