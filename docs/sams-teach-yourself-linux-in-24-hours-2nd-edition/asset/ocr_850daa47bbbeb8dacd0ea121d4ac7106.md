5. To go to your KDE session, press Ctrl+Alt+F7. To go to another virtual console, press Ctrl+Alt+F3 (because the first and second are being used). To go back to fvwm, press Ctrl+Alt+F8.

# Logging in to OpenLinux and X11 with xdm

The default configuration of OpenLinux is to boot Linux to a login prompt for a console, or shell command line. You can, however, boot OpenLinux directly to an X11 login prompt. This can be done by passing a kernel message, or boot-prompt option, through the LILO boot prompt or by configuring OpenLinux to start X11 and the xdm, or X display manager client, after booting.

> You must properly configure X for your computer's graphics card before trying this, or you can lock up your system!

To boot directly to the xdm login screen, turn on your computer, and at the LILO boot prompt, type the following:

```
linux 5
```

After you press Enter, Linux boots and presents the xdm login screen, as shown in Figure 7.3. This method works by booting OpenLinux directly to a particular run level, as specified in the OpenLinux system initialization table, inittab, under the /etc directory. Run level 5 is defined in /etc/inittab as follows:

```
x:5:respawn:/usr/bin/X11/xdm -nodaemon
```

This line specifies that when OpenLinux is started, the login prompt is provided by xdm. To start your X session (which uses fvwm by default), type your username, press Enter, then type in your password, and press Enter again.

To configure OpenLinux to boot directly to this login screen, log in as the root operator, and then open /etc/inittab with your favorite text editor. Scroll through the file until you see the following:

```
# Default runlevel.
id:3:initdefault:
```

> Editing your system's initialization table is inherently dangerous! Make a backup copy first, and make sure to disable line-wrapping (such as using the -w option with the pico editor) when editing this file.