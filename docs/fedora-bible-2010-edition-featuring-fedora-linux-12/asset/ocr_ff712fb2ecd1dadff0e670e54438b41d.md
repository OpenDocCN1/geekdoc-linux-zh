+   **Export only if mounted** — If a file system that is set to be shared is a mount point that is currently not mounted, the file system will not be exported if this option is on (represented by the `mp` option). This can prevent NFS from sharing empty directories and having contents stored to the empty directory disappear the next time the resource is mounted.

+   **Optional mount point** — You can also identify the mount point directly by checking this box and setting the file system mount point. For example, if you are sharing the `/mnt/files/isos` directory and you identify `/mnt/files` as the mount point (`mp=/mnt/files`), the `/mnt/files/isos` directory will not be shared if the `/mnt/files` directory isn’t mounted.

+   **Set explicit Filesystem ID** — Because not all file systems have UUIDs to identify them, you can identify a further file system you want to share using its file system ID. The result is that the `fsid` option is set to that value (`fsid=???`). If you prefer, you can identify a file system as the root of your shared file systems (`fsid=0`).

+   Click the User Access tab, and then select any of the following options:
+       * **Treat the remote root user as local root** — If this option is on, it enables the remote root user host accessing your shared directory to save and modify files as though he or she were the local root user. Having this on is a security risk because the remote user can potentially modify critical files. (This sets the `no_root_squash` option.)
+       * **Treat all client users as anonymous users** — When this option is on, all users will be assigned the default anonymous user and group ID of 65534 (`nfsnobody`). (This sets the `all_squash` option.) You can also indicate that particular user and group IDs be assigned to every user accessing the shared directory from a remote computer by entering the user ID and group ID you want assigned to all remote users. (This sets the `anoid` and `anogid` options to the numbers you choose.)

+   Click OK. The new shared directory appears in the NFS Server Configuration window.

+   Click the Server Settings button. If your system is configured to use a firewall, the pop-up window that appears lets you set static ports for NFS-related services. Once you set specific numbers for those ports, you need to set firewall rules to allow access to those ports through your firewall (see Chapter 13 for information on configuring your firewall).

At this point, the configuration file (`/etc/exports`) should have the shared directory entry created in it. The `/etc/sysconfig/nfs` file should have the static ports assigned to NFS services, if you set them in the previous step. To turn on the NFS service and make the shared directory available, type the following from a Terminal window as root user:

+   To immediately turn on NFS, type:

```
# service nfslock start; service nfs start
```

+   To permanently turn on the NFS service, type:

```
# chkconfig nfslock on; chkconfig nfs on
```