
mounted as read-write, or containing executable files, should always be mounted with the hard option. If you use soft mounted file systems, unexpected I/O errors can occur. For example, consider a write request. If the NFS server goes down, the pending write request simply gives up, resulting in a corrupted file on the remote file system. A read-write file system should always be mounted with the specified hard and intr options. This lets users make their own decisions about killing hung processes. Use the following to mount a file system named /data located on a host named thor with the hard and intr options:

```
mount -F nfs -o hard,intr thor:/data /data
```

If a file system is mounted hard and the intr option is not specified, the process hangs until the remote file system reappears if the NFS server goes down. For a terminal process, this can be annoying. If intr is specified, sending an interrupt signal to the process kills it. For a terminal process, this can be done by pressing Ctrl+C. For a background process, sending an INT or QUIT signal as follows usually works:

```
kill -QUIT 3421
```

To mount a file system called /data, which is located on an NFS server called thor, issue the following command, as root, from the NFS client:

```
mount -F nfs -o ro thor:/data /thor_data
```

In this case, the /data file system from the server thor is mounted read-only on /thor_data on the local system. Mounting from the command line enables temporary viewing of the file system. If the umount command is issued or the system is restarted, the mount is lost. If you would like this file system to be mounted automatically at every startup, add the following line to the /etc/vfstab file:

```
thor:/data - /thor_data nfs - yes ro
```

To view resources that can be mounted on the local or remote system, use the dfmounts command as follows:

```
dfmounts sparcserver
```

The system responds with a list of file systems currently mounted on sparcserver:

| RESOURCE | SERVER | PATHNAME | CLIENTS |
|---|---|---|---|
| - | ultra5 | /usr | 192.168.1.201 |
|  | ultra5 | /usr/dt | 192.168.1.201 |

> NOTE
> Sending a KILL signal (-9) does not kill a hung NFS process.

> NOTE
> The mount and umount commands require root access. The umount command and /etc/vfstab file are described in Chapter 6.

Sometimes you rely on NFS mount points for critical information. If the NFS server were to go down unexpectedly, you would lose the information contained at that mount point. You can address this issue by using client-side failover. With client-side failover, you specify an alternative file system to use in case the primary file system fails. These file systems should contain equivalent directory structures and identical files. This option is available only on read-only file systems. To set up client-side failover, use the following procedure.

On the NFS client, mount the file system using the -ro option. You can do this from the command line or by adding an entry to the /etc/vfstab file that looks like the following:

```
zeus,thor:/data  -  /remote_data  nfs  -  no  -o ro
```

If multiple file systems are named and the first server in the list is down, failover uses the next alternative server to access files. To mount a replicated set of NFS file systems, which might have different paths to the file system, use the following mount command:

```
mount -F nfs -o ro zeus:/usr/local/data,thor:/home/data \
/usr/local/data
```

Replication is discussed again in the section that describes AutoFS.

A new feature in Solaris 8 is NFS server logging. Logged file systems were discussed in Chapter 7, “Solaris File Systems: Advanced Topics.” This extends that functionality to networked file systems. The daemon, nfslogd, provides NFS logging and is enabled using the log=<tag> option in the share command described later. When NFS logging is enabled, all NFS operations on the file system are recorded in a buffer by the kernel. The data recorded includes a timestamp, the client IP address, the UID of the requestor, the file handle of the resource that is being accessed, and the type of operation that occurred. The nfslogd daemon converts this information into ASCII records that are stored in ASCII log files.

## STEP BY STEP

### 17.1 Enabling NFS Server Logging

To enable nfs server logging, follow these steps:

- 1. As root, share the NFS file system using the following command:

```
share -F nfs -o ro,log=global <file system name>
```

Add this entry to your /etc/dfs/dfstab file if you want it to go into effect every time the server is booted.

- 2. If the nfslogd daemon is not already running, start it by typing:

```
/usr/lib/nfs/nfslogd
```

You can change the file configuration settings in the NFS server logging configuration file called /etc/nfs/nfslog.conf. This file defines path, filenames, and type of logging to be used by nfslogd. Each definition is associated with a tag. The global tag defines the default values, but you can create new tags and specify them for each file system you share. The NFS operations to be logged by nfslogd are defined in the /etc/default/nfslogd configuration file.

## WebNFS

WebNFS is a product from Sun Microsystems that extends its NFS to the Internet. Sun believes WebNFS offers considerable performance advantages over the current Internet protocols, HTTP and FTP. Netscape, Oracle, IBM, Apple, and Novell have announced support for WebNFS.

The World Wide Web has become the people’s choice for information distribution and sharing across the Internet. The web’s ease of use and widespread availability has helped it outshine similar technologies. Unfortunately, the protocol for the web and HTTP, leaves much to be desired in terms of performance. HTTP is a one-way protocol that transfers multiple data formats inefficiently. Entire pages and all their contents must be transferred at the same time to the requesting browser. On the other hand, NFS works with only portions of files at a time, usually only the sections that are in use. It is possible to update sections of a file with NFS, a task that is virtually impossible with HTTP. The following are the benefits of WebNFS over HTTP and FTP:

- **Connection management.** A WebNFS client can download multiple files over a single persistent TCP connection.

- **Concurrency.** WebNFS clients can issue multiple concurrent requests to an NFS server. The effect is a better use of server and network resources and better performance for the end user.

- **Fault tolerance.** WebNFS is well-known for its fault tolerance in the face of network and server failures. If interrupted, other FTPs require the download to be restarted from the beginning, causing users to retrace steps and waste time in duplicating efforts. However, if a WebNFS client faces an interruption, it can resume a download from where it left off.

- **Performance and scalability.** NFS servers currently handle over 21,000 operations per second. They are highly integrated with the OS, tuned for maximum system performance, and easy to administer.

WebNFS helps simplify remote file access. It can work with and through firewalls, meaning that system administrators can now specify which directories or files they want to export, or make available over the Internet. After these files are exported and an application requests them, WebNFS can automatically locate them, negotiate file access privileges, and transparently “mount” the files from anywhere on the Internet. Users can then access that data as if it were local to their machine.

Unlike current file access protocols, such as FTP and HTTP, WebNFS is a complete file system that supports in-place editing of a file, eliminating the need to download, edit, and upload the file. Instead, users can edit the original file right from their desktops. This saves time and preserves the integrity of shared files.

WebNFS can mount an entire file system at a time, or it can communicate with individual files on the server. This feature is known as multi-component lookup (MCL), and it lets the client look up a document based on a full given path to a file rather than having to look up individual components of that path until deriving the actual file location. For example, to look up a file such as /books/solaris/test.txt in NFS, you have to look up the individual components (books and solaris) before you can find test.txt. With WebNFS, you simply pass the entire path to the server itself and have the server return the file handle directly. This improves performance by saving several steps of data transfers.
