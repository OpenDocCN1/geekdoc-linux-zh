of these directories, with the exception of /etc, have namesakes within /usr, as in /usr/bin and /usr/lib. The binary and library directories that exist directly off of the root directory hold critical system files—those that Linux needs to boot and operate as a bare-bones system. The namesakes of these directories under /usr hold program files and libraries that are less critical for basic functioning, such as word processors, Web browsers, and the X Window System. The /usr/share directory also deserves mention; it holds miscellaneous shared data files, such as fonts, as well as ancillary data files for specific programs. The /proc directory, described in more detail in Chapter 3, holds pseudo-files that provide information on, and in some cases a means to control, low-level hardware devices.

# # Linux Filesystem Options

Linux's standard filesystem for most of the 1990s was the second extended filesystem (ext2 or ext2fs), which was the default filesystem for most distributions. Ext2fs supports all the features required by Linux (or by Unix-style OSs in general) and is well tested and robust.

> ### Real World Scenario
> 
> #### When to Create Multiple Partitions
> 
> One problem with splitting off lots of separate partitions, particularly for new administrators, is that it can be difficult to settle on appropriate partition sizes. As noted in Table 6.1, the appropriate size of various partitions can vary substantially from one system to another. For instance, a workstation is likely to need a fairly small /var partition (say, 100MB), but a mail or news server might need a /var partition that's gigabytes in size. Guessing wrong is annoying. You'll need to resize your partitions (which is tedious and dangerous) or set up symbolic links between partitions so that subdirectories on one partition can be stored on other partitions.
> 
> For this reason, I generally recommend that new Linux administrators try simple partition layouts first. The root (/) partition is required, and swap is a very good idea. Beyond this, /boot can be very helpful on hard disks of more than 8GB with older distributions or BIOSs but is seldom needed with computers or distributions made since 2000. An appropriate size for /home is often relatively easy for new administrators to estimate, so splitting it off generally makes sense. Beyond this, I recommend that new administrators proceed with caution.
> 
> As you gain more experience with Linux, you may want to break off other directories into their own partitions on subsequent installations or when upgrading disk hardware. You can use the du command to learn how much space is used by files within any given directory.

Ext2fs has one major problem, though: if the computer is shut down improperly (because of a power outage, system crash, or the like), it can take several minutes for Linux to verify an ext2fs partition's integrity when the computer reboots. This delay is an annoyance at best,