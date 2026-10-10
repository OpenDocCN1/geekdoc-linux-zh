Although most mobile Linux users will always want to use the highest resolution available, there might be instances when you want to use a lower resolution. You’ll have to experiment with different settings in your XF86Config file. You should also read about your notebook’s graphics chipset in a readme file under the /usr/X11R6/lib/X11/doc directory.

# ## Using Multiple X Sessions

If you don’t configure Linux to boot directly to X11, you most likely use the *startx* command to jump to your X session. This command has a number of interesting features and command-line options you can use to start multiple X11 sessions on your notebook (if you have enough RAM). Why would you want to do this? Because you can then run different X11 window managers, use X11 at different screen resolutions, or run a session using a different *color depth*, or number of colors.

To start multiple X sessions, configure your Red Hat (or Mandrake) /etc/inittab to boot Linux to multiuser mode, or runlevel 3. Next, log in and use the *startx* command to start your X session:

```
# startx -- :0 vt7
```

After you press Enter, X will start and use the default display (:0) and default virtual console (7). To start another X11 session, press Ctrl+Alt+F2. You’ll see another text-only login prompt. Log in, and again use *startx* to start another X11 session:

```
# startx -- :1 vt8
```

You’ll end up in another X11 session running on a different display (:1) and using a different virtual console (vt8). To jump to the other X11 session, press Ctrl+Alt+F7. After working in that X desktop, you can jump back by pressing Ctrl+Alt+F8. To jump to a new text-only session, press Ctrl+Alt+F3. After working at the command line, you can jump back to either X session by pressing Alt+F7 or Alt+F8.

This is a great way to show off the features of your Linux notebook and a quick way to jump between different window managers. You should know, however, that running multiple X11 sessions can quickly exhaust your system’s memory and tax system resources! Properly log out of each running X session to return memory to the Linux kernel.

# ## Changing the Number of Screen Colors

The *startx* command may also be used to start X using a different number of colors (color depth). Your notebook’s graphics chipset must support the desired