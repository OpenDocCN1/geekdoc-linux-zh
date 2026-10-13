# NFS Service Daemons

While the basic NFS control script (/etc/init.d/nfs) is fairly simple, that script includes a number of service daemons, each with its own function. These service daemons may be stored either in the /sbin or the /usr/sbin directories. All but rpc.statd are controlled by the NFS control script.

+   - **rpc.idmapd** Works if /etc/idmapd.conf is configured.
+   - **rpc.mountd** Processes mount requests and verifies current exports.
+   - **rpc.nfsd** Supports client access with needed kernel threads.
+   - **rpc.rquotad** Works with quota information.
+   - **rpc.statd** Configures the status monitor, controlled by the /etc/init.d/nfslock script.

# NFS Control Commands and Files

NFS includes a wide variety of commands to set up exports, to show what's available, to see what's mounted, to review statistics, and more. Except for specialized mount commands, these commands are can be found in the /usr/sbin directory.

The NFS mount commands are mount.nfs, mount.nfs4, umount.nfs, and umount.nfs4. Functionally, they work like regular mount and umount commands. As suggested by the extensions, they apply to filesystems shared via NFSv4 and other NFS versions. Like other mount.* commands, they have functional equivalents. For example, the mount.nfs4 command is functionally equivalent to the mount -t nfs4 command.

If you're mounting a directory shared via NFSv2 or NFSv3, the mount.nfs and mount -t nfs commands are available for both systems.

The packages associated with NFS include a substantial number of commands in the /usr/sbin directory. The list of commands shown here are just the ones most commonly used to configure and test NFS.

+   - **exportfs** The exportfs command can be used to manage directories shared through and configured in the /etc/exports file.
+   - **nfsios tat** A statistics command for input/output rates based on an existing mount point. Uses information from the /proc/self/mountstats file.
+   - **nfsstat** A statistics command for client/server activity based on an existing mount point. Uses information from the /proc/self/mountstats file.