11. You've added a new disk to a computer that already uses LVM. You've partitioned the new disk and used pvcreate on its one partition in preparation for adding it to your existing LVM. What command should you use to add this partition (/dev/sdb1) to your existing biglvm volume group?

+   A. pvdisplay /dev/sdb1
+   B. vgcreate biglvm /dev/sdb1
+   C. vgextend biglvm /dev/sdb1
+   D. lvextend biglvm /dev/sdb1

12. Which of the following is a GUI tool that supports resizing several filesystems, including FAT, ext2fs, and ReiserFS?

+   A. QTParted
+   B. GNU Parted
+   C. Part
+   D. cfdisk

13. Which of the following options is used with fsck to force it to use a particular filesystem type?

+   A. -A
+   B. -N
+   C. -t
+   D. -C

14. Which of the following utilities would create the following display?

```
total used free shared buffers cached
Mem: 256452 251600 4852 0 10360 130192
-/+ buffers/cache: 111048 145404
Swap: 515100 1332 513768
```

+   A. mt
+   B. df
+   C. swapon
+   D. free

15. What will be the result of the root user running the following command?
# mount /dev/sdc5 /home2

+   A. The contents of /home2 will be mounted on /dev/sdc5 with the default filesystem used and a prompt for options will appear.
+   B. The contents of /home2 will be mounted on /dev/sdc5 with the filesystem type auto-detected and default options used.
+   C. The contents of /dev/sdc5 will be mounted on /home2 with the filesystem type auto-detected and default options used.
+   D. The contents of /dev/sdc5 will be mounted on /home2 with the default filesystem used and a prompt for options will appear.