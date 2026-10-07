TrueType font support XFree86 4.0 adds support for TrueType fonts (the stan-
dard font type in Microsoft Windows). In practice, TrueType fonts have been avail-
able in Linux for some time through separate font servers, as described shortly in
"Configuring a Font Server." Built-in TrueType support is an added convenience.

DRI support The Direct Rendering Interface (DRI) is a hardware acceleration
standard that allows Linux programs to take advantage of video boards with 3-D
hardware acceleration features. As of XFree86 4.0.1, only the 3dfxs chips are sup-\ported, but this support is likely to expand in 2001 and beyond.

New configuration file format The new XFree86 options mandate a new configu-
ration format. The configuration file may be called XF8Config, or it may be
halled XF8Config-4 on some systems (including Red Hat 7.0).

You can check whether you're running XFree86 4.0 by looking for a link X
in /etc or /etc/X11. If this link points to /usr/X116/bin/XFree86, your system is con-
figured to use XFree86 4.0. If the link points to some other file, your system uses
3.x or possibly a third-party X server (see the sidebar "Alternatives to XFree86").

# Configuring XFree86 4.0

For an administrator, the XFree86 4.0 change that's important is to change the
configuration file format. The general organization of the new XF8Config file is similar
to that 3.x's XF8Config, so you should read "The XF8Config File" earlier, for details.
In addition, the new file adds a few extra sections:

+   * ServerLayout This section defines some overarching features of the server. Speci-
ically, this section binds specific input and output devices. Chances you won't
eed to adjust this section from its default.
* Module2 This section specifies server modules you want loaded. Modules can pro-
vid functionality such as TrueType support and DRI support. You probably won't
have to adjust this section of the file.
* DRI If you're lucky enough to have a video card with 3-D acceleration features sup-
ported by XFree86, you can define who may access these features in this section. A
s line allows all users to access DRI functions:

Mode 0666

In Red Hat 7.0, there's only one standalone X configuration utility: xf86cfg. This is an
X-based configuration tool (see Figure 16.3). To configure X with this utility, you can
right-click the icon for a component in the main section of the window and select Con-
figure from the resulting pop-up menu.