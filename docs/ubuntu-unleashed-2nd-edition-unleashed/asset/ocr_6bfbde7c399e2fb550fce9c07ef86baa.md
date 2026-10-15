![](bbox=[0.064, 0.088, 0.754, 0.521])

**FIGURE 22.4**  Enter a Samba username and password in the SWAT Password page.

Click the Status icon (as shown in Figure 22.2 or 22.4) to view Samba’s status or to start, stop, or restart the server. You can use various buttons on the resulting web page to control the server and view periodic or continuous status updates.

You can also use SWAT to share a Linux directory. First, click the Shares icon in the toolbar at the top of the main Samba page (refer to Figure 22.2). Type a share name in the Create Shares field, and then click the Create Shares button. The SWAT Shares page displays the detailed configuration information in a dialog box, as shown in Figure 22.5, providing access to detailed configuration for the new Samba share.

Type the directory name (such as /music) you want to share in the Path field under the Base options. Select No or Yes in the Read Only field under Security options to allow or deny read and write access. Select Yes in the Guest OK option to allow access from other users and specify a hostname, IP address, or subnet in the Hosts Allow field to allow access. Click the Commit Changes button when finished. Remote users can then access the shared volume. This is how a Linux server running Samba can easily mimic shared volumes in a mixed computing environment!

Alternatively, use the shares-admin client (from the command line or the Server Settings Samba Server menu item on the System Settings menu). Figure 22.6 shows the properties of a shared directory named /music. Use the Add button to create new shares and the Properties button to edit the share’s access options.