```
[root@redhat X11]# ls -l X
lrwxrwxrwx 1 root root 29 Aug 21 15:32 X ->
../../../usr/X11R6/bin/XF86_SVGA
```

This shows the `/etc/X11/X` file is linked to `/usr/X11R6/bin/XF86_SVGA`, which is the SVGA X server. Since XFree v4 does not have separate X servers, the `X` file is linked to the same server, as shown here:

```
debian:/etc/X11# ls -l X
lrwxrwxrwx 1 root root 20 Dec 11 10:55 X ->
/usr/bin/X11/XFree86
```

The file `/usr/bin/X11/XFree86` is the X server for v4 and will always be the destination of the link.

The main configuration file for the X server is the `XF86Config` file. The format for this file is similar between XFree v3 and v4, but some slight differences exist. If you use one of the provided tools to create this file, you do not need to worry about the differences.

One of the best enhancements in XFree v4 is speed. XFree v4 noticeably increases performance over XFree v3. The new version also supports greater hardware acceleration for games and graphic applications.

# # Configuring X

## 2.10 X

![](bbox=[0.13, 0.59, 0.18, 0.62])

+   -   Install & Configure XF866. Verify that the video card and monitor are supported by an X server, install the correct X server, configure the X server, install an X font server, install required fonts for X (may require a manual edit of /etc/X11/XF86Config in the "Files" section), customize and tune X for videocard and monitor. Commands: XF86Setup, x86config. Files: /etc/X11/XF86Config, .xresources.

Configuring the X Window System can stop a new Linux user in their tracks. It can turn into a very complicated problem with odd error messages and strange results. Since most distributions now do an excellent job of detecting the hardware and monitor on a system, users do not need to go through all of the procedures that used to be required. But, if you install X manually or have an unusual setup, you may still be faced with configuring X yourself. The two configuration tools covered here can be used with any distribution. Further, each distribution commonly supplies its own distribution-specific tool. For example, Red Hat uses Xconfigurator, Mandrake uses DrakX, and Debian uses anXious and Dax.

The configuration file for the X server is `XF86Config`.