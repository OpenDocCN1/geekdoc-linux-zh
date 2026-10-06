# Part IV: Fedora RHEL Network and Server Setup

```
comment = All Printers
path = /var/spool/samba
guest ok = yes
browse = no
writeable = no
printable = yes
```

The settings shown resulting from Configuring Samba from the Samba Configuration (System -> Administration -> Samba) window. You need to install the system-config-samba package to use the Samba Server Configuration window. In this case, I selected to use encrypted passwords. The lines show that printers from /etc/printcap were loaded and the CUPS service is being used. The /etc/samba/smbpasswd file stores the encrypted passwords. Because password sync is on, each user's Samba password is synchronized with the local UNIX password for the user.

The last few lines show here up the [printers] section, which determines the defaults for how printers are shared in Samba. The final line (printable = yes) defines that users can print to all printers.

# Summary

Sharing printers is an economical and efficient way to use your organization’s printing resources. A centrally located printer can make it easier to maintain a printer, while still allowing everyone to get his or her printing jobs done.

You configure your printer with the Printer configuration window. A variety of filters make it possible to print to different kinds of printers, as well as to printers that are connected to computers on the network.

The default printing service in Fedora and RHEL is the Common UNIX Printing Service (CUPS). Besides being able to set up your computer as a Linux print server, you can also have your computer emulate SMB (Windows) print server. After your network is configured properly and a local printer is installed, sharing printer over the network as a UNIX or SMB print server is not very complicated.