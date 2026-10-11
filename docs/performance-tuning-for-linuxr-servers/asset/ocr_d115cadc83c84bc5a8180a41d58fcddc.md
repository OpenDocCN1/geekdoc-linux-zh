+   2. Add a journal file to the existing Ext2d file system you want to convert by running the tune2fs program with the -j option. You can run tune2fs on a mounted or unmounted Ext2 file system. For example, if /dev/hdb3 is an Ext2 file system, the following command creates the log:
+   
+   # tune2fs -j /dev/hdb3

If the file system is mounted, a journal file named .journal is placed in the root directory of the file system. If the file system is not mounted, the journal file is hidden. (When you mount an Ext3 file system, the .journal file appears. The .journal file can indicate that the file system is indeed of type Ext3.)

+   3. Change the entry for /dev/hdb3 in the /etc/fstab file from ext2 to ext3.

+   4. Reboot and verify that the /dev/hdb3 partition has type Ext3 by typing **mount** and examining the output. The output should include an entry like the following:
+   
+   # mount
+   
+   /dev/hdb3 on /test type ext3 (rw)

# Using a Separate Journal Device on an Ext3 File System

The first thing you need to do to use an external journal for an Ext3 file system is to issue the `mkfs` command on the journal device. The block size of the external journal must be the same block size as the Ext3 file system. In the following example, the /dev/hda1 device is used as the external log for the Ext3 file system:

# mkfs.ext3 -b 4096 -O journal_dev /dev/hda1

# mkfs.ext3 -b 4096 -J device=/dev/hda1 /dev/hdb1

# Ext2/Ext3 Utilities

The e2fsprogs package contains various utilities for use with Ext2 and Ext3 file systems. The following is a short description of each utility:

+   * **badblocks**. Searches for bad blocks on a device.
+   * **chattr**. Changes the file attributes on an Ext2 or Ext3 file system.