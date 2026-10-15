On SWAT, you can specify a guest account entry on the GLOBALS page. By default, this is already set to the nobody user.

# Passwords

As noted previously, user-level security requires that each user log into the Samba server using passwords. Samba can use either clear text or encrypted passwords, though current Windows clients support encrypted passwords. You can use the smbpasswd command to add and change Samba passwords. On SWAT, you can enable password encryption on the Globals page and manage passwords on the Passwords page. In the Server Password Management section, you can add, change, remove, enable, or disable users. To add a new user, enter the username and password, then click Add New User. As the root user on the Samba server, you can add new passwords as well as enable or disable current ones. Normal users can use the Client/Server Password Management section to change their own passwords.

# Homes Section

The Homes section specifies default controls for accessing a user home directory through the SMB protocols by remote users. To access the Homes section on SWAT, you simply select the SHARES page, select the Homes entry from the drop-down menu, and click Choose Share. Setting the browseable entry to no prevents the client from listing the files in a file browser. The writable entry specifies whether users have read and write control over files in their home directories. The create mode and directory mode set default permissions for new files and directories (on SWAT, these are create mask and directory mask). The valid user entry uses the %S macro to map to the current service.

```
[homes]
comment = Home Directories
browseable = no
writable = yes
valid users = %S
create mode = yes
directory mode = 775
```

# Printer Section

The Printers section specifies the default controls for accessing printers. These are used for printers for which no specific sections exist. In this case, Samba uses printers defined in the server’s printcap file.

In this context, setting browseable to no simply hides the Printers section from the client, not the printers. The path entry specifies the location of the spool directory Samba will use for printer files. To enable printing at all, the Printable entry must be set to yes. To allow guest users to print, set the guest ok entry to Yes. The writable entry set to no prevents any kind of write access, other than the printer’s management of spool files. On SWAT, select the PRINTER page and the Printers entry in the drop-down menu, and then select Choose Printers. A standard implementation of the Printers section is shown here:

```
[printers]
comment = All Printers
path = /var/spool/samba
```