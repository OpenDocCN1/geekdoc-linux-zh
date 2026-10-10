won't be able to see that information. For example, you could create a file named `/etc/samba/creds.smbpub` containing the following two lines:

```
username=chris
password=a72mg
```

You could then change the mount command shown earlier to appear as follows:

```
# mount -t cifs -o credentials=/etc/samba/creds.smbpub //toys/chris
```

# Using Samba shared directories from Windows

While using a Windows system, to see the file and print services available from your Linux Samba server (as well as from other computers on the network), open the Network and Sharing Center window in Windows Vista. Selections at the bottom of that window enable you to see all the files and folders you and others are sharing.

For other Windows systems, open the My Network Places window (for Windows XP) or Network Neighborhood (Windows 98 and older Windows systems). To open the window, select Start $\rightarrow$ My Network Places from the Windows XP desktop. Figure 17-6 shows an example of the My Network Places window with shares available from the local Windows XP system (named Bluestreak) and the Samba server in Linux (named Waldo).

![](bbox=[0.12, 0.45, 0.83, 0.78])

**Figure 17-6:** View your Linux Samba server from the My Network Places window.

The My Network Places window shows the computers that Windows found on your network. If your server appears on the screen (in my case, the server's name is Waldo), double-click it. Otherwise, you may need to double-click Entire Network, and then open the workgroup that your server is a part of to find your server. The server should show two kinds of resources: