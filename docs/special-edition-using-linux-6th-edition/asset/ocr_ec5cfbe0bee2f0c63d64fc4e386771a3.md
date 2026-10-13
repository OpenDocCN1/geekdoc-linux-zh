This is often the most frightening thing a user who is new to Linux will encounter, but it is nothing to be feared. In most cases, you can simply run `fsck -y /dev/<harddrive>`, which tells fsck to go ahead and take care of things without intervention. Manually repairing a filesystem is beyond the scope of this book and requires extensive knowledge of how the ext2 filesystem works. At any rate, the worst that could happen is that you will need to reinstall everything. The question “You do have a backup, don’t you?” comes to mind at this point.

If worse comes to worst, you can still boot from a Linux boot floppy and save your data files before reinstalling the files on the corrupt partition. This, by the way, is the reason most seasoned systems administrators prefer to put the `/home` directory on a separate partition—to help isolate and protect it somewhat and to make running fsck manually easier.

The Linux community is working on a successor to the ext2 filesystem that will be a journaling filesystem. If you are familiar with SQL databases, this is like the transaction logging that enables unfinished transactions to be rolled back and finished transactions that have been committed to be ignored. Running fsck on ext2 can take a long time on a large partition. With a journaling filesystem, this would take a very short time (typically less than 10 percent of the time it takes to check a nonjournaling filesystem).

To run fsck manually as a preventive measure (monthly, if you never shut your system down), perform the following steps:

+   1. Enter maintenance (single user mode) by typing the following from a command prompt:
+   
+      `init 1`
+   
+   2. When the system reaches runlevel 1, it prompts you for root's password; enter it to log in.
+   
+   3. You need to unmount mounted filesystems you want to check. The root filesystem cannot be unmounted, so it needs to be mounted read-only. Assuming you have `/home` mounted as `/dev/hda2` and the root filesystem as `/dev/hda1`, issue the following command:
+   
+      `umount /home`
+   
+      Alternatively, umount `-a` unmounts all filesystems except root:
+   
+      `mount -n -o remount,ro /`
+   
+      If you get the error message `cannot unmount <filesystem>, <filesystem> in use`, you need to identify the process running on that filesystem or the user (root) that cd'd into that filesystem, and kill the process or cd out of the filesystem.
+   
+   4. Run fsck on the two partitions:
+   
+      `fsck -f /dev/hda2`
+   
+      `fsck -f /dev/hda1`
+   
+   5. When the filesystem checks finish, remount the filesystems:
+   
+      `mount -n -o remount,rw /`
+   
+      `mount /home`
+   
+      Alternatively, `mount -a` mounts all filesystems designated to be automatically mounted at bootup.