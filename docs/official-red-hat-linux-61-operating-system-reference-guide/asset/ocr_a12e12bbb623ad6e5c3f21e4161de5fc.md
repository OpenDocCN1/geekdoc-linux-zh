+   - `--server <server>`
+       Server from which to install (hostname or IP).
+   - `--dir <dir>`
+       Directory containing the Red Hat installation tree.

For example:
`nfs --server <server> --dir <dir>`

# **CD-ROM**

Install from the first CD-ROM drive on the system.
For example:
`cdrom`

# **hard drive**

Install from a Red Hat installation tree on a local drive, which must be either VFAT or ext2.

+   - `--partition <partition>`
+       Partition to install from (such as, sdb2).
+   - `--dir <dir>`
+       Directory containing the Red Hat installation tree.

For example:
`harddrive --partition <partition> --dir <dir>`

# **F.5.7 keyboard**

**keyboard (required)**