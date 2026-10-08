# 470 LINUX IN A HETEROGENEOUS NETWORK

Intensive use, however, may turn this situation into the opposite. If one computer is used by many users as a file and print server, reasonable interactive work on that computer is no longer possible. Since, for example, Windows for Workgroups has not been designed as a server operating system, problems will now occur with the maintenance of this computer, which is probably now standing in a locked room.

The SMB protocol is used by many products; besides the Windows family, the most widely used ones are LAN manager (by Microsoft and IBM) and Pathworks (by DEC). The SMB specificaton is now being enhanced to the Common Internet Filesystem (CIFS), which should address some of the SMB and NFS problems.

# 19.2.1 LINUX as an SMB client

If a workgroup or a domain already exists in your network, you can use LINUX to participate in this group. The smbfs file system required for this is implemented in the kernel. In addition, you will need the smbount program, which mounts the exported volume into the LINUX file system.

To set up the smbfs, you will need root privileges. Also, this file system is not portable to other systems. In exchange, the shares are integrated into the normal LINUX directory tree. For the user, it does not matter at all whether the files are stored locally, on an NFS server, or on an SMB server.

The samba package includes an SMB client (smclient) which is handled in a similar way to the ftp program. This program can be used without special privileges; help is obtained by the help command inside the program. On other UNIX systems, this is a simple way to access SMB shares. In contrast to LINUX's npcfs this does not provide seamless access.

The syntax of the shares name is exactly as under Windows: first two backslashes, the computer name, and separated by another backslash, the share name. Note, however, that you must quote the special characters of the shell (backslash) (Listing 19.8).

```
(Linux) >> smclient -L pea
(Linux) >> smclient \\pea\jochen
```

Listing 19.8 The use of smclient.

With the option -l, you will get a list of the shares available from this server (disks and printers). You can obtain access to these shares if you specify their names as in the second example.