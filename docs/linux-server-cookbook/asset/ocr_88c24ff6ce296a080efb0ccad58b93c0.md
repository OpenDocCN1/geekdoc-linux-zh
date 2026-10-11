Samba server can be configured to use different authentication sources, such as **Lightweight Directory Access Protocol** (LDAP). Samba can also act as an **Active Directory Domain Controller**, providing DNS services and **Kerberos** authentication. This book only covers Samba as file sharing.

# ## Samba client

The Samba software suite includes different commands to act as a client for the protocol SMB. The most used command is **smbclient**, which is part of the package **samba-client** in RPM software repositories and the package **smbc1ient** on DEB software repositories. This command is used to access the connect to an SMB Service to access the resources. The command works in interactive mode unless the option **-L** (**--list**) is used. *Figure 10.11* and *10.12* shows the syntax and the different usages:

+   List the shared resources from the server 192.168.122.43, as shown in *figure 10.11*:

```
```
[root@rhel ~]# smbclient -L //192.168.122.43/ -U agonzalez
Password for [SMB\ agonza1ez]:
Sharename    Type    Comment
---------    ----    -------
print$       Disk    Printer Drivers
storage      Disk    Storage directory
public       Disk    Public directory
IPC$         IPC     IPC Service (ubuntu server (Samba, Ubuntu))
SMB1 disabled -- no workgroup available
```
```

*Figure 10.11:* *Example of usage of the command smbclient*

+   Access interactive to the Samba server and list the content of the *storage* directory, as shown in *figure 10.12*:

```
```
[root@rhel ~]# smbclient //192.168.122.43/storage/ -U agonzalez%Start123
Try "help" to get a list of possible commands.
smb: \> dir
       D    0 Sat Sep 10 21:17:56 2022
       D    0 Sat Sep 10 22:43:09 2022
       N    0 Sat Sep 10 21:17:56 2022  newfile
   11758760 blocks of size 1024. 5635424 blocks available
```
```

*Figure 10.12:* *Example of the usage of command smbclient*

It is possible to mount a remote *SMB* resource in a Linux system using the command **mount**. The command **mount**, when the type is **cifs** (or **smb3**), will