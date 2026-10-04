
# 694 Configuring DNS

If you want to use dig to check the DNS server, type the following command:

```bash
dig @localhost wpx.naba.net
```

That @localhost part specifies the DNS server that dig contacts.

When you successfully use dig to contact a DNS server, you can get a bit fancier with what you ask that server to do. Here, for example, is the command I type to try a reverse lookup with the IP address 192.168.0.2:

```
host 192.168.0.2 localhost
```

This command displays the following output:

+   Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:

```
2.0.168.192.in-addr.arpa domain name wpx.naba.net
```

# # Chapter 6: Running Samba and NFS

In This Chapter

- Sharing files with NFS
- Using the NFS Server Configuration tour
- Installing and configuring Samba
- Setting up a Windows server using Samba

Your local area network is like many others, it needs the capability to share files between systems that run Linux and other systems that don't. This Fedora Core includes two prominent file-sharing services:

- Network File System (NFS) is for sharing files with other UNIX systems (or PCs with NFS client software)
- Samba is for file sharing and print sharing with Windows systems.

In this chapter, I describe how to share files using NFS and Samba.

## ## Sharing Files with NFS

Sharing files through NFS is simple and involves two basic steps:

- On the Fedora Core system that runs the NFS server, you export (share) one or more directories by listing them in the /etc/exports file and running the exports command. In addition, you must run the NFS server by logging in root and typing the command service nfs start.
- On each client system, you use the mount command to direct the directories that your server has exported.

The only problem in using NFS is that each client system must support it. Microsoft Windows doesn't come with NFS. That means you have to buy NFS software separately if you want to share files by using NFS. However, using NFS if all systems on your LAN run Linux (or other variants of UNIX) with built-in NFS support makes sense.

# 696 Sharing Files with NFS

> Note: NFS has security vulnerabilities. Do not set up NFS on systems directly connected to the Internet.

In the next sections, I walk you through NFS setup, using an example of two Fedora Core PCs on a LAN.

# Exporting a file system with NFS

Start with the server system that exports — makes available to the client systems — the contents of a directory. On the server, you must run the NFS service and designate one or more file systems to export — made available to the client.

To export a file system, you need to add an appropriate entry to the /exports file. For example, suppose you want to export the /home directory and you want to enable the host named LNBP75 to mount this file system for read and write operations. You can do so by adding the following entry to the /etc/exports file:

```bash
/home LNBP75(rw,sync)
```

If you want to grant access to all hosts on a LAN such as 192.168.0.0, you could change this line to

```bash
/192.168.0.0/24(rw,sync)
```

Every line in the /etc/exports file has this general format:

```
directory host1(options) host2(options) ...
```

The first field is the directory shared via NFS, followed by one or more fields that specify which hosts can mount that directory remotely and a number of options within parentheses. You can specify the hosts with names or IP addresses, including ranges of addresses.

The options within parentheses denote the kind of access each host is granted and user group IDs from the server are mapped to ID the client (for example, if a file is owned by root on the server, what owner is that on the client?). Within parentheses, commas separate the options. For example, if a host is allowed both read and write access — and all IDs are to mapped to the anonymous user (by default this is the user named nobody) — then the options look like this:

```
(rw,all_squash)
```

Table 6-1 shows the options you can use in the /etc/exports file. You find two types of options — general options and user ID mapping options.

# Sharing Files with NFS 697

| Table 6-1 Options in /etc/exports |
| This Option | Does the Following |
| :--- | :--- |
| General secure | Allows connections from only ports 1024 or lower (default). |
| insecure | Allows connections from 1024 or higher. |
| ro | Allows read-only access (default). |
| rw | Allows both read and write access. |
| sync | Performs write operations (writing information to the disk) when requested (default). |
| async | Performs write operations when the server is ready. |
| no_delay | Performs write operations immediately. |
| hide | Hides an exported directory that is a subdirectory of another exported directory (by default). |
| no_hide | Behaves the opposite of hide. |
| subtree_check | Performs subtree checking, which involves checking parent directories of an exported sub उभ whenever a file is accessed (by default). |
| no_subtree_check | Turns off subtree checking (opposite of subtree_check). |
| insecure_locks | Allows infuse locking. |
| User ID Options all_squash | Maps all user IDs and group IDs to the anonymous user on the client. |
| no_all_squash | Maps remote user and group IDs to similar IDs on the client (by default). |
| root_squash | Maps remote root to the anonymous user on the client (by default). |
| no_root_squash | Maps remote root to the local root user. |
| anuid=UID | Sets the user ID of anonymous user to be used for the all_squash and root_squash options. |
| angid=GID | Sets the group ID of anonymous user to be used for the all_squash and root_squash options. |

After adding the entry in the /etc/exports file, manually export the file system by typing the following command in a terminal window:

```bash
exportfs -a
```

This command exports all file systems defined in the /etc/exports file.

# 698 Sharing Files with NFS

Now you can start the NFS server processes. To do so, log in as root and type the following command in a terminal window:

```bash
service nfs start
```

If you want the NFS server to start when the system boots, type the follow-command to turn it on:

```bash
chkconfig --level 35 nfs on
```

When the NFS service is up, the server side of NFS is ready. Now you can try to mount the exported file system from a client system, and access the exported file system as needed.

If you ever make changes to the exported file systems listed in the /etc/exports file, remember to restart the NFS service. Do so, log in as root and type the following command in a terminal window:

```bash
service nfs restart
```

# Mounting an NFS file system

To access an exported file system on a client system, you have to mount file system on a mount point. The mount point is nothing more than a local directory. For example, suppose you want to access the /home directory exported from the server named LNBP200 at the local directory /mnt/lnbp200 on the client system. To do so, follow these steps:

- 1. Log in as root and create the directory with this command:

```bash
mkdir /mnt/lnbp200
```

- 2. Type the following command to mount the directory from the remote system (LNBP200) on the local directory /mnt/lnbp200:

```bash
mount lnbp200:/home /mnt/lnbp200
```

After these steps, you can view and access exported files from the local directory /mnt/lnbp200.

To confirm that the NFS file system is indeed mounted, log in as root on the client system and type mount in a terminal window. You see a line similar to the following about the NFS file system:

```
lnbp200:home on /mnt/lnbp200 type nfs (rw,addr=192.168.0.4)
```

# Using the NFS Configuration tool

Fedora Core comes with a graphical NFS Server Configuration tool that makes configuring and starting the NFS server easy. To configure the NFS server using this tool, follow these steps:

- 1. Log in as root and choose Main Menu: System Settings->Settings:NFS from the GNOME or KDE desktop.

The NFS Server Configuration window appears.

- 2. Click Add to the toolbar.

The Add NFS Share dialog box appears.

- 3. Add the directories you want to share via NFS.

Start by specifying the directory, which has access to it (the hosts or IP addresses), and what type of access (read-only or read-write). Figure 6-1 shows the settings for the /home directory being shared with read-write access all hosts in the 192.168.0.0 network.

- 4. Click the General Options tab in the Add NFS Share dialog box and set the options you want (as shown in Figure 6-2).

These options correspond to the options listed in the General Options section of Table 6-1.
```
