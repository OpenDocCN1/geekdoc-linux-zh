for the Samba server and the clients on the LAN, the clients cannot see that the Samba server has directories or printers to share.

# ### Samba service running?

First, try the `smbclient` command from your Linux system to check that everything is running and being shared as you expect it to be. The `smbclient` command is a great tool for getting information about a Samba server and even accessing shared directories from both Linux and Windows computers. While logged in as root or any user who has access to your Samba server, type the following:

```
```
$ smbclient -L localhost
Password: ******
Domain=[ESTREET] OS=[Unix]  Server=[Samba  3.4.2-47.fc12]

Sharename       Type      Comment
---------       ----      -------
homes           Disk      Home Directories
IPC$            IPC       IPC Service (Samba Server)
ADMINS$         Disk      IPC Service (Samba Server)
hp-ns1          Printer

Domain=[ESTREET] OS=[Unix]  Server=[Samba  3.4.2-47.fc12]

Server          Comment
---------       -------
PINE            Samba Server
MAPLE           Windows XP
NS1             Samba Server

Workgroup       Master
---------       -------
ESTREET         PINE
```
```

This shows that the Samba server is running on the local computer. Shared directories and printers, as well as servers in the workgroup, appear here. If the Samba server is not running, you will see Connection refused messages. You need to start the Samba service as described in the “Starting the Samba service” section earlier in this chapter.

# ### Firewall or SELinux restricting access?

If the Samba server is running, it should begin broadcasting its availability on your LAN. If you try to access the server from a Windows or Linux client on your LAN, but get a Connection refused error, the problem may be that the firewall on your Linux Samba server is denying access to the NetBIOS service. If you have a secure LAN, you can type the following (as root user) to flush your firewall rules temporarily and set the default policy to Accept: