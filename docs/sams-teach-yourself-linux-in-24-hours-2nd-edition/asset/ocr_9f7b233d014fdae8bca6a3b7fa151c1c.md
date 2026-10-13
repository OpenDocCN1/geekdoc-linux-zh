# Starting KDE

By default, you'll start KDE after logging into the kdm, or KDE display manager login. However, if you've disabled the login manager, you should know that there's another way to start KDE. When you log in to your OpenLinux console without X11, you're greeted with the following:

You can start X11 with 'startx' or KDE with 'kde'.

This is true, but if you've configured X11 with the xf86config command, and simply type kde and press Enter, your KDE and X session will start using only 256 colors, or an eight-bit pixel depth. To use a greater color depth, start your X sessions using the -- -bpp, or bits-per-pixel option. For example, to start KDE with thousands of colors, type kde, followed by the -bpp option, like so:

```
# kde -- -bpp 16
```

If you're fortunate enough to have a graphics card supporting millions of colors, try

```
# kde -- -bpp 24
```

or

```
# kde -- -bpp 32
```

![](bbox=[0.04, 0.7, 0.15, 0.84])

> The available color depths are defined in the XF86Config file found under the /etc directory. Look for the Depth settings in the Display subsection of the Screen section. If you configured X11 by editing XF86Config, use pound sign (#) characters to comment out lower color-depth settings. Another way is to use the DefaultColorDepth option, followed by 8, 15, 16, 24, or 32, in the Screen section. You can then just type kde to start X11 at higher color depths. For details about configuring X11, see Hour 3, "Configuring the X Window System and OpenLinux."