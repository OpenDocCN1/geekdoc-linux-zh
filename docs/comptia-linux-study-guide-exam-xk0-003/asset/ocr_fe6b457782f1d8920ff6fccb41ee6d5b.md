system, you slide the frame with hard drive into the mounting bay. You can get by with one of each component, but it's best to buy one frame for each hard drive, which effectively raises the media cost. From a Linux software point of view, removable hard disk systems work like regular hard disks or other removable disk systems, like Zip disks. The disks are likely to be partitioned, and the partitions are likely to hold ordinary Linux filesystems.

Tapes are accessed via special tape device files, such as /dev/st0 or /dev/nst0 (for devices that use SCSI drivers) or /dev/ht0 or /dev/nht0 (for devices that use PATA drivers). Many backup programs, such as tar, can access the tape device file directly.

Optical discs require special programs to write, but they can be mounted much like hard disks. The programs used to write to optical discs are described in the upcoming section \"Writing to Optical Discs.\" 

# ## Common Backup Programs

Linux supports several backup programs. Some are tools designed to back up individual files, directories, or computers. Others build on these simpler tools to provide network backup facilities. Basic backup programs include tar (described earlier in this chapter in \"Handling Tarballs\"), dump, and cpio. ARKEIA (http://www.arkeia.com) and BRU (http://www.tol1sgroup.com) are two commercial backup packages that provide explicit network support and GUI front-ends. AMANDA (http://www.amanda.org) is a network-\-capable scripting package that helps tar or dump perform a backup of an entire network. When dealing with tapes, the mt program is useful for controlling the tape hardware. This section provides a look at the cpio, dump, restore, and mt tools for performing backups.

# ### The cpio Utility

The cpio program is similar in principle to tar; it creates an archive file that contains copies of the original files. You can create a cpio archive on your hard disk or direct cpio to create the archive directly on a tape device. The cpio utility has three operating modes:

**Copy-out mode** This mode, activated by using the -o or --create option, creates an archive and copies files into it.

**Copy-in mode** You activate copy-in mode by using the -i or --extract option. This mode extracts data from an existing archive. If you provide a filename or a pattern to match, cpio will extract only the files whose names match the pattern you provide.

**Copy-pass mode** This mode is activated by the -p or --pass-through option. It combines the copy-out and copy-in modes, enabling you to copy a directory tree from one location to another.

![](bbox=[0.14, 0.88, 0.25, 0.96])

The names for the copy-out and copy-in modes are confusing.

In addition to the options used to select the mode, cpio accepts many other options, the most important of which are summarized in Table 7.11. To back up a computer, you'll