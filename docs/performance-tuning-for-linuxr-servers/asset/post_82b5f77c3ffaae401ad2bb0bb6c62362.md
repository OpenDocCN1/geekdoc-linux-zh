
- NFS version 3 (highly recommended) client or server
- NFS over TCP on the server (recommended); it is always on in the client
- NFS version 4 (experimental)
- NFS direct I/O (experimental)

For SMB/CIFS, there is a choice of two clients: the legacy smdfs and the newer CIFS VFS. For the server, by far the most popular choice is the Samba network file server, which provides not just SMB/CIFS network file serving but also the following:

- A logon server for Windows and winbind Linux clients
- A network print server
- Administration tools and DCE/RPC-based management services
- An RFC 1001/1002 NetBIOS name server

## Tuning the Linux Client

### Some Key Concepts

This section covers some of the key concepts you need to consider when tuning the Linux client. These concepts include the following:

- Protocol layering
- Opportunistic locking
- Metadata
- File change notification
- Read-only volumes and read-only files

### Protocol Layering

The following trace, taken from the Ethereal network analyzer, shows the typical 20 network frames (requests and responses) that occur at mount time (see Figure 16-2). The trace was taken from the _mount_ command using CIFS VFS version 1.0.3 running on a Linux kernel 2.4.23 based client.

**Figure 16-2. The typical 20 network frames that occur at mount time.**

![](img/08b574e80eed8279bfda286dbd25d40d_441_0.png)

Figure 16-3 shows a more detailed view of a particular frame; in this case, the Tree Connect request clearly shows the layering of an SMB request (the mount data, with the SMB header) inside an RFC 1001 (NetBIOS session service) frame, inside a TCP/IP frame, inside an Ethernet frame.

**Figure 16-3. A detailed view of the Tree Connect request.**

![](img/08b574e80eed8279bfda286dbd25d40d_442_0.png)

In this example, the SMB request is 86 bytes (including 32 bytes of SMB header), preceded by a 4-byte RFC 1001 header (length), preceded by 32 bytes of TCP header, 20 bytes of IP header, and 14 bytes of Ethernet header. This layering is much like nesting envelopes—this is enclosing an envelope with a letter for a child inside a larger envelope addressed to the child's parent.

### Opportunistic Locking

Figure 16–4 shows the protocol flow involved in opportunistic locking (oplock) handling for CIFS. CIFS has two types of opportunistic locks that are used to control distributed access to files. By contrast, AFS and DFS have much more complex but heavyweight token-management mechanisms. NFS versions 2 and 3 have no locking mechanisms and therefore have relaxed UNIX file semantics at the risk of data integrity.

**Figure 16-4. Protocol flow in opportunistic locking. (Source: www.microsoft.com/Mind/1196/CIFS.htm)**

![](img/08b574e80eed8279bfda286dbd25d40d_443_0.png)

The first type of opportunistic lock is the whole file lock (exclusive oplock), which allows the client to do aggressive write-behind and read-ahead caching on the file, often greatly improving performance.

The second type of oplock is a read oplock. A read oplock allows multiple clients to read, but not update, a file. Attempts to update such a file by one client cause all clients with that file open to lose their caching privileges for that file. Distributed caching encounters a problem with Linux because files that are closed cannot be safely cached with the oplock mechanism alone. (Although not particularly common, the standard POSIX file semantics allow a memory mapped file to have no open file instances, but the data associated with the inode can still be read.)

A third type of oplock, the batch oplock, is more rare. It is used to address certain performance problems associated with the line-by-line interoperation of DOS batch files (scripts) by allowing limited read-ahead caching of batch files by the client. These distributed caching mechanisms in the Linux client are in addition to and unrelated to caching being done in the server file system's page manager, and again in the server disk controllers.

### Metadata

