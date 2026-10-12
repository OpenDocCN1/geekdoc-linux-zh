The only problem in using NFS is that each client system must support it. Most PCs don't come with NFS — that means you have to buy NFS software separately if you want to share files by using NFS. If, however, all systems on your LAN run Linux (or other variants of UNIX with built-in NFS support), then it makes sense to use NFS.

![](bbox=[0.18, 0.28, 0.27, 0.38])

Note that NFS has security vulnerabilities. Therefore, you should not set up NFS on systems directly connected to the Internet.

In the upcoming section, I walk you through an NFS setup, using an example of two Linux PCs on a LAN.

# Exporting a file system with NFS

Start with the server system that exports — makes available to the client systems — the contents of a directory. On the server, you must run the NFS service and also designate one or more file systems that are to be exported, or made available to the client systems.

To export a file system, you have to add an appropriate entry to the /etc/exports file. For example, suppose you want to export the /home directory and you want to enable the host named LNB P75 to mount this file system for read-and-write operations (you can use a host's IP address in place of the host name). You can do so by adding the following entry to the /etc/exports file:

```
/home LNB P75(rw)
```

After adding the entry in the /etc/exports file, manually export the file system by typing /usr/sbin/exportfs -a in a terminal window. This command exports all file systems defined in the /etc/exports file

```
/usr/sbin/exportfs -a
```

Now start the NFS server — log in as root and type the following command in a terminal window:

```
service nfs start
```

To restart the NFS service, type service nfs restart.

When the NFS service is up, the server side of NFS is ready. Now you can try to mount the exported file system from a client system and access the exported file system.

![](bbox=[0.18, 0.85, 0.27, 0.95])

If you ever make any changes to the exported file systems listed in the /etc/exports file, remember to restart the NFS service. To do so, type service nfs restart in a terminal window.