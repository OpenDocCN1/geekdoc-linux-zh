Use the ps command again to see a list of the running processes. The top utility is no longer running.
Caution: Be very careful when using the kill command. If you kill a process that the operating system needs, you can cause disastrous results!

In this section, you learned about several utilities to monitor and maintain the system. You learned to use the dd command to copy files and duplicate floppy disks. You used the mkfs command to create a file system on a floppy disk and used the fdformat command to perform a low-level format on a floppy disk. You learned to query the partition containing the root device with the rdev command. Also, you learned to monitor disk, memory, and CPU usage with the df, du, top, and free commands. Finally, you learned to run programs in the background with the & operator, to list all running processes with the ps command, and to terminate processes no longer needed with the kill command. In the next section you learn about utilities that format text files.

# SUMMARY

+   • UNIX utilities are classified into seven major function areas dictated by user needs: file processing, networking, communications, system status, programming, source code management, and miscellaneous tasks.

+   • Utility programs are distinguished from other operating system programs, because they are "add-ons" and not a part of the UNIX shells, nor a component of the "kernel."

+   • Because utility programs are executed by entering their names on the command line, these programs are commonly referred to as commands.

+   • The dd command possesses a rich set of options that allow it to handle copies when other copying methods fail.

+   • To make a bootable floppy disk, you use four utility programs: rdev, mkfs, fdformat, and the dd commands.

+   • The rdev command queries and sets the root device. The root device is the hard disk partition that houses UNIX’s root file system.

+   • The fdformat command low-level formats a floppy to ensure that the media is without defect and is writable to set up a file system.

+   • The mkfs utility sets up a file system and works in tandem with fdformat to prepare the floppy disk for use.

+   • The df utility checks and reports on free disk space.

+   • The du command checks for disk usage (consumption).