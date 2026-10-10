The Network File System (NFS) is the standard UNIX method for sharing file systems between computers, meaning that NFS enables you to access remote file systems exactly as if they were local. NFS file systems accessed in this way are called NFS volumes.

NFS has a couple of important uses:

+   - Users' home directories can be kept on a central NFS server and mounted by clients. This allows users to use any of a number of workstations and still have access to their files in the same location in the file system tree. Combined with NIS, NFS allows you to make workstations on a LAN "generic:" providing exactly the same login environment to all users.
+   - Large local software installations can be kept on a central server. This reduces disk space requirements and simplifies software updates.

> **Note**
> 
> NFS does have its drawbacks, however. NFS is not secure—anyone who has physical access to your network can intercept and inspect NFS data. Furthermore, it is relatively easy for computer criminals to fool NFS's authentication mechanisms and impersonate another user on your network. For this reason, you should never use NFS to share sensitive information or use it across the Internet. You should set up firewalls to block NFS traffic.

# How NFS Works

NFS uses Sun RPC (as discussed in Chapter 14) for client-server communications.

Under Linux, the client side of NFS is built directly into the Linux kernel. However, two normal Linux programs implement the server side.

> **Background Material**
> 
> Traditional UNIX systems implement both client and server directly in the kernel. There is a kernel-space NFS server for Linux, but it is still experimental. You should use the user-space programs for now.