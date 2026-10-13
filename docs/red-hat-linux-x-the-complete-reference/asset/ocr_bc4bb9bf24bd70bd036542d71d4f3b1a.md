# Journaling

The ext3 and ReiserFS file systems introduced journaling capabilities to Linux systems. Journaling provides for fast and effective recovery in case of disk crashes, instead of using e2fsck or fsck. With journaling, a log is kept of all file system actions, which are placed in a journal file. In the event of a crash, Linux only needs to read the journal file and replay it to restore the system to its previous (stable) state. Files that were in the process of writing to the disk can be restored to their original state. Journaling also avoids lengthy fsck checks on reboots that occur when your system suddenly loses power or freezes and has to be restarted physically. Instead of using fsck to manually check each file and directory, your system just reads its journal files to restore the file system.

Keeping a journal entails more work for a file system than a nonjournal method. Though all journaling systems maintain a file system's directory structure (what is known as the metadata), they offer various levels of file data recovery. Maintaining file data recovery information can be time-consuming, slowing down the file system's response time. At the same time, journaling systems make more efficient use of the file system, providing a faster response time than the nonjournaled ext2 file system.

There are other kind of journaling file systems you can use on Linux. These include ReiserFS, JFS, and XFS. ReiserFS, named after Hans Reiser, provides a completely reworked file system structure based on journaling (www.namesys.com). Most distributions also provide support for ReiserFS file systems. JFS is the IBM version of a journaling file system, designed for use on servers providing high throughput such as e-business enterprise servers (oss.software.ibm.com/developerworks/opensource/jfs/). It is freely distributed under the GNU public license. XFS is another high-performance journaling system developed by Silicon Graphics (oss.sgi.com/projects/xfs/). XFS is compatible with RAID and NFS file systems.

# ext3 Journaling

Journaling is supported in the Linux kernel with ext3. The ext3 file system is also fully compatible with the earlier ext2 version it replaces. To create an ext3 file system, you use the mkfs.ext3 command. You can even upgrade ext2 file systems to ext3 versions automatically, with no loss of data or change in partitions. This upgrade just adds a journal file to an ext2 file system and enables journaling on it, using the tune2fs command. Be sure to change the ext2 file type to ext3 in any corresponding /etc/fstab entries. The following example converts the ext2 file system on /dev/hda3 to an ext3 file system by adding a journal file (-j).

```
tune2fs -j /dev/hda3
```

Though the ext3 file system maintains full metadata recovery support (directory tree recovery), it offers various levels of file data recovery. In effect, you are trading off less file data recovery for more speed. The ext3 file system supports three options: writeback, ordered, and journal. The default is writeback. The writeback option provides only metadata recovery, no file data recovery. The ordered option supports limited file data recovery, and the journal option provides for full file data recovery. Any files in the process of being changed during a crash will be recovered. To specify an ext3 option, use the data option in the mount command.

```
data=ordered
```

# ReiserFS

Though journaling is often used to recover from disk crashes, a journal-based file system can do much more. The ext3, JFS, and XFS file systems only provide the logging operations used in recovery, whereas ReiserFS uses journaling techniques to completely rework file system operations. In ReiserFS, journaling is used to read and write data, abandoning the block structure used in traditional Unix and Linux systems. This gives it the capability to access a large number of small files very quickly, as well as use only the amount of disk space they need. However, efficiency is not that much better with larger files.