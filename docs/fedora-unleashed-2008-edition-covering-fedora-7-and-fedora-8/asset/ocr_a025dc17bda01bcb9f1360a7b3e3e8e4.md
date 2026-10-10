# TIP

LPNg, like CUPS, can be configured to restrict print services to single hosts, one or more specific local or remote users, all or part of a domain, or a LAN segment (if you specify an IP address range). An entry in `/etc/lpd.perms`, for example, to allow print requests only from hosts on 192.168.2.0, would look like this:

ACCEPT SERVICE=x REMOTEIP=192.168.2.0/255.255.255.0

The `lpd.perms` man page (included as part of the LPNg documentation) contains an index of keywords you can use to craft custom permissions. Don’t forget to restart the `lpd` daemon after making any changes to `/etc/lpd.perms` (or `/etc/lpd.conf`).

If the computer with an attached printer is using Fedora and you want to set up the system for print serving, again use the `system-config-printer` client. You can create a new printer, but the easiest approach is to publish details of your printer across the network.

To enable sharing, start `system-config-printer`, and then select the Server Settings option in the left pane. All you need to do is select **Share Published Printers Connected to This System** to automatically allow access to all your printers, as shown in Figure 19.9.

![](bbox=[0.08, 0.5, 0.9, 0.76])

FIGURE 19.9 Sharing enables you to offer a locally attached printer as a remote printer on your network.

By default, all users are allowed access to the printer. You can change this setting by selecting the Access Control tab and adding users into the list.