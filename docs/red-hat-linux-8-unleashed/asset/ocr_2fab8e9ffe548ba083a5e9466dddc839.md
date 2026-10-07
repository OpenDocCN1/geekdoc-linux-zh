which is included with XFree86, and Owen Taylor's xsri client, as specified in the file Xsetup_0 in the xdm directory /etc/X11. The xsri client is used to set the background color of the login display's desktop and to place an image of Red Hat's logo in the upper-left corner of the display.

# Starting X from the Console by using

If you have Red Hat set to boot to runlevel 3, a text-based console login, you can start an X session from the command line. You use the startActivity command (which is actually a shell script) to do so. You launch the X server and an X session by using startx, like this:

```
$ startx
```

startX first looks in your home directory for a file named .xinitrc. This file can contain settings that will launch an alternative desktop and X clients for your X session. The default system .xinitrc is found in the /etc/X11/xinit directory, but a local file can be used to customize an X session and launch defaults. For example, you can download and install the mlwm window manager, which is available from http://www.w2u.biglobe.ne.jp/~y-miyata/mlwm.html in the /usr/local/bin directory. You can then use the mlwm desktop for your X session, the xterm terminal client creating a .xinitrc file containing the following:

xterm &

```
exec /usr/local/bin/mlwm
```

Using a custom .xinitrc is not necessary if you're using Red Hat's desktop, which runs X and either a GNOME-aware window manager or KDE as a desktop environment.

You can also use the startActivity command with one or more command-line options. These options are passed to the X server before it launches an X session. For example, you can use startx to specify a color depth for an X session using the -depth option, followed by a number as 8, 16, 24, or 32 for 256, thousands, or millions of colors (as defined in the X configuration file and if supported). Using different color depths can be useful during development, for testing how X clients look on different displays, or to conserve of video memory, such as when trying to get the highest resolution (increased color depth can sometimes affect the maximum resolution of older video cards).

For example, to start a session with thousands of colors, you use the startActivity command like:

```
$ startx --depth 16
```

Another option that can be passed is a specific dots-per-inch (dpi) resolution that is to be used for the X session. For example, to use 100 dpi, use the -dpi option followed by one, like this:

```
$ startx -dpi 100
```