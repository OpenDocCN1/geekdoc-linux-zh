RPC protocol, which implements a reboot notification service (letting clients know when the NFS server has been rebooted), which is used by the NFS file locking service, rpc.lockd, to handle existing locks after a reboot. You can set this to no in a pure NFS 4 environment to avoid starting an unnecessary service, but I recommend against it unless you guarantee that no client speaks only the NFS 2 or NFS 3 protocol will ever need to mount directories from this NFS server.

+   - STATDOPTS: Enables to pass you to pass arguments to the rpc.stat daemon when it starts. The most common of these are the -p listenport and -s sendport, which you can use to define specific ports for the status daemon to listen and send on. This can be useful if you are using a port-based firewall or if you want to use other ports than the defaults as a security measure. Unless this is the case, you should usually not provide a value for this option.
- NEED_IDMAPD: Set to yes to ensure that the rpc.idmapd daemon, required by NFS 4 clients, is started. This server supports UID/GID mappings to specific user and group names.
- NEED_GSSD: Set to no to ensure that the rpc.gssd daemon, which is required for Kerberos authentication support, is not started. If you are using Kerberos authentication with NFS, you should set this to yes to ensure that this daemon is started.

After setting these values, file this startup script creates and mounts an in-memory pipe filesystem associated with basic NFS support by executing the command sudo /etc/init.d/nfs-common restart.

# Note

When run in start or restart modes, this startup script creates and mounts an in-memory pipe filesystem called rpc_pipes, used for inter-process communication by RPC-based server processes such as idmapd or rpc.gssd, mounting it on the directory /var/lib/rpc_pipes. Although this filesystem will be listed in the mount command, you will not see this filesystem in your /etc/fstab file because the filesystem is created and mounted by the nfs-common script to limit NFS-related changes to files that are created by other packages.

# Configuring NFS Kernel Server Options

Options for the common NFS services for an NFS server are set in the file /etc/default/nfs-server, which you can edit using your favorite editor. Each of the following options is defined in a setting that looks like setting=value, where value is one of yes or no. The options that you should set are the following:

+   - RPCNFSDCOUNT: Set this to a specific numeric value to identify the number of NFS deamon instances that you want to start. The default value, 8, is usually sufficient, although you may want to increase this value if your NFS server is serving files to a large number of clients.