# Linux Administration: A Beginner's Guide

Network File System NFS is one of the native ways of sharing files and applications across the network in the Linux/UNIX world. The NFS concept is similar to that of Microsoft Windows File Sharing, in that it allows you to attach to a remote file system (or disk) and work with it as if it were a local drive—a handy tool for sharing files and large storage among users.
NFS and Windows File Sharing are solutions to the same problem; however, these solutions are very different beasts. NFS requires different configurations, management strategies, tools, and underlying protocols. We will explore these differences as well as how to deploy NFS in the course of this chapter.

# Mechanics of NFS

With most network-based services, NFS follows the usual client and server paradigms—that is, it has its client-side components and its server-side components.
Chapter 7 covers the process of mounting and unmounting file systems. The same principles apply to NFS, except you need to service the server hosting the share in addition to the other items (such as options) you would normally define. Of course, you also need to make sure the server is configured to permit access to the share

Let's look at an example. Assume there exists an NFS server named serverA that needs to share its local /home partition or directory over the network. We say that the NFS is "exporting its /home partition". Assume there also exists a client system on the network clientA that needs access to the contents of the /home partition exported by the NFS server. Finally, all other requirements are met (permissions, security, compatibility, and so on).

For clientA to access the /home share exported by serverA, clientA needs to make an NFS request for /home so that it can mount it locally, that the share appears locally as the /home directory. The command to trigger this request can be as this:

```
[root@clientA ~]# mount serverA:/home /home
```

Assuming that the command was run from the host named clientA, all users on clientA would be able to view the contents of /home as if it were just another directory or local file system. Linux took care of all of the network requests to the server.

Remote procedure calls (RPCs) are responsible for handling the requests between the client and the server. RPC technology provides a standard mechanism for any RPC client to connect to the server and find out which the calls should be directed. Thus, whenever a server wants to make itself available on a server, it needs to register with the RPC service manager, portmap, which tells the client where the actual service is located on the server.