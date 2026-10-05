change the look of your desktop, its color scheme, or its handling of windows. For details
other about ways to configure AfterStep, read its FAQ or browse to http://www.
afterstep.org.

# # The fwm Window Manager

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window
manager but has several advantages, such as using less memory, supporting fancier window
decorations, and providing virtual desktops.

**Figure 5.3
The fwm window manager is an improvement over
The XII's twm window manager.

![](bbox=[0.243, 0.323, 0.833, 0.583])

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is
name system. .fwmrc. Copy this file to your home directory .fwmrc and make
changes to customize it for your use. fwm startup file contains sections for customizing
window colors and style, menus, and the number of virtual desktops. Look for the desktop
section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different
desktop by pressing your left mouse button on the appropriate square in the desktop pager's