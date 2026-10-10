
To mount an NFS file system, use the `mount` command like this:

```
# mount -t nfs server:volume mountpt
```

Here, `server` is the name of the NFS server and `volume` is the volume on the server. `mountpt` is a local mount point.

Here is a concrete example. I have a fast CD-ROM drive on `shishi` and would like `shevy` to be able to access the drive.

On `shishi`, there’s a line in `/etc/exports` like this:

```
/mnt/cdrom     shevy(ro,no_root_squash)
```

This allows `shevy` to mount `/mnt/cdrom` read-only. To mount the volume on `shevy`, I type:

```
# mount -t nfs shishi:/mnt/cdrom /mnt/shishi-cd
```

After this command has executed, the CD-ROM on `shishi` is available under `/mnt/shishi-cd` on `shevy`.

To unmount the volume, I use the usual `umount` command:

```
# umount /mnt/shishi-cd
```

### NFS Mount Options

NFS volumes can have a number of mount options associated with them. These include:

- `rsize=n` Sets the number of bytes NFS uses when reading from an NFS server. The default is 1024, but throughput may be improved for some servers by specifying 8192.
- `wsize=n` Sets the number of bytes NFS uses when writing to an NFS server. The default is 1024, but throughput may be improved for some servers by specifying 8192.
- `timeo=n` Sets the initial retransmission timeout in tenths of a second. NFS has a complex system of back-off if transmissions time out; see `nfs(5)` for more details.
- `retrans=n` Sets the number of minor timeouts and retransmissions before a major timeout occurs. Depending on other NFS options, a major timeout either causes a message to be printed on the console or the file operation to be aborted.
- `retry=n` The number of minutes that `mount` will keep trying to mount an NFS file system. The default is 10,000 minutes or about a week.
- `bg` If the first NFS mount attempt times out, `mount` puts itself in the background and keeps trying. If this option is missing, `mount` remains in the foreground and keeps trying to mount the file system.

You should use this option carefully depending on the file system you are trying to mount. For example, if you are NFS-mounting /usr at boot-time, then in all likelihood the workstation will be unable to proceed until /usr is mounted. Do not use bg in this situation.

However, if you are NFS-mounting a USENET news directory, it's probably more important to get the workstation up and running than wait for the news server to come alive. You should use the bg option in this case.

- `fg` This option does the opposite of `bg` (and the default behavior).
- `soft` If an NFS file operation has a major timeout, report an I/O error to the calling program.
- `hard` If an NFS file operation has a major timeout, print a message on the console and keep trying. This is the default.

The hard and soft options should be used carefully, too. You probably want important volumes hard-mounted because the system cannot continue unless they are mounted. Less important volumes can be soft-mounted. Be aware that soft-mounted file systems can cause data loss because NFS may not report errors immediately (because of network latency and other factors).

#### Background Material

Hard-mounted NFS file systems have been compared to slow disk drives, and soft-mounted ones have been compared to broken ones.

- `intr` If the volume is hard-mounted, this option allows you to interrupt the NFS file operation with the interrupt key. The default is to disallow this and force you to wait until the NFS server comes back up.

There are several more options for specialized situations; see `nfs(5)` for more details.

### NFS Volumes in /etc/fstab

You can automatically mount NFS volumes at startup by placing their mount parameters in `/etc/fstab`. Here's an example:

| Filesystem | Mountpoint | Type | Options | Dump | Pass |
| :--- | :--- | :--- | :--- | :--- | :--- |
| shishi:/mnt/cdrom | /mnt/shishi-cd | nfs | ro, bg | 0 | 0 |

This option mounts `shishi:/mnt/cdrom` on `/mnt/shishi-cd` read-only. If the initial mount request times out, `mount` puts itself in the background and keeps trying while the rest of the boot sequence continues.

### The showmount Program

The `showmount` command is useful for seeing which NFS volumes have been mounted by clients and which NFS volumes are being exported by a server.

To see the list of file systems exported by a server, type:

```
$ showmount -e server
```

For example:

```
$ showmount -e shishi
Export list for shishi:
/mnt/cdrom *.roaringpenguin.com
```

On the NFS server, you can see a list of hosts mounting file systems from the server:

```
$ showmount
Hosts on shishi.roaringpenguin.com:
scruffy.roaringpenguin.com
shevy.roaringpenguin.com
```

You can get more details with the `-a` option:

```
$ showmount -a
All mount points on shishi.roaringpenguin.com:
scruffy.roaringpenguin.com:/mnt/cdrom
shevy.roaringpenguin.com:/mnt/cdrom
```

This lets you see which hosts are mounting which volumes.

`showmount` has a few more options; see `showmount(8)` for details.

### Automounting

Sometimes it is convenient to distribute users’ home directories across many NFS servers. It would be highly annoying to have to always mount all the directories on all the machines when at any given time only one or two are required.

The automounter lets you create automount maps that specify which machine a certain directory resides on. Only when the directory is actually requested (for example, when someone logs in or tries to read a file from a directory) is the mount performed.

Linux supports two types of automounters: The *autofs* file system is built into the kernel and is configured by a utility program called *automount*. Unfortunately, Caldera OpenLinux does not include this package. It is available on most Linux archives, however.

The second automounter is called `am-utils` and does not rely on kernel support. Instead a daemon called *amd* "pretends" to be an NFS server. It intercepts NFS requests and performs any mounts needed to satisfy them.

Unfortunately, *amd* is quite complicated to set up. It comes with a 97-page manual whose contents are beyond the scope of this chapter. You can look at the manual using *info* like this:

```
$ info "(am-utils)Top"
```

Automounting is powerful, but it is often more trouble than it is worth. Unless you have a large network with many NFS servers, it is easier to use normal NFS mounts. In particular, most small networks are organized around a central file server with many clients. In this case, each client can directly mount files from the server without requiring complex automount maps.

### Summary

In this chapter, you have learned the basic principles of NFS, including its stateless design. You have learned how to mount NFS file systems and how NFS uses user and group IDs to determine access permissions. Next, you learned how to configure an NFS server by editing `/etc/exports` and how to start an NFS server by invoking `rpc.mountd` and `rpc.nfsd`. You learned some security considerations when setting up NFS servers. Next, you learned how to configure an NFS client and mount NFS volumes. Finally, you learned how to use `showmount` to get information about mounted and available NFS volumes. You were given a brief introduction to automounting and a pointer to the *amd* documentation.

## Configuring Samba

In This Chapter

- Overview of SMB 350
- Samba Configuration 351
- Running Samba 360
- Debugging a Samba Setup 360
- Mounting SMB Shares 362
- Checking Samba’s Status 363
- Web-Based Samba Configuration 364

Samba is software that allows Linux machines to share disk directories and printers with Windows clients. Samba uses the Server Message Block (SMB) protocol to communicate with Windows clients. This chapter will teach you how to set up a Linux machine to serve as a file and print server for Windows clients. You will also learn how to set up a Linux machine as a client for a Windows file server. These capabilities let you use Linux machines seamlessly in a mixed UNIX/Windows environment. By using Linux as a file and print server, you can save the often considerable cost of an NT license and the associated Windows NT maintenance and upgrade costs.

### Overview of SMB

SMB is a protocol originally designed to share resources over a local area network. It was originally a very primitive protocol, running on a proprietary network protocol called NetBIOS. Over the years, as more features were required, SMB became more and more complex until it grew into the complicated and ugly protocol it is today.

Until Samba was available, only Microsoft Windows, OS/2, and a number of proprietary and expensive add-on programs for UNIX machines could implement the SMB protocol. Samba is a free software suite that implements SMB by encapsulating NetBIOS packets over TCP/IP. Microsoft Windows can be configured to do the same and can interoperate with Samba as if Samba were a native Windows NT file and print server.

> **Note**
> 
> To use Samba, your Windows clients must have TCP/IP networking enabled and must be configured to use Client for Microsoft Networks and File and Printer Sharing for Microsoft Networks using TCP/IP.

Mapping SMB clients to UNIX poses some difficult problems because of the widely different philosophies of Windows and UNIX. Let's look at some of the areas of difficulty. UNIX uses user IDs to validate all file-access operations. SMB has a very loose user-name concept; early SMB protocols had no concept of usernames at all. Samba tries to cope with this by using user-level share security where possible. Windows 95/98 has no concept of user-level security; it permits only share-level security. In user-level security, access is granted based on a user supplying a username and a valid password. In share-level security, each shared resource is given a password, and a person connecting to it need only supply the password. This is clearly a problem for UNIX, which always requires a user ID.
