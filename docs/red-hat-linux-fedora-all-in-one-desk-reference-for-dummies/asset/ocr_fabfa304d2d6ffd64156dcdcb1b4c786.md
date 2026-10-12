This creates the appropriate Samba configuration files in the /etc/samba directory and starts the Samba service. In particular, the file /etc/samba/smb.conf contains the configuration details for the Samba share you just created.

After adding a Samba share, type the following command to verify that the Samba configuration file is okay:

```
testparm
```

If the command says that it loaded the files okay, you're all set to go. The testparm command also displays the contents of the Samba configuration file.

![](bbox=[0.15, 0.42, 0.22, 0.55])

To start the SMB services automatically when the system reboots, type the following command:

```
chkconfig --level 35 smb on
```

# Trying out Samba

You can now try to access the Samba server on the Red Hat Linux system from one of the Windows systems on the LAN. Double-click the Network Neighborhood icon on the Windows 95/98/Me desktop. On Windows XP, choose Start→My Network Places and then click View Workgroup Computers. This should show all the computers on the same workgroup.

As you can see from the label (Figure 6-6), Lnblp1 is actually a Red Hat Linux system running Samba.

Figure 6-7:
You can view the Fedora Samba server from Windows XP.

![](bbox=[0.28, 0.68, 0.78, 0.86])