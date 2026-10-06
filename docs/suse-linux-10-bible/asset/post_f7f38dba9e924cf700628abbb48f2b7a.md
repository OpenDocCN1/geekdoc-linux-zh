
# Chapter 22 Working with NFS and NIS

```
/test * (rw, sync)
```

Making a change in /etc/exports, use the command nfserver reload to make the NFS server re-read the configuration without restarting.

You can specify an IP number or range, or a Domain Name System (DNS) name (provided it can be resolved) as the client or clients to export. So do any of the following work:

```
/test client (rw, sync)
/test 192.168.1.26 (rw, sync)
/test 192.168.1.0/255.255.255 (rw, sync)
/test 192.168.1.0/24 (rw, sync)
```

The option rw (read-write) is set in all the preceding lines. However, the option allows read-only access only if you want.

As previously noted, the /etc/exports file is a simple collection of lines those we've chosen. The comment character is #. So the following might be a simple complete /etc/exports:

```
# See the exports(5) for a description of the syntax of this file.
# This file contains a list of all directories that are to be exported to
# other clients via NFS (Network File System).
# This file used by rpc.nfsd and rpc.mount. See their mappings for details
# on how to make changes in this file effective.
```

```
/data2/* (sync)
/home/peter/* rabbit (rw, root_squash, sync)
/home/david/* * (rw, root_squash, sync)
/media/cdrom/* (sync)
```

In this example, the comments at the top are all that you will see in /etc/exports on a new installation. The directory /data2 is exported-read (that's the default if neither ro nor rw is specified) to host. Peter's home directory is exported read-write with root_squash option, but to his machine rabbit. If he becomes root on rabbit, he will not have root privileges over the files in the server. The CD is exported to all hosts.

# Setting Root, User, and Group Client Privileges

By default, the root user on the client is mapped to the anonymous user nobody on the server, which means that the root user on the client does not have full privileges over the files on the mounted share. This default option can be made explicitly by specifying root_squash. The opposite of this is no_root_squash, which allows the root user to enjoy full root privileges on the NFS server.

> Unless there is a special reason to do otherwise, filesystems should be exported with the root_squash option.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_633_0.png)

The option all_squash is similar but maps all users to the user nobody. When the share is mounted, a normal user on the client will not be able to write to the share unless the permissions on the directory allow others to write to it. And any file that is created in this will be owned by user nobody and group nogroup.

When using the all_squash option, you can also specify explicitly the user ID (UID) and group ID (GID) that you want users to be mapped to rather than the defaults for the user nobody. For example:

```
/test client (rw, sync, all_squash, anonuid-1999, anogid-1999)
```

This enables you to create a user on the server with the stated UID and GID and properly arrange that user's permissions on the share.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_634_0.png)

Figure 22-2: Configuring the NFS server with YaST

When you start the module, it asks whether or not the NFS server should be started and then provides an interface that enables you to add a directory (to be exported) and specify the hosts and the options for that. These are precisely the options discussed previously, and you have to type them in hand.

# The exports Command

The exports command can be used to handle the exporting of directories directly from the command line. To export all directories listed in /etc/exports, use exports -a.

If /etc/exports has changed, exports -r reread /etc/exports and changes the state of the directories being exported accordingly. This is like doing nfsserver reload.

You can export a directory that is not mentioned in /etc/exports by doing something like this:

```
root@client: ~ # exports -iv -o rw,sync client:/tmp
```

The -iv option tells exports to ignore /etc/exports and is verbose. The -o introduces the options, and the command as a exports the directory /tmp to the machine client.

With the option -u, the command exports a currently exported directory:

```
root@client: ~ # exports -u client:/tmp
```

To export all directories mentioned in /etc/exports, do exports -au.

# The showmount Command

The command showmount client: ~ provides information about mounts on an NFS server.

```
user@client: ~ > showmount -e bible
```

This command lists the lists for the server bible. Typically this will be the contents of /etc/exports, but if changes have been made without using exports as described in the previous section, these will be reflected in the output.

```
root@client: ~ # exports -i -o rw,sync client:/home
```
```
user@client: ~ > showmount -e bible
/home
```

In the preceding example, you can see /home, which you just configured, and /test, which was included in /etc/exports.

If you want information about what is actually mounted from bible, use the -a option:

```
user@client: ~ showmount -a
All mount points on bible:
client
```

This shows that the directory /test is currently mounted by client.

showmount -d bible shows the directories being mounted:

```
user@client: ~ showmount -d bible
Directories on bible:
/
```

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_636_0.png)

> Caution The information given by showmount can sometimes include mounts that are no longer present. This can happen if the client reboots without unmounting the NFS mount. To correct this situation, necessarily, remove the file /var/lib/nfs/mounttab -r and restart the NFS server.

# Problems with Mounting NFS Shares

If you find that you cannot mount a share that you think should, the first thing to check is whether the NFS server is actually running. Check the /etc/exports file and be sure that you have done exports -r since making any changes to it. The command rpcinfo can be useful; if all is well, its output should look like this:

```
user@client: ~ rpcinfo -p
```

| program | proto | port | status |
| :--- | :--- | :--- | :--- |
| 100000 | tcp | 111 | portmapper |
| 100000 | udp | 111 | portmapper |
| 100003 | tcp | 2049 | nfs |
| 100003 | udp | 2049 | nfs |
| 100027 | tcp | 2049 | nfs_acl |
| 100027 | udp | 2049 | nfs_acl |
| 100021 | udp | 3771 | nlockmgr |
| 100021 | udp | 3771 | nlockmgr |
| 100023 | tcp | 3771 | nlockmgr |
| 100023 | udp | 3771 | nlockmgr |
| 100021 | tcp | 3280 | nlockmgr |
| 100021 | udp | 3280 | nlockmgr |
| 100024 | tcp | 3280 | nlockmgr |
| 100024 | udp | 3280 | nlockmgr |
| 100005 | tcp | 629 | mountd |
| 100005 | udp | 629 | mountd |
| 100005 | tcp | 633 | mountd |
| 100005 | udp | 633 | mountd |

If you don't see entries for nfs in this listing, then something is seriously wrong; perhaps the NFS server has not registered itself with the portmapper. Stopping the NFS server, the portmap service, and the network and starting them in the reverse order.

# NFS Security Considerations

NFS has inherent security problems. Just as SMB shares, you certainly should not make it available beyond the private network.

The lists of all exports file are no defense against anyone who is able to alter a machine's IP address (with physical access in practice means anyone). The point made in the previous section about UIDs that a user may have the wrong permissions on other's files on the server, but if a user has root access on the client (again, with physical access that they can become any user they want).

NFS security will improve when the client becomes fully compliant with the NFS version 4 standard. In the future, it will be possible to secure authentication for NFS on Linux. In the meantime, no measures to tighten NFS security should be regarded as totally effective. The subject is discussed further in the NFS document at http://nfs.sourceforge.net/nfs-howto/

Finally, NFS provides a very simple and transparent way of sharing filesystems across a network. It is likely to be an essential part of any network infrastructure, which includes Linux or Unix systems both as server and client. The information in this chapter should enable you to work with NFS on both the client and the server.

# Using NIS for Authentication

As touched upon when discussing the root_squash and all_squash options, the question of ensuring consistent user and group IDs across a network of NFS clients and servers is not a trivial one. The previous section focused on ensuring that the root user on an NFS system didn't get undue privileges to files owned by root on a file system that is exported by an NFS server. However, the same basic problem is also present for normal users. If a user's ID differs on the NFS server and client,
