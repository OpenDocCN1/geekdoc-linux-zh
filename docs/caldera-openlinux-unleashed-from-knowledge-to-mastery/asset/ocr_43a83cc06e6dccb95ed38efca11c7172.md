NFS is a stateless protocol. This means that the server does not remember anything about file operations; each operation is atomic as far as the server is concerned. For example, suppose you wish to read a 2KB file. You may read one kilobyte first, followed by the second kilobyte. The NFS server does not remember a "file position" or any such thing; it is up to the NFS client to handle all the state.

In the example, the NFS client would do an atomic "read one kilobyte starting at location 0" followed by an atomic "read one kilobyte starting at location 1024."

This design is highly unusual, but it has a number of benefits:

+   - An NFS server can crash and reboot, and the client won't notice anything wrong. Because the server doesn't store any information about "connections," it can't lose any information if it crashes. (Until the server reboots, however, the client will notice that it is taking a very long time to respond.)
+   - An NFS server can handle many clients. Because there is no per-client connection or state to maintain, thousands of clients can mount NFS volumes with no impact on the server (unless they all try accessing the volumes at the same time!).

However, the stateless design has a serious drawback: There is no way to lock NFS files because a file lock implies that the server must remember some state. There are a number of ways around this, usually involving special locking daemons, but none of these is available for Caldera OpenLinuX. So do not place database files (which often require locking) on an NFS volume.

# Mounting an NFS Volume

To mount an NFS volume, the kernel (on the client) contacts a special mount daemon on the server. It passes the path name of the volume to mount. The mount daemon returns a handle, which is a chunk of bytes. The meaning of the handle is irrelevant to the client; presumably, it means something to the server. Whenever the client wishes to refer to the mounted volume, it passes the same handle back to the server.

To refer to a particular file, the client asks the NFS server to perform directory searches (starting with the handle given by the mount daemon). The NFS server returns another handle, which refers to the file. From this point on, the client specifies the handle and the desired operation for all subsequent NFS operations.

The server generates handles in such a way that if the server crashes and restarts, the handles are still valid. This allows clients to keep going if it nothing but a slowdown in the network traffic happened.