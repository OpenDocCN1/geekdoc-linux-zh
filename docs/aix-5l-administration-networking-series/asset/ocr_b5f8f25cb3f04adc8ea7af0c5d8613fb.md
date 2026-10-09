# The backup and restore Facility Commands

IBM has also added the backup and restore facility to AIX, which allows you to back up by filename or by i-node. The **backup** utility is the most common way of backing up file systems using a rotating backup schedule. The command is intuitive to use, and restoration of data is easier than with some other methods found on the system. The section "Backup Schedules and Rotation," later in this chapter, details the use of the backup command.

# The mkcd command

The **mkcd** command was new to AIX starting with 4.3.3. The requirements to make system backups using the **mkcd** command are quite extensive. First of all, you must have enough disk space to hold the contents of the CD-ROM or DVD on disk, which is 645MB for a CD-ROM and 8.8GB for a DVD. Additionally, IBM uses a proprietary DVD case that has an angled slot for the write-protect hole. I found this out the hard way when the DVDs that I bought would not let me write on them because the drive insisted they were write-protected. So just be aware that you will have to buy your DVDs from an IBM source. For more details on the **mkcd** command, see "Requirements for Writable CD and DVD Drives," later in this chapter.

# The tar Command

The **tar** command is as old as UNIX. *Tar (the name stands for tape archive)* is a very flexible tool. This is the most widely used archiving tool because it is easy and intuitive to use and it has few failures. "Network Backups," later in the chapter, has more information on using the **tar** command.

# The cpio Command

Backups made using **cpio** are among the more difficult backups to restore back on the system if the exact command parameters are not known. The **cpio** command stands for *copy input/output*. I mostly use **cpio** when I move data around within the machine. The section "Other Backup Utilities," later in this chapter, shows some of the more common uses for the **cpio** command.

# The pax Command

The **pax** utility now supports files larger than 2GB under AIX 5L, yet **tar** and **cpio** do not. IBM now uses **pax** with the **snap** command for gathering system information for IBM support. The nice thing about **pax** is that it can read both **tar** and **cpio** archives. See "Other Backup Utilities," later in the chapter, for more on using the **pax** command.

# The dd Command

The **dd** command works on data at the byte level. This command has conversion capabilities that no other command on the system can perform. One of the more