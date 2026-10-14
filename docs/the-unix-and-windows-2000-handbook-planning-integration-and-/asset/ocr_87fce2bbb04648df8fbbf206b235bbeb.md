| Variable | Value | Description |
|---|---|---|
| netbios name | Text | The name (no pun intended) really speaks for itself. This parameter specifies the name that the SAMBA server will advertise on the NetBIOS network. It is best to keep this name the same as your DNS hostname. |
| workgroup | Text | Indicates which NetBIOS network the SAMBA server will belong to. There is no option for domain name; this option covers both realms. |
| server string | Text | This is equivalent to the description of a Windows machine. Use this line to provide a more meaningful description of your SAMBA server. |
| browseable | yes/no | This sets the default browse option for all services. In a nutshell, this option determines whether or not a server is advertised to the network. We recommend setting this variable to yes. |
| hosts allow | Comma-separated list | Specifies a list of IP addresses (or subnets) that are allowed to access your SAMBA server. |
| hosts deny | Comma-separated list | Specifies a list of IP addresses (or subnets) that are NOT allowed to access your SAMBA server. |
| load printers | yes/no | Specifies whether or not the printers on your SAMBA server will be loaded when you start the SAMBA service. |
| printcap name | Pathname | Specifies where to find your printcap file to load the printers. |
| printing | AIX | BSD | HPUX | LPRNG | PLP | QNX | SOFTQ | SYSV | Specifies the type of printing system to use. The most common printing system is BSD. |
| log file | Pathname | Specifies a path to log Samba messages to. This is typically somewhere in the /var/log directory. |
| max log size | Number | Specifies how large the log file is allowed to be. |

# Table 8.10 SAMBA [global] Section Variables