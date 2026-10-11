By default, the JFS mount option `integrity` is set, which causes metadata changes to be committed to the journal. To change the performance of the JFS file system, use the `nointegrity` mount option. `nointegrity` causes the file system to not be written to the journal. The primary use of this option is to allow for higher performance when restoring a volume from backup media. However, the volume's integrity is not guaranteed if the system abnormally abends. Specify the `integrity` option to remount a volume where the `nointegrity` option was previously specified in order to restore normal behavior.

Linux records an atime, or access time, whenever a file is read. However, this information is not very useful, and it can be costly to track. To get a quick performance boost, simply disable access time updates with the mount option `noatime`.

# Tuning JFS

A performance option that the jfs_tune utility provides is the capability to change the journal's location, which allows you to move the journal to an external device. Changing a journal's location involves the following steps:

+   1. Create a journal on an external device /dev/hda2:
+      ```
+      # mkfs.jfs -J journal_dev /dev/hda2
+      ```

+   2. Attach the external journal to the file system, which is located on /dev/hdb1:
+      ```
+      # jfs_tune -J device=/dev/hda2 /dev/hdb1
+      ```

# JFS Utilities

The following JFS utilities are available in the jfsutils package:

+   - `jfs_fsck`. Initiates a replay of the JFS transaction log and checks and repairs a JFS formatted device.

+   - `jfs_mksfs`. Creates a JFS formatted partition.

+   - `jfs_logdump`. Dumps the journal log of a JFS formatted device.

+   - `jfs_tune`. Adjusts tunable file system parameters on JFS.