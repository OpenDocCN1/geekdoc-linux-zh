# **Example 33.1.1 Elastic smb.conf File**

```
# Global parameters
[global]
    workgroup = ROBINNEST
    netbios name = ELASTIC
    netbios aliases = CDSERVER
    smb ports = 139
    printcap name = cups
    disable spoolss = Yes
    show add printer wizard = No
    printing = cups
    include = /etc/samba/smb-%L.conf

[homes]
    comment = Home Directories
    valid users = %S
    read only = No
    browseable = No

[office]
    comment = Data
    path = /data
    read only = No

[printers]
    comment = All Printers
    path = /var/spool/samba
    create mask = 0600
    guest ok = Yes
    printable = Yes
    use client driver = Yes
    browseable = No
```

# **Example 33.1.2 CDROM Server smb-cdserver.conf file**

```
# Global parameters
[global]
    workgroup = ARTSDEPT
    netbios name = CDSERVER
    map to guest = Bad User
    guest ok = Yes

[carousel]
    comment = CDROM Share
    path = /export/cddata
    read only = Yes
    guest ok = Yes
```