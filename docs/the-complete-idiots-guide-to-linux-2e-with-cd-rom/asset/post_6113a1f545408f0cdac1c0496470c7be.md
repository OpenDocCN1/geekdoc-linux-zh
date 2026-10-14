
1       samba
1       test_project

In this example, all home directories are summarized.

## Finding the Amount of Free Disk Space: df

To find the amount of disk space to devices available in your system, use the df (disk free) command, as shown in the following:

```
[root@digital /home]# df
Filesystem           1024-blocks   Used Available Capacity Mounted on
/dev/hda1             686892  606189    45223      93% /
```

The command produces a nice table specifying how much space is available. Numbers are expressed in kilobytes.

In UNIX/Linux, just because there’s free space doesn’t mean that you can create files. If the file system’s inode table fills up (unlikely, but possible if a disk holds a great deal of tiny files), your system would be unable to create additional files. To see how you are doing on inodes, provide the -i option to df:

```
[root@digital /home]# df -i
Filesystem     Inodes   IUsed   IFree %IUsed Mounted on
/dev/hda1       177480   34971  142509    20% /
```

If you compare the regular df output, you’ll see that under normal circumstances, there are plenty of inodes left. On my disk, I have used 93% of my disk, yet only 20% of the inodes.

## Log Files

Many of the programs that run in the background, Web server, email, FTP, and so on generate logs for errors or just as a record of someone accessing it. This type of information is recorded, for example, every time a user logs in or out of the system.

## Monitoring Logins: last

Linux keeps very good track of users and their logins. This information is particularly useful when you are in a networked environment, and as a security precaution, you check to make sure that no “weird” traffic is going on in your machine.

By default, Linux is set up to keep track of logins and logouts. You can browse the login record using the last command.

To filter output to a specific user, provide the username as an argument to last:

```
[alberto@digital log]$ last alberto
alberto  tty p0     192.168.0.3   Fri Oct  2 18:32   still logged in
alberto  tty p0     192.168.0.3   Fri Oct  2 18:29 - 18:32
alberto  tty2       192.168.0.3   Fri Oct  2 15:20 - 17:01   (01:40)
alberto  tty p1     192.168.0.3   Fri Oct  2 14:55 - down     (03:32)
alberto  ftp       192.168.0.3   Fri Oct  2 13:41 - 13:42   (00:00)
alberto  ftp       192.168.0.3   Fri Oct  2 13:12 - 13:28   (00:16)
alberto  tty1       Fri Oct  2 13:02 - down     (05:25)
alberto  tty1       Wed Sep 30 17:41 - down     (00:18)
alberto  tty1       Tue Sep 29 11:10 - down     (00:10)
alberto  tty1       Mon Sep 28 17:36 - down     (00:47)
```

The last command prints the username, the terminal used to access the system, where the user came from (IP address) if the login was remote, and the date and duration of the session.

If the log file /var/log/wtmp doesn’t exist in your system, the system will not keep track of login information. To enable (or disable) this feature, just create or delete this file.

## Monitoring Bad Logins: lastb

The lastb command keeps track of bad (unsuccessful) logins. To enable bad login accounting, as root create the file /var/log/btmp. You can do this using the touch command (touch /var/log/btmp).

To review bad logins, use the lastb command. Unfortunately, Caldera OpenLinux doesn’t currently support lastb use.

If an account has an unusual number of bad logins, it is possible that the account is under attack by someone. Such accounts should be disabled and the user owning the account should be notified.

## Disabling an Account

The easiest way to disable an account is to put an asterisk (*) before the encrypted password in the /etc/passwd file. (The password is the second field in /etc/passwd.) Fields are separated by colons (:), like this:

```
me:*Ms.7kvaAYyHbU:500:100:Me:/home/me:/bin/sh
```

If you are using shadow passwords, the easiest way to disable an account is to use usermod and expire it with a date in the past:

```
usermod -e MM/DD/YY login
[root@digital alberto]# usermod -e 09/01/98 me
```

(Usermod is introduced in Chapter 18. "Users, Groups, and Passwords.")

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Chapter 23
Sharing Files over the Network

## In This Chapter

- The Network File System
- Using the mount and umount Commands
- Navigating the File System with FTP
- Uploading and Downloading Files
- Controlling File Access

Sharing files over the network allows you to collaborate more easily with others. Linux has the capability to provide file-sharing services in many ways. You can also be a client to almost all popular network file-sharing schemes.

The most popular ways for sharing files under UNIX are FTP (File Transfer Protocol), NFS (Network File System), and HTTP (the Web). Other protocols, such as Gopher, have given way to Web counterparts. Windows-based PCs share files using the SMB (Server Message Block) protocol. Linux can easily be a client to an SMB server and provides you with an FTP-like interface to a server.

If the information here should awaken your interest, feel free to read the online documentation (see Chapter 15, “Help Please”). Accessing a service (being a client) is easy. Setting up a server is slightly (a few orders of magnitude) more complicated, and entire books have been written on the various subjects. Given

the limited space, I have covered what I consider the least you should need to know to publish data and to access data from other servers.

## NFS

The NFS is how you share files between UNIX-based machines. Originally developed by Sun, NFS is very flexible and could be used to share information between networks. However, exporting directories to networks outside your control requires careful security considerations. By design, NFS was not intended for sharing across the Internet, but given today’s high-speed communication networks, it is feasible to share files over the Net.

NFS allows a directory tree to be grafted into the file system by other computers on the network in much the same way you mount a floppy disk or CD-ROM.

One issue with NFS is that file system security is based on the same mechanism your local file system uses: User IDs (UIDs) and Group IDs (GIDs) of files. If the UID of a user accessing a remote NFS volume doesn’t match the user’s own, the user will lack the necessary privileges. This means that in order to use NFS effectively, there needs to be a mechanism that shares login and password information. Luckily, such a system does exist; it is called NIS (Network Information Services). A long time ago, NIS was called Yellow-Pages. Configuring NIS and NFS requires more depth of information than a few paragraphs can offer. This section will only show you how to export and import an NFS volume. For in-depth configuring information, you should consult the online documentation and how-to guides and perhaps even acquire a book on NIS and NFS. Linux implementation is fairly standard, and you should have no problem adapting that information to your system.

## Exporting an NFS Volume

Before you can export NFS volumes, you’ll need to enable the NFS Server services in your computer. This is done through LISA under Configure daemon/server autostart under the System Configuration area; then you’ll need to reboot your computer. LISA, as you learned in Chapter 21, “LISA: Linux Installation and System Administration Utility,” is a command line program that manages your hardware and software configuration for the more important portions of your system.

With NFS, you don’t need to export an entire disk volume; a directory of your choosing will suffice. To export a directory, you merely need to edit the file /etc/exports. When you export a directory, you choose how you make it available and the permissions that others may have on the volume. Typically, unless you know what you are doing, you should just export the volume read-only. This way, users can see and access files, but they won’t be able to modify or delete files.

```
/share   (ro,insecure,all_squash)
```

In the entry shown, /share is exported with several options; here’s what they
