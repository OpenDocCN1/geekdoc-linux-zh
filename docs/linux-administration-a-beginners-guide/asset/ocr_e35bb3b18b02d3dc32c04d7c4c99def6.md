# Chapter 18: Network File System (NFS)

the /etc/exports file.) If the client does have permission, the mount service returns an affirmative.

+   3. The client again contacts the portmapper, this time to find out on which port the NFS server is located. (Typically, this is port 2049.)
+   4. Whenever the client wants to make a request to the NFS server (for example, to read a directory), an RPC is sent to the NFS server.
+   5. When the client is done, it updates its own mount tables but doesn't inform the server.

> NOTE: Notification to the server is unnecessary because the server doesn't keep track of all clients that have mounted its file systems. Because the server doesn't maintain state information about clients and the clients don't maintain state information about the server, clients and servers can tell the difference between a crashed system and a really slow system. Thus, if a NFS server is rebooted, all clients can automatically continue their operations with the server as soon as the server is back on line.

# Security Considerations for NFS

NFS, unfortunately, is not a very secure method for sharing disks. The steps necessary to make NFS more secure are no different from those for setting any other system. The only catch is that you must be able to trust the users on the client system, especially the root user. If you're the root user on both the client and server, then there is a little less to worry about. The important thing in this case is to make sure non-root users don't become root—which is something you should be doing anyway!

If you are in a situation where you cannot fully trust the person with whom you need to share a disk, it will be worth your time and effort to seek alternative methods of sharing resources (such as read-only sharing of the disk, for instance).

As always, stay up to date on the latest security bulletins coming from the Computer Emergency Response Team (www.cert.org). And keep up with the all the patches from your distribution vendor.

# Versions of NFS

NFS is not a static protocol. Standards committees have helped NFS evolve to take advantage of new technologies as well as changes in usage patterns. Today the standards are up to version 3.0, with 4.0 in the works. Linux's NFS implementation is, unfortunately, behind the times in this regard—it supports up to version 2.0 only. Efforts are being made to support NFS version 3.0, but this will of course take time.

Most other operating systems supporting NFS probably have an NFS version 2.0 mode which allows you to use Linux servers. Some of these systems (including IRIX) require that you explicitly specify the NFS mount option (-vers=2) for servers that only allow NFS 2.0. Refer to the appropriate vendor's documentation for details.