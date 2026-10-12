You can specify settings for security, remote network logins, the X server, and session and session chooser setup by clicking on the tabs in the GDM Setup dialog.

# Configuring kdm

The kdm client, which is part of the KDE X desktop suite, offers a graphical login similar to gdm. You configure kdm by running the KDE Control Center client kcontrol, as the root operator, by clicking the Control Center menu item from the KDE kicker or desktop panel menu. You can also start KDE Control Center by using the kcontrol client at the command line like so:

```
$ kcontrol &
```

In the Index tab of the left pane of the KDE Control Center window, you click the System Administration menu item to open its contents, and then you click the Login Manager menu item. The right pane of the Control Center window displays the tabs and configuration options for the kdm Login Manager, as shown in Figure 6.6.

![](bbox=[0.14, 0.4, 0.79, 0.74])

**FIGURE 6.6** You configure kdm by choosing tabs and settings in the Control Center dialog box.

To make any changes to the KDE display manager while logged in as a regular user, you must first click the Administrator Mode button, and then enter the root operator password. You can click on a tab in the Control Center dialog to set configuration options. Options in these tabs allow you to control the login display, prompts, user icons, session management, and configuration of system options (for shutting down or rebooting). After you make your configuration choices in each tab, click the Apply button to apply the changes immediately; otherwise, the changes are applied when the X server restarts.