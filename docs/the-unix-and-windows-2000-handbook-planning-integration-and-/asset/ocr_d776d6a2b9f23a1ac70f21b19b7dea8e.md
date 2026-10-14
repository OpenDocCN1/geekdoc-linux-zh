# Table 8.11 SAMBA [homes] Section Variables

| Variable | Value | Description |
|---|---|---|
| comment | Text | Used to describe the service being offered. When used in the [homes] section, you should specify a generic phrase. |
| browseable | yes/no | Specifies whether or not this service is browseable on the NetBIOS network. |
| guest ok | yes/no | Specifies whether or not guests are allowed to access this share. When used in the homes section, we recommend that you set this to no. |
| writeable | yes/no | Specifies whether or not the share can be written to. Unless you only want users to see their home directory and not use it, specify yes for this parameter. |

# Table 8.12 SAMBA [printers] Section Variables

| Variable | Value | Description |
|---|---|---|
| comment | Text | Used to describe the service being offered. When used in the [printers] section, you should specify a generic phrase. |
| browseable | yes/no | Specifies whether or not this service is browseable on the NetBIOS network. |
| path | pathname | Specifies the path to spool documents to. This is usually somewhere in the /var/spool directory. |
| printable | yes/no | Specifies whether or not the printers can be printed to. Why create the share and then say, "No, you can't print, ha, ha." Always set this parameter to yes. |

```
# -------------------- Global Settings --------------------
[global]
netbios name = LILDIPPER
workgroup = COSMOS
server string = Samba %v Server

browseable = yes

hosts allow = 192.168.
hosts deny = 192.168.224.

load printers = yes
printcap name = /etc/printcap
printing = bsd
```