A Oh yeah! Remember, when you run a disk formatting utility, you wipe all the data on that disk, so overwriting the superblocks on an existing drive, for example, instantly unhooks all the files and directories that were on that drive previously. Please use these commands judiciously to ensure you don’t get into any trouble!

# Workshop

# Quiz

+   1. Why would you want to mount a disk read-only?
+   2. Why would you specify noatime at mount, and what does it mean?
+   3. If a disk is automatically mounted with mount -a, what does that imply about boot-time?
+   4. Which of the following file types is not supported by Linux: FAT12, OS/2, Plan 9, CP/M, Golden Bow, DRDOS, DOS, or BeOS.
+   5. If you want to have more than four partitions on a disk, will you need to use primary or extended partitions?

# Answers

+   1. Generally, you should always match the access permissions of the peripheral itself. If you’re mounting a CD-ROM, for example, you’d use read-only because your system can’t write CD-ROMs. (If you have a read/write CD-ROM burner, it’s a different story, of course, but even then, if you’re writing a CD-ROM you’ll want to unmount and remount the device to enable writing.)
+   2. On drives that store lots of small files and have frequent access (Usenet archive servers, for example), disabling updates to the access times for the filesystem can improve performance a bit.
+   3. It implies that the disk will also be automatically mounted at boot-time.
+   4. It’s a trick question! All of these are supported by Red Hat Linux 7.2.
+   5. Both, actually. You’ll want to have partitions 1–4 as primary partitions, and all subsequent partitions as extended.

In the next hour, we’ll explore the different options for boot-time operating system selection, focused specifically on LILO and GRUB. Use of these tools enable you to boot into different operating systems as desired, a very handy capability.