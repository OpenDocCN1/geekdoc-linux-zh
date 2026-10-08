Every interface on your network must have a unique IP address. Systems that have two network interfaces must have two unique IP addresses. I will cover some networking commands in Windows in an upcoming chapter.

# ## NFS Background

I am not going to limit the discussion and examples in this chapter to NFS. There are other services used to share files that are also useful, such as File Transfer Protocol (FTP) which I'll show examples of as well. Because NFS is so widely used in the UNIX user community, it is one of my goals to expose you to how NFS can be used in a Windows and UNIX environment.

NFS allows you to mount disks on remote systems so that they appear as though they are local to your system. Similarly, NFS allows remote systems to mount your local disk so that it looks as though it is local to the remote system.

NFS, like X Windows, has a unique set of terminology. Here are definitions of some of the more important NFS terms:

**Node** A computer system that is attached to or is part of a computer network.

**Client** A node that requests data or services from other nodes (servers).

**Server** A node that provides data or services to other nodes (clients) on the network.