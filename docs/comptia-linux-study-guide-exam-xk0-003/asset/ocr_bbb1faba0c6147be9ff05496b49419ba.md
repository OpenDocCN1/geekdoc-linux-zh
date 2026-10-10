# # Review Questions

+   1. Typing `fdisk -1 /dev/hda` on an x86 Linux computer produces a listing of four partitions: `/dev/hda1`, `/dev/hda2`, `/dev/hda5`, and `/dev/hda6`. Which of the following is true?
+   
+   A. The disk contains two primary partitions and two extended partitions.
+   B. Either `/dev/hda1` or `/dev/hda2` is an extended partition.
+   C. The partition table is corrupted; there should be a `/dev/hda3` and a `/dev/hda4` before `/dev/hda5`.
+   D. If you add a `/dev/hda3` with `fdisk`, `/dev/hda5` will become `/dev/hda6`, and `/dev/hda6` will become `/dev/hda7`.

+   2. Which of the following pieces of information can `df` *not* report?
+   
+   A. How long the filesystem has been mounted
+   B. The number of inodes used on an ext3fs partition
+   C. The filesystem type of a partition
+   D. The percentage of available disk space used on a partition

+   3. A new Linux administrator plans to create a system with separate `/home`, `/usr/local`, and `/etc` partitions. Which of the following best describes this configuration?
+   
+   A. The system won't boot because `/etc` contains configuration files necessary to mount nonroot partitions.
+   B. The system will boot, but `/usr/local` won't be available because mounted partitions must be mounted directly off their parent partition, not in a subdirectory.
+   C. The system will boot only if the `/home` partition is on a separate physical disk from the `/usr/local` partition.
+   D. The system will boot and operate correctly, provided each partition is large enough for its intended use.

+   4. What mount point should you associate with swap partitions?
+   
+   A. `/\`
+   B. `/swap`
+   C. `/boot`
+   D. None

+   5. You run Linux's `fdisk` and modify your partition layout. Before exiting from the program, though, you realize that you've been working on the wrong disk. What can you do to correct this problem?
+   
+   A. Nothing; the damage is done, so you'll have to recover data from a backup.
+   B. Type `w` to exit from `fdisk` without saving changes to disk.
+   C. Type `q` to exit from `fdisk` without saving changes to disk.
+   D. Type `u` repeatedly to undo the operations you've made in error.