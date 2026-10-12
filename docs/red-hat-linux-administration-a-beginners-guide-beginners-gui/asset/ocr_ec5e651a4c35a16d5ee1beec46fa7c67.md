![](bbox=[0.34, 0.12, 0.67, 0.31])

**Figure 7-1** Manage the file system starting with the root directory.

As the boot scripts run, additional partitions are mounted, adding to the structure of the file system. The mount process overlays a single subdirectory with the directory tree of the partition it is trying to mount. For example, let’s say that /dev/hda1 is the root partition. It has the directory /usr, which contains no files. The partition /dev/hda3 contains all the files that you want in /usr, so you mount /dev/hda3 to the directory /usr. Users can now simply change directories to /usr to see all the files from that partition. The user doesn’t need to know that /usr is actually a separate partition.

Keep in mind that when a new directory is mounted, the mount process hides all the contents of the previously mounted directory. So in the /usr example, if the root partition did have files in /usr before mounting /dev/hda3, those /usr files would no longer be visible. (They’re not erased, of course—once /dev/hda3 is unmounted, the /usr files would become visible once again.)