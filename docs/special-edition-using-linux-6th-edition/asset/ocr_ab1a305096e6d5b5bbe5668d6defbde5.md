distribution specific, and you should check xsession itself to be sure. Some distributions will also skip this step if the user requested a specific session through kdm or gdm. In that case, xsession might just run the desktop or window manager directly.

+   - **Run Xclients**—The final fallback is almost always `/etc/X11/xinit/Xclients`. This script generally figures out what desktop or window manager the user wants (sometimes by querying distribution-specific configuration files), and starts it.

# ## Desktop or Window Manager Startup

The final startup step is generally an “exec” command that starts a desktop (KDE or GNOME for example) or a window manager (fvwm2 or Blackbox for example). The exec instructs the script to remove itself from memory before launching the desired environment. This not only saves memory, but also ensures that the rest of the script won’t be accidentally executed when the user logs out.

KDE starts with a script called `startkde`. This script launches the various servers that KDE needs for inter-process communication. It also starts the window manager, panel, and other useful applications.

GNOME starts with a script called `gnome-session`. This script does essentially the same things as `startkde`.

Window managers are generally started by simply running the window manager’s executable.

# ## Variation: `startx`

Your system does not have to be in runlevel 5 to start the X Window System. If XFree86 is not running, you can start it at any time using `startx`.

`startx` has a much simpler startup sequence than the display managers, but it is basically very similar.

After starting XFree86 itself, `startx` runs `/etc/X11/xinit/xinitrc`. This script is very similar to `xsession`, except that it will generally never start a desktop or window manager itself. It generally does not honor the user’s `$HOME/.xsession` script, but will generally honor `$HOME/.Xclients`. If the user does not have a `.Xclients`, then `xinitrc` will almost always run `/etc/X11/xinit/Xclients`, which will start a desktop or window manager.

# # Troubleshooting

*When XFree86 starts up, text flashes on the screen, the monitor clicks and then repeats too fast to stop it.*

In almost all cases, this indicates an error in your XF86Config file when your system is at runlevel 5.

![](bbox=[0.911, 0.798, 1.0, 0.915])