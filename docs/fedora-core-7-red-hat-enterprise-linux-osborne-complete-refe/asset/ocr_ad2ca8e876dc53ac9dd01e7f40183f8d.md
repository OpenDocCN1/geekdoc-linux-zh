```
dns proxy = No
hosts allow = 192.168.0., 192.168.1., 192.168.2., 127.
cups options = raw

[homes]
    comment = Home Directories
    path = /home
    read only = No
    guest ok = Yes

[printers]
    comment = All Printers
    path = /var/spool/samba
    guest ok = Yes
    printable = Yes
    browseable = No

[myprojects]
    path = /myprojects
    read only = No
    guest ok = Yes

[myhp]
    path = /var/spool/samba
    read only = No
    guest ok = Yes
    printable = Yes
    printer = myhp
    oplocks = No
    share modes = No
```

> **TIP** *The **writeable** option is an alias for the inverse of the **read only** option. The **writeable = yes** entry is the same as **read only = no** entry.*

# Global Section

The Global section determines configuration for the entire server, as well as specifying default entries to be used in the home and directory segments. In this section, you find entries for the workgroup name, password configuration, and directory settings. Several of the more important entries are discussed here.

# Specifying the Workgroup and Server

The Workgroup entry specifies the workgroup name you want to give to your network. This is the workgroup name that appears on the Windows client’s Network Neighborhood window. The default Workgroup entry in the **smb.conf** file is shown here:

```
[global]

# workgroup = NT-Domain-Name or Workgroup-Name
workgroup = MYGROUP
```