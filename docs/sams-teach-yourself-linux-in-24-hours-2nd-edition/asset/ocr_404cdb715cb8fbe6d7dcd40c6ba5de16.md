This command sets the screen saver to run after five minutes of no keyboard or mouse activity. You can control this client with the xscreensaver command client to turn the xscreensaver on or off or to activate it immediately. Although the xscreensaver client has a -lock option to password-protect your display, you have to recompile the program to enable this feature.

The xscreensaver client comes with nearly two dozen different screen savers, which can also be run as standalone programs. For example, you can run the fractal drawing program, hopalong, in a window, as follows:

```
# hopalong
```

After you press Enter, a fractal image appears in a window (as shown in Figure 7.9), so you can see what it looks like.

# FIGURE 7.9

The hopalong client is part of a screen saver for X11.

![](bbox=[0.27, 0.55, 0.88, 0.88])

For a list of the screen savers that work with the xscreensaver client, read the file XScreenSaver in the /usr/X11R6/lib/X11/app-defaults directory. You can find other settings in the file, which is the X11 resources file for this client.

You might also be interested in the xlock client. Although it is not a screen saver, xclock is a sophisticated terminal-locking program with nearly 50 command-line options and more than 50 different displays built in. The xlock client is helpful if you want to password-protect your display to prevent others from using your computer while you're away.