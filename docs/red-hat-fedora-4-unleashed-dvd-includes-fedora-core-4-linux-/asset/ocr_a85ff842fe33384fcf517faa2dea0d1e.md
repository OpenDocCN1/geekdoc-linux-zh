In the **Index** tab of the left pane of the KDE Control Center window, you click the **System Administration** menu item to open its contents, and then you click the **Login Manager** menu item. The right pane of the Control Center window displays the tabs and configuration options for the kdm Login Manager, as shown in Figure 6.6.

![](bbox=[0.12, 0.19, 0.84, 0.57])

**FIGURE 6.6**  You configure kdm by choosing tabs and settings in the Control Center dialog box.

In order to make any changes to the KDE display manager while logged in as a regular user, you must first click the **Administrator Mode** button, and then enter the root operator password. You can click on a tab in the Control Center dialog to set configuration options. Options in these tabs allow you to control the login display, prompts, user icons, session management, and configuration of system options (for shutting down or rebooting). After you have made your configuration choices in each tab, click the **Apply** button to apply the changes immediately; otherwise, the changes are applied when the X server restarts.

# Using the xdm Display Manager

The *xdm* display manager is part of the Xorg distribution and offers a bare-bones login for using X. Although it is possible to configure *xdm* by editing various files under the `/etc/X11/xdm` directory, GNOME and KDE offer a greater variety of options in display manager settings. The default *xdm* login screen’s display is handled by the `xsetroot` client, which is included with Xorg, and Owen Taylor’s *xsri* client, as specified in the file `xsetup_0` in the *xdm* directory under `/etc/X11`. The *xsri* client may be used to set the background color of the login display’s desktop and to place an image in the initial display.