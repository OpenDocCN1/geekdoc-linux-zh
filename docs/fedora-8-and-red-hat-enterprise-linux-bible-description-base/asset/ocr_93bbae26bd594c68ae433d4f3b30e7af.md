(represented by the `mp` option). This can prevent sharing empty directories and having contents stored to the empty directory disappear the next time the resource is mounted.

+   *   **Optional mount point** — You can also identify the mount point directly by checking this box and setting the file system mount point. For example, if you are sharing the `/mnt/files/isos` directory and you identify `/mnt/files` as the mount point (`mp=/mnt/files`), the `/mnt/files/isos` directory will not be shared if the `/mnt/files` directory isn't mounted.

+   *   **Set explicit Filesystem ID** — Because not all file systems have UUIDs to identify them, you can identify a further file system you want to share using its file system ID. The result is that the `fsid` option is set to that value (`fsid=???`). If you prefer, you can identify a file system as the root of your shared file systems (`fsid=0`).

+   4.  Click the **User Access** tab, then select any of the following options:

+   *   **Treat the remote root user as local root** — If this option is on, it enables the remote root user host accessing your shared directory to save and modify files as though he or she were the local root user. Having this on is a security risk, since the remote user can potentially modify critical files. (This sets the `no_root_squash` option.)

+   *   **Treat all client users as anonymous users** — When this option is on, you can indicate that particular user and group IDs be assigned to every user accessing the shared directory from a remote computer. Enter the user ID and group ID you want assigned to all remote users. (This sets the `anoniuid` and `anongid` options to the numbers you choose.)

+   5.  Click **OK**. The new shared directory appears in the NFS Server Configuration window.

At this point, the configuration file (`/etc/exports`) should have the shared directory entry created in it. To turn on the NFS service and make the shared directory available, type the following from a Terminal window as root user:

+   1.  To immediately turn on NFS, type:

```
# service nfs start
```

+   2.  To permanently turn on the NFS service, type:

```
# chkconfig nfs on
```

+   3.  If you have a firewall configured, you must ensure that UDP ports 111 and 2049 are accepting requests. (See Chapter 14 for information on configuring your firewall.)

The next few sections describe the `/etc/exports` file you just created. At this point, a client can only use your shared directory if he mounts it on his local file system. Refer to the “Using NFS file systems” section later in this chapter.