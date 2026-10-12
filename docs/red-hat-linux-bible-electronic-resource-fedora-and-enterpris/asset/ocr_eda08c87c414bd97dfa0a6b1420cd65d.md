+   • **Field 1** — The name of the device representing the file system. The word `none` is often placed in this field for file systems (such as `/proc` and `/dev/pts`) that are not associated with special devices. Notice that this field can now include the `LABEL` option. Using `LABEL`, you can indicate a universally unique identifier (UUID) or volume label instead of a device name. The advantage to this approach is that, since the partition is identified by volume name, you can move a volume to a different device name and not have to change the `fstab` file.

+   • **Field 2** — The mount point in the file system. The file system contains all data from the mount point down the directory tree structure, unless another file system is mounted at some point beneath it.

+   • **Field 3** — The file system type. Valid file system types are described in the “Supported file systems” section earlier in this chapter.

+   • **Field 4** — Options to the mount command. In the preceding example, the `noauto` option prevents the indicated file system from being mounted at boot time. Also, `ro` says to mount the file system read-only (which is reasonable for a CD-ROM player). Commas must separate options. See the mount command manual page (under the `-o` option) for information on other supported options.

> **TIP:** Normally, only the root user is allowed to mount a file system using the mount command. However, to allow any user to mount a file system (such as a file system on a floppy disk), you could add the `user` option to Field 4 of `/etc/fstab`.

+   • **Field 5** — The number in this field indicates whether or not the indicated file system needs to be dumped. A number 1 assumes that the file system needs to be dumped. A number 2 assumes that the file system doesn’t need to be dumped.

+   • **Field 6** — The number in this field indicates whether or not the indicated file system needs to be checked with `fsck`. A number 1 assumes that the file system needs to be checked. A number 2 assumes that the file system doesn’t need to be checked.

If you want to add an additional local disk or an additional partition, you can create an entry for the disk or partition in the `/etc/fstab` file. To get instructions on how to add entries for an NFS file system, see Chapter 18.

# ### Using the mount command to mount file systems

Your Red Hat Linux system automatically runs `mount -a` (mount all file systems) each time you boot. For that reason, you would typically only use the mount command for special situations. In particular, the average user or administrator uses mount in two ways:

+   • To display the disks, partitions, and remote file systems that are currently mounted.
+   • To temporarily mount a file system.