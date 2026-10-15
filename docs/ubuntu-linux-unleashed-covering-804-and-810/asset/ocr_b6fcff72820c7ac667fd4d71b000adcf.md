![](bbox=[0.07, 0.11, 0.68, 0.68])

FIGURE 3.14 You configure kdm by choosing tabs and settings in the Login Manager dialog box.

To make any changes to the KDE display manager while logged in as a regular user, you must first click the Administrator Mode button, and then enter your password. You can click on a tab in the Login Manager dialog to set configuration options. Options in these tabs allow you to control the login display, prompts, user icons, session management, and configuration of system options (for shutting down or rebooting). After you make your configuration choices in each tab, click the Apply button to apply the changes immediately; otherwise, the changes are applied when the X server restarts.

# Using the xdm Display Manager

The xdm display manager is part of the Xorg distribution and offers a bare-bones login for using X. Although it is possible to configure xdm by editing various files under the /etc/X11/xdm directory, GNOME and KDE offer a greater variety of options in display manager settings. The default xdm login screen's display is handled by the xsetroot client, which is included with Xorg.

# Changing Window Managers

Ubuntu makes it fairly painless to switch to another window manager or desktop environment. By desktop environment, we refer to not only the window manager but also the suite of related applications such as productivity or configuration tools.