# 404 Understanding How Fedora Cores

# Understanding the GUI startup

The graphical login screen starts at run level 5. When the init process starts up at run level 5, the last line of the /etc/inittab causes init to start the graphical login process. Here's what the last line in the /etc/inittab file looks like (the number 5 denotes run level 5):

```
x:5-respawn:/etc/X11/prefdm -nodamem
```

This line calls init to run /etc/X11/prefdm, a script that starts a specific display manager — gdm, kdm, or xdm — depending on the setting of a variable DISPLAYMANAGER defined in the /etc/sysconfig/desktop file. The display manager is a program responsible for displaying the graphical login window, authenticating users who log in, running initialization at a start of a session, and cleaning up after the session. The display manager processes the display, making it available to the users and cleaning up after the user session.

If the DISPLAYMANAGER variable is not defined, the /etc/X11/prefdm script checks for gdm, kdm, and xdm in that order and runs whichever manager finds first. The end result is you get gdm if you installed GNOME and KDE as your sole desktop. If you install both GNOME and KDE you get gdm by default because the prefdm script looks for if you have both GNOME and KDE installed on your system and you want gdm as the display manager, define the DISPLAYMANAGER variable in the /etc/sysconfig/desktop file like this:

```
DISPLAYMANAGER="KDE"
```

The next time you reboot the system, the kdm display manager runs.

# GNOME display manager (gdm)

The gdm program is a display manager similar to xdm, the X display manager. Like xdm, gdm starts an X server for each local display, displays a login box, and enables the user to log in to the system.

When gdm runs, it reads various parameters from the configuration file /etc/X11/gdm/gdm.conf, which has a structure similar to a Windows IN file. For example, here are a few lines from a typical gdm.conf file:

```
[daemon]
AutomaticLoginEnable=false
AutomaticLogin-
TimedLogin=false
TimedLogin-
TimedLoginDelay=30
Gre=/usr/bin/gdmgreeting
lines deleted...
```

![](bbox=[0.125, 0.203, 0.215, 0.303])

![](bbox=[0.125, 0.413, 0.215, 0.513])