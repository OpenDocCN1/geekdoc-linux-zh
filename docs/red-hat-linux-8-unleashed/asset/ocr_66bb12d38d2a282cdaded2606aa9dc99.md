# Putting Samba to Work

![](bbox=[0.183, 0.098, 0.812, 0.458])

FIGURE 1.37 Enter a Samba username and password in the SWAT page.

For example, if you have set up Samba on a hosted shuttle2 that has a user sprice, the user will be able to access the home directory on shuttle2 from any remote host (if allowed by the GLOBALS settings), by perhaps using the smbclient like so:

```
$ smbclient //shuttle2 -U sprice
added interface ip=192.168.2.68 bcast=192.168.2.255 nmask=255.255.255.255
Password:
Domain=[MYGROUP] OS=[Unix] Server=[Samba 2.2.5]
smb: \> pwd
Currentirect directory is \shuttle2\sprice\
smb: \> quit
```

If you need to start, stop, or restart Samba, click the Status button. You'll see the Server Status dialog box, as shown in Figure 13.8.

Click the Start smbd or Restart smbd buttons to control Samba. Active connections or shares in use will be displayed by the buttons. The view is updated every 30 seconds by default, you can either click your browser's Reload button to see an update or the Auto Refresh button to get continuous updates.

You can also use SWAT to share a Linux directory. First, click the Shares button in the toolbar at the top of the main Samba page, Type a share name in the Create Shares field, and then click the Create Shares button. The SWAT page will display the detailed configuration information, a dialog as shown in Figure 13.9, providing access to detailed configuration for the new Samba share.