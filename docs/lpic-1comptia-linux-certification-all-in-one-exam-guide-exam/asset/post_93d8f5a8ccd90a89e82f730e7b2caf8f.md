
### Figure 5-7 Ubuntu architectures
Get Ubuntu Desktop Edition Download
You can download Ubuntu Desktop Edition online, completely free.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_182_0.png)

## Planning the File System

When planning a Linux implementation, you need to include specifications for how the file system will be created and maintained on the system’s hard disk drive. This is yet another unique aspect of the Linux operating system. When implementing other operating systems, such as Microsoft Windows, you usually create only a single disk partition and format it using the NTFS file system.

With Linux, however, you have many more choices to make. You can customize how your disk will be partitioned and what file system will be used. In this part of the chapter, we’ll discuss the following:

- Choosing a file system
- Planning your partitions

Let’s begin by discussing file systems.

## Choosing a File System

Because you’re a techie, you already know how a hard disk drive works. The drive is made up of multiple aluminum platters each with two read-write heads that are used to read and write data. When conducting disk I/O operations, the operating system needs to know where data is stored, how to access it, and where it is safe to write new information.

This is the job of the file system. It reliably stores data on the hard drive and organizes it in such a way that it is easily accessible. When you use a file browser to navigate through the directories on a hard disk drive and open a file, it’s the file system that makes the entire process possible.

Most Linux distributions offer a wide variety of file systems that you can choose from. In this topic, we’ll review some of the most widely used types:

- ext2
- ext3
- Reiser
- ext4

> **NOTE** You can also use many other file systems with Linux. For example, you can use the XFS file system from Silicon Graphics. You can even use VFAT or NTFS file systems, although NTFS support isn't fully baked yet. We'll discuss creating VFAT and XFS file systems in Chapter 10.

Let's begin by discussing the ext2 file system.

**ext2** The ext2 file system is one of the oldest Linux file systems still available. The acronym ext2 stands for “Second Extended File System.” Originally introduced back in 1993, ext2 stores data in the standard hierarchical fashion used by most other file systems. Data is stored in *files*; files are stored in directories. A directory can contain either files or other directories (subdirectories).

The maximum file size supported in the ext2 file system is 2 terabytes (TB). An ext2 volume can be up to 4TB. File names can be up to 255 characters long. The ext2 file system supports Linux file system users, groups, and permissions (called POSIX permissions). It also supports file compression.

The ext2 file system is a fantastic file system. It's been around long enough for most of its bugs to be worked out. In fact, it's probably the most widely used Linux file system ever implemented. It's also reputed to be the fastest Linux file system available.

However, ext2 has one key weakness that has led to the development of other file systems. This is the fact that ext2 takes a long time to recover if the system shuts down abruptly. When shutting down the Linux system, the operating system first cleanly dismounts the file system, ensuring all pending file system transactions are written to disk before the system shuts off.

The problem arises when the system halts without completing this clean dismount procedure. For example, suppose a power outage occurs and the Linux system shuts off suddenly without going through the proper shutdown procedure. When this happens, it is possible that pending disk transactions weren't completed.

> **TIP** You're using an uninterruptible power supply to keep this from happening, right? If not, do so! I lost data once due to a power outage, and I've sworn to never let it happen again.

To clean up the file system, the ext2 file system will automatically run a program called *e2fsck* the next time the system is booted. This utility tries to fix any problems that were created when the system went down without properly dismounting the disk. If it finds nonallocated files or unclaimed blocks of data, it will write this information in a directory called *lost+found*. By doing this, ext2 tries to ensure that data integrity is maintained in spite of the improper shutdown.

The issue here is that *e2fsck* will analyze the entire file system when this happens, not just the last few files that were in the process of being modified. On a basic Linux system, this can take from 10 to 15 minutes. On an extensive system that has a lot of file system data (such as a network file server), this process can take several hours. It's bad enough that the system went down unexpectedly in the first place; now you have to wait hours for it to start back up again!

Because of this issue, other Linux file systems have started replacing ext2. The first of these is ext3. Let's discuss this file system next.

## ext3

The ext3 file system is an updated version of ext2. In fact, ext3 stands for “Third Extended File System.” The two are so similar that most of the file system utilities used by ext2 are also used by ext3. You can easily upgrade ext2 file systems to ext3. You can even downgrade an ext3 file system to ext2.

However, the ext3 file system offers one key advantage that makes it highly preferable over ext2: *journaling*. Remember that the key disadvantage of ext2 is the fact that it must check the *entire* file system if the system goes down uncleandly. Journaling eliminates this problem.

Before committing a transaction to the *hard disk drive*, the ext3 file system records the transaction to a journal and marks it as *incomplete*. After the disk transaction is complete, the ext3 file system marks the transaction as *complete* in the journal. By doing this, the ext3 file system can keep a log (a *journal*) of the most recent file transactions and whether or not they were actually completed.

In an event such as a power outage occurs that causes the system to shut down without properly dismounting the disk, the ext3 file system will replay the journal when the system comes back up. This allows the file system to verify the data on the disk and bring it back to a consistent state (if possible) using the information stored in the journal. Unlike ext2, the ext3 file system doesn't need to check the entire file system. Because it has a log of the most recent transactions in the journal, the ext3 file system simply checks the transactions that are listed as *incomplete*.

Using journaling, disk recovery time after an improper shutdown takes dramatically less time than that experienced using ext2. Instead of taking hours, the ext3 file system can replay the journal in only a few seconds or minutes, even if the file system is very large.

The disadvantage of ext3 is the fact that the journaling process uses up more system memory and slows down disk I/O operations slightly. However, because it does a better job of ensuring data integrity and does it faster, most system administrators prefer ext3 over ext2 in spite of the slightly decreased performance.

## Reiser

The Reiser file system is an alternative to the ext3 file system. Like ext3, Reiser utilizes journaling to make crash recovery very fast. However, Reiser is a completely different file system from ext2 and ext3, using a dramatically different internal structure. This allows the Reiser file system to support a larger maximum file size of 8TB and maximum volume size of 16TB. In addition, the structure of Reiser allows it to perform much faster than ext2 or ext3.

## ext4

The ext4 file system was released in late 2008. As you might guess, ext4 (Fourth Extended File System) is an updated version of ext3. Just as ext3 is backward compatible with ext2, ext4 is backward compatible with ext3 (and ext2, for that matter). The ext4 file system supports volumes up to 1 exabyte in size and files up to 16 terabytes in size. You can have a maximum of four billion files in an ext4 file system. As with ext2
