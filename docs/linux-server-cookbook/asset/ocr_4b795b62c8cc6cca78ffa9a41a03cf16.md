```
[agonzalez@rhel exported]$ groups
nfsusers wheel agonzalez
[agonzalez@rhel exported]$ ls -ld /exported/
drwxrwx---. 2 root nfsusers 4096 Sep 10 21:17 /exported/
[agonzalez@rhel exported]$ touch newfile
[agonzalez@rhel exported]$ ls -l
total 0
-rw-r--r--. 1 agonzalez nfsusers 0 Sep 10 21:17 newfile
```

![](bbox=[0.31, 0.27, 0.67, 0.29])

The syntax for the file `/etc/fstab` is the following for an NFS share:

```
server:/directory /mntpoint nfs4 rw 0 0
```

# SMB introduction

The protocol **Server Message Block (SMB)** was originally developed in 1983 and provided shared access to files and printers in the network. Microsoft published version 1.0 of the protocol with some modifications, with the name **Common Internet File System (CIFS)**, in 1996. This proposal was never accepted, and Microsoft discounted the use of CIFS and continued developing new versions of SMB. The protocol SMB uses port 445 on protocol TCP and port 139, as well TCP, for communication over NetBIOS.

Similar to NFS, the SMB protocol has different protocol versions, which were introduced to different versions of Windows. Version 2.0 was introduced in the year 2006 on Windows Vista and Windows server 2008, publishing the specifications allowing interoperate with other systems. Version 2.1 was introduced in Windows 7 and Windows 2008 R2. Version 3.0 of the protocol was introduced with Windows 8 and Windows Server 2012. New versions are 3.0.2 and 3.11, included in the latest versions of the Windows and Windows Server.

# Samba server and client

The specifications for the protocol SMB are proprietary and were closed in the beginning. With version 2.0, the protocol was made available, allowing developers to create software to interoperate with the protocol and the Windows systems.

In the year 1991, a project called **Samba** started to implement a solution for SMB/CIFS for Unix systems, which, years later, came to be a popular project