
# Date: 2001/09/09 01:09:07
# Global parameters
[global]
    server string = Samba Server
    security = SHARE
    encrypt passwords = Yes
    ssl CA certFile = /usr/share/ssl/certs/ca-bundle.crt
    log file = /var/log/samba/%m.log
    max log size = 0
    socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192
    dns proxy = No
    printing = cups

[homes]
    comment = Home Directories
    path = /home
    writeable = Yes
    guest ok = Yes

[printers]
    comment = All Printers
    path = /var/spool/samba
    guest ok = Yes
    printable = Yes
    browseable = No

[myprojects]
    path = /myprojects
    writeable = Yes
    guest ok = Yes

[myhp]
    path = /var/spool/samba
    writeable = Yes
    guest ok = Yes
    printable = Yes
    printer = myhp
    oplocks = No
    share modes = No

## Global Section

The Global section determines configuration for the entire server, as well as specifying default entries to be used in the home and directory segments. In this section, you find entries for the workgroup name, password configuration, and directory settings. Several of the more important entries are discussed here. Figure 37-4 shows the Global Variables page on the SWAT that you can use to set global options. The Basic View of this page lists the options you would most likely need.

## Global Variables

![](img/6c226e8ba1efd427dec3bf582418d33f_773_0.png)

### FIGURE 37-4 SWAT Global Variables page

## Specifying the Workgroup and Server

The Workgroup entry specifies the workgroup name you want to give to your network. This is the workgroup name that appears on the Windows client’s Network Neighborhood window. The default Workgroup entry in the smb.conf file is shown here:

```
[global]
# workgroup = NT-Domain-Name or Workgroup-Name
workgroup = MYGROUP
```

The workgroup name has to be the same for each Windows client that the Samba server supports. On a Windows client, the workgroup name is usually found on the Network Identification or General panel in the System tool located in the Control Panel window. On many clients, this is defaulted to WORKGROUP. If you want to keep this name, you would have to change the Workgroup entry in the smb.conf file accordingly. The Workgroup entry and the workgroup name on each Windows client have to be the same.

```
workgroup = WORKGROUP
```

The server string entry holds the descriptive name you want displayed for the server on the client systems. On Windows systems, this is the name displayed on the Samba server icon. The default is Samba Server, but you can change this to any name you want.

```
# server string is the equivalent of the NT Description field
server string = Samba Server
```

## Security Level

Samba resources are normally accessed with either share- or user-level security. On a share level, any user can access the resource without having to log into the server. On a user level, each user has to log in, using a password. Furthermore, Windows 98, ME, NT, and XP clients use encrypted passwords for the login process. You will have to enable encrypted passwords for these clients. The default for encrypted passwords is no, so you will need to change it to yes. In the smb.conf file, the security option is set to the level you want and the encrypt passwords option is set to yes to enable encryption.

```
security = user
encrypt passwords = yes
```

If you want share-level security, specify share as the security option:

```
security = share
```

On the SWAT Globals page, select the security level from the Security pop-up menu, either User or Share. Then select Yes for the encrypt passwords entry.

## Network Access Control

As a security measure, you can restrict access to SMB services to certain specified local networks. On the host's network, type the network addresses of the local networks for which you want to permit access. To deny access to everyone in a network except a few particular hosts, you can use the EXCEPT option after the network address with the IP addresses of those hosts. The localhost (127) is always automatically included. The next example allows access to two local networks:

```
hosts allow = 192.168.1. 192.168.2.
```

## Printing

To enable printing, allow Samba to load the printer descriptions from your printcap file.

```
printcap name = /etc/printcap
load printers = yes
```

To specify your printing system, you set the printing option. On Red Hat, CUPS is the print server now supported. To set the printing system to CUPS, use the following:

```
printing = cups
```

## Guest User Access

You can use a guest user login to make resources available to anyone without requiring a password. A guest user login would handle any users who log in without a specific account. On Linux systems, by default Samba will use the nobody user as the guest user. Alternatively, you can set up and designate a specific user to use as the guest user. You designate the guest user with the Guest Account entry in the smb.conf file. The commented smb.conf file provided with Samba currently lists a commented entry for setting up a guest user called pcguest. You can make this the user you want to be used as the guest user. Be sure to add the guest user to the password file:

```
guest account = pcguest
```