File and directory timestamps reflect the time of the last update to a file or directory. The CIFS network file system client uses timestamps to determine whether data in its page cache needs to be discarded when reopening a file that has been closed, but this caching is transparent to the user. AFS and DFS clients have a much more complex token-management approach to achieving cache consistency, which can safely cache network files on disk on the client for long periods. NFS versions 2 and 3 generally have looser data consistency and read-ahead and write-behind cache data based on timers.

### File Change Notification

File change notification is available in NFS version 4 and CIFS as a way of allowing a client application to be notified of changes to certain files and directories. File change notification can be used to augment the client file system's distributed caching facility, although this has not been proven to be efficient and is not currently implemented for this purpose in the Linux clients.

### Read-only Volumes and Read-Only Files

Read-only clients can cache aggressively if the mounted volume is known to contain read-only data (such as a mount to a server that is exporting a read-only CD-ROM or DVD). However, read-only clients provide little benefit over oplock, which in effect allows the same thing.

The legacy smbfs client does not do safe distributed caching (oplock). Instead, it relies on timers to determine the invalidation frequency for client-cached network file data and has limited performance adjustments. A significant improvement in smbfs performance was obtained midway through the 2.4 kernel development when the smbfs network request buffer size was increased from 512 bytes to approximately one page (4096 bytes).

The Linux CIFS client implements oplock, which is enabled by default (oplock can be disabled by setting /proc/fs/cifs/OplockEnabled to 0 on the client). The Linux CIFS client attempts to negotiate a buffer size of about 16K. If the server supports this buffer size, more efficient read and write transfers with fewer network round trips can be achieved. By reducing the rsize and wsize (configurable by specifying the size as an option on mount), as with the NFS client, the default read and write size can be reduced in an attempt to minimize TCP packet fragmentation, but this usually slows performance. The lookup caching mechanism in the CIFS VFS, as in smbfs, is done based on a timer rather than with the CIFS FindNotify API. This caching of inode metadata, even for short periods, improves performance over the alternative, that is, revalidating inode metadata on every lookup, but with the risk that the client's view of stat information (such as file size and timestamps) on a file will be out of date more often. CIFS lookup caching can be disabled by setting /proc/fs/cifs/LookupCacheEnabled. A limited set of statistics is kept by the CIFS client in /proc/fs/cifs/Stats. Enabling debugging or tracing (setting /proc/fs/cifs/cifsFYI to 1, or setting /proc/fs/cifs/traceSMB to 1) can slow the client performance slightly.

Unlike the current 2.6 smbfs and cifs client file system modules, the NFS client does a good job of dispatching multiple read-ahead requests in parallel to a single server from a single client. This parallelism helps keep the server disk busy. The difference is even more significant when writing large files from a single process on the client to the server. A Linux client can copy files using NFS version 3 much faster to a lightly loaded Linux server on Gigabit Ethernet than using CIFS copying to a Linux/Samba server. This is due to the efficient implementation of multipage asynchronous write-behind in the NFS client. The differences in read performance between NFS and CIFS are not as dramatic because both implement multipage read-ahead (readpages). The CIFS client is in turn faster than the smbfs client for file copy from the same Samba server because CIFS can use a larger read size (16K versus 4K) of the CIFS VFS and can read more than one page at a time (via the new readpages function, which is now an optional feature that 2.6 kernel file systems may implement). Future versions of the CIFS VFS client should be able to narrow the performance gap against NFS. However, exceeding NFS performance for large file copy will require a redesign of the SMB dispatching mechanism of the Samba server, as is being done for Samba version 4. When multiple processes copy different files to the same server, CIFS benefits from the capability to queue as many as 50 simultaneous read or write requests to the server.

## Linux File Server Tuning

Network file system tuning is complex. Bottlenecks can be caused by high CPU usage, disk usage, or network usage, and network latency can dramatically influence throughput. The following list summarizes some general principles to use when evaluating performance improvements:

- Maximize parallelism from each client
- Maximize server parallelism in adapter interrupt dispatching
- Maximize server CPU parallelism
- Maximize client caching opportunities
- Minimize data sent
- Minimize round trips from client to server
- Maximize command chaining
