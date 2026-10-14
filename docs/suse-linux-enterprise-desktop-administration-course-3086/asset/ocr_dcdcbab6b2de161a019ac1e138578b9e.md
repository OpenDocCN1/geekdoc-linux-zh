Double-click on one of the servers and then on one of the shares to open the dialog shown in Figure 13-11.

![](bbox=[0.126, 0.134, 0.484, 0.354])

Figure 13-11

Enter a username and password to access the share.

# Use Nautilus to Share Directories Using Samba

For users to be able to share folders with others using the SMB protocol, Samba needs to run on the computer and the Samba configuration has to permit users to share directories. The following lines are needed in the Global section of the /etc/samba/smb.conf file:

```
usershare allow guests = yes
usershare max shares = 50
usershare path = /var/lib/samba/usershare
```

The first line allows access to the shares without a password.
The second line limits the number of shares that can be created.
The third line specifies the directory where Samba stores the information on shared directories. The directory specified in the configuration file has to exist and needs to be writable for the users who are allowed to share directories. The following commands create the directory, change the owning group, and set the proper permissions for the directory:

```
da10:~ # mkdir /var/lib/samba/usershares
da10:~ # chgrp users /var/lib/samba/usershares
da10:~ # chmod 1770 /var/lib/samba/usershares
```

To start Samba, enter rcnmb start; rcsmb start. To have Samba start at system start, enter insserv nmb and insserv smb.