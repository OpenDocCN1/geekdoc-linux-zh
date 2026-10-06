# Chapter 18: Setting Up a File Server 793

You then need to open ports 137, 138, and 139 in your firewall so that the Samba server will be able to accept connections for services. (See Chapter 14 for information on modifying your firewalls.)

# User passwords working?

Try accessing a shared Samba directory as a particular user (from the local host or other Linux system on your LAN). You can use the smclient command to do this. Here's an example:

```
# smclient //localhost/home/chris/files -U chris
added interface ip=10.0.0.1 bcast=10.0.0.255 mask=255.255.255.0
Password: ********
Domain=[ESTREE] Server=[Samba 3.2.4]
smb:\>
```

In this example, smclient connects to the directory named tmp as the Samba user chris. If the password is accepted, you should see information about the server and a smb:\> If you cannot access the shared directory from a Windows client, it's possible that the client is using an improper user name and password. Part of the problem may be that the Windows client is not providing encrypted passwords.

For Windows clients, using encrypted passwords requires that you change a Windows registry for the machine. One way to change the registry is with the Windowsedit command. Registry changes required for different systems are contained within the /usr/share/doc/samba-*/docs/registry directory.

> TIP: The smclient command, used to list server information and test passwords, can also be used to browse the shared directory and copy files after you are connected. After you see the smb:\> prompt, type help to see the available commands. The interface is similar to any ftp client, such as sftp.

# Summary

By providing centralized file services, an organization can efficiently share information and applications with people within the organization, with customers, or with anyone around the world. Different technologies are available in Fedora and RHEL to enable you to make your Linux file server.

The Network File System (NFS) protocol was one of the first file server technologies available. It is particularly suited for sharing file systems among Fedora, RHEL, and UNIX systems. NFS uses standard mount and umount commands to connect file systems to the directory structures of client computers.

The Samba software package that comes with Fedora and RHEL contains protocols and utilities for sharing files and printers among Windows and OS/2 operating systems. It uses SMB protocols that are included with Microsoft Windows systems, and therefore provide a convenient method of sharing resources on LANs containing many Windows systems.