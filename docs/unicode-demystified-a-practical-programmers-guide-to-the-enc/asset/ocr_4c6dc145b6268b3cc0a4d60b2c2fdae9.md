Click Your RHN, Entitlements, and then the Service Entitlements tab. You should see your profilename in the Name column toward the bottom of the frame. Use the drop down list in the Entitled column to select Basic for your system. Click Update Entitlements.

+   * Check for updates. Run update2, or choose Red Hat Network Alert Notification Icon menu: Check for updates (page 939) to see if the RHN server downloads files or exchanges information with your system. You can also give the command update2 --list to see whether any packages are available for your system, thereby testing your connection with the RHN server.

You can start the flow of updates from your system or from the Web Site. From your system log in, click Systems>Systems List>Detailed view, click UPDATE NOW on the line with profile on it, and click Confirm Update For This System. In this case the next time the rhnsd daemon on your system contacts the RHN server, you will get updates per the RHN system profile (installed or not, left on the system or source code or not, and so on).

# Red Hat Network Alert Notification Tool

The Red Hat Network Alert Notification Tool can take care of everything you need to set up, run, and administer your RHN account. The Red Hat Network Alert Notification Tool is represented by a round button on both the GNOME and KDE Main panel. It shows one of four icons:

+   * Blue with a check mark indicates that all is well: There are no pending downloads.
* Red with an exclamation point indicates that files need to be downloaded. Click the button.
* Green with half arrows pointing left and right indicates that the system is communicating with the RHN server.
* Grey with a question mark indicates that there has been an error. Click the icon to display the error message.

If the button is not on the Main panel, run rhn-alert-gui from Run Program on the GNOME menu or Run Command on the K menu to display it. Table 17-5 describes the selections on the Red Hat Network Alert Notification Tool panel icon (right click),