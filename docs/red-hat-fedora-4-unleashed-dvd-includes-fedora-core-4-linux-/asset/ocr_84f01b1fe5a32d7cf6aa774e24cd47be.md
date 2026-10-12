![](bbox=[0.14, 0.08, 0.85, 0.48])

FIGURE 21.4 Enter a Samba username and password in the SWAT Password page.

For example, if you have set up Samba on a host named shuttle2 that has a user named spice, the user can access the home directory on shuttle2 from any remote host (if allowed by the GLOBALS settings), perhaps by using the smbclient command like so:

```
$ smbclient //shuttle2/spice -U spice
added interface ip=192.168.2.68 bcast=192.168.2.255 nmask=255.255.255.0
Password:
Domain=[MYGROUP] OS=[Unix] Server=[Samba 2.2.5]
smb: \> pwd
Current directory is \\shuttle2\spice\
smb: \> quit
```

Click the Status icon (as shown in Figure 21.2 or 21.4) to view Samba's status or to start, stop, or restart the server. You can use various buttons on the resulting web page to control the server and view periodic or continuous status updates.

You can also use SWAT to share a Linux directory. First, click the Shares icon in the toolbar at the top of the main Samba page (refer to Figure 21.2). Type a share name in the Create Shares field, and then click the Create Shares button. The SWAT page displays the detailed configuration information in a dialog box as shown in Figure 21.5, providing access to detailed configuration for the new Samba share.