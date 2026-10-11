When the **prefdm** script is executed, as shown in the code, it looks (on Red Hat) at the /etc/sysconfig/desktop file for a preferred display manager. If that file is not found or configured, it tries in succession **gdm**, **kdm**, and **xdm** to try to load a display manager.

All the display managers get the login screen setup information from the /etc/X11/xdm/Xsetup_0 file, which also calls the **xresources** file for other setup information.

> **ALERT**  If you want to customize the login screen to include font choices, login prompt size, colors, welcome messages, and background graphics, these settings are made in the /etc/X11/xdm/Xresources file.

# # Tuning X

Several programs exist to help you get the most out of your display and monitor with X. These are typically included with X or are a package that's closely related to X.

For example, some monitors don't display the screen correctly, with part of the output being cut off, or off-center. To fix some of these problems, you can use the **xvidtune** command. Running **xvidtune** from within X shows the interface in Figure 7.3.

![](bbox=[0.091, 0.579, 0.578, 0.771])

**Figure 7.3**  The xvidtune program.

This program comes with some dire warnings, and with good reason. You can damage your monitor and when the tube goes, you will see (and smell) the “magic blue smoke” from the ruined tube. The best thing about the xvidtune program is that it tells you the display resolution and lets you adjust the image on your monitor to stretch properly from edge to edge and be centered properly.