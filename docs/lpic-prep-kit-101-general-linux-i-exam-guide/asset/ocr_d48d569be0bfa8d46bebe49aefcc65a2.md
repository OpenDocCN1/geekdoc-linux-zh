Answer *a* is incorrect; you must tell `mkfs` the type of the filesystem to apply to the partition. **Answer b is correct; the `mkfs` command does not need to know the number of bytes on the partition.** Answer *c* is incorrect; you must tell `mkfs` which partition to format. Answer *d* is incorrect; you must tell `mkfs` how many blocks are present on the partition you are formatting.

+   6.  The inode structure contains all of the following, except
+      a.  Filename
+      b.  Access permissions
+      c.  The file's owner
+      d.  Date and time the file was last accessed

**Answer a is correct; the filename is stored in the directory, not the inode structure.** Answer *b* is incorrect; the permission block is stored in the inode. Answer *c* is incorrect; both the owner and group names are stored in the inode. Answer *d* is incorrect; the times the file was last accessed and last modified are stored in the inode.

+   7.  You want to run `fsck` on your root partition. Which of the following will not enable you to do this?
+      a.  Boot with a floppy and then run `fsck` on root.
+      b.  Start in single-user mode and then run `fsck`.
+      c.  Use `fsck` with the `-t` option to force the check.
+      d.  Configure `fsck` to run at boot.

Answer *a* is incorrect; if you boot from a floppy, you will be able to run `fsck`. Answer *b* is incorrect; booting into read-only, single-user mode will enable you to run `fsck` on root. **Answer c is correct; there is no -t option to force fsck to run on a mounted filesystem.** Answer *d* is incorrect; the most common time to run `fsck` on root is during boot.

+   8.  You need to prepare a report for your supervisor with the total space used by each user. What command would help you prepare this report?
+      a.  `du`
+      b.  `df`
+      c.  `ls -l`
+      d.  `wc`

**Answer a is correct; the `du` command displays the amount of disk space being used.** Answer *b* is incorrect; the `df` command shows the amount of space used on an entire partition. Answer *c* is incorrect; this displays a list of all the files and their attributes. Answer *d* is incorrect; the `wc` command counts the words, characters, and lines in a file.