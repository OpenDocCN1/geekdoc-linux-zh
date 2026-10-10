+   - `-a` — Mount all file systems in `/etc/fstab` (except those indicated as `noauto`).
+   - `-f` — This goes through the motions of (fakes) mounting the file systems on the command line (or in `/etc/fstab`). Used with the `-v` option, `-f` is useful for seeing what mount would do before it actually does it.
+   - `-P` — When used with `-a`, you tell mount to fork off a new incarnation of mount for each file system listed to be mounted in the `/etc/fstab` file. An advantage of using this option, as it relates to NFS shared directories, is that other file systems can be mounted if an NFS file system isn't immediately available. This option should not be used, however, if the order of mounting is important (for example, if you needed to mount `/mnt/pco` and then `/mnt/pco/axctic`).
+   - `-r` — Mounts the file system as read-only.
+   - `-w` — Mounts the file system as read/write. (For this to work, the shared file system must have been exported with read/write permission.)

The next section describes how to make the mount more permanent (using the `/etc/fstab` file) and how to select various options for NFS mounts.

# Automatically mounting an NFS file system

To set up an NFS file system to mount automatically each time you start your Fedora system, you need to add an entry for that NFS file system to the `/etc/fstab` file. The `/etc/fstab` file contains information about all different kinds of mounted (and available to be mounted) file systems for your Fedora system.

The format for adding an NFS file system to your local system is the following:

```
host:directory  mountpoint  nfs  options  0  0
```

The first item (*host:directory*) identifies the NFS server computer and shared directory. *mountpoint* is the local mount point on which the NFS directory is mounted, followed by the file system type (*nfs*). Any options related to the mount appear next in a comma-separated list. (The last two zeros just tell Fedora not to do \_dump\_ backups of the contents of the file system and not to run \_fsck\_ on the file system.)

> NOTE: System-created entries in `/etc/fstab` for hard disk mounts will likely show a UUID, or universal identifier, in place of the *host:directory* entry—for example, `UUID=8366237bb-d845-4117-a1b2-e286d056f15`. You can view these entries under `/dev/disk/by-uuid`.

The following are two examples of NFS entries in `/etc/fstab`:

```
maple:/home/chris/files  /mnt/maple  nfs  size=8192,wsize=8192  0  0
oak:/apps  /oak/apps  nfs  noauto,ro  0  0
```