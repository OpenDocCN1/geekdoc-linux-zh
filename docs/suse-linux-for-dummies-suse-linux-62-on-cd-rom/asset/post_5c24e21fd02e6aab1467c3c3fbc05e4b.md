
# Making the file system

Every partition is simply an empty space with a beginning and an end. Unless the partition is being used for swap space, you have to put some type of file system on the partition before it becomes useful. The `mkfs` command is used to create the file system on the partition. Normally, the file system is a native Linux file system, which at this time is called ext2. The Linux version has been nicely streamlined and requires hardly any input. To create a file system on the disk partition sda1, for example, you enter the following command:

```
mkfs -t ext2 /dev/sda1
```

If you want to create an MS-DOS file system on the disk partition, you use this command:

```
mkfs -t mdsos /dev/sda2
```

You can continue to execute `mkfs` commands to create file systems for every partition on your new disk. Or you can leave some partitions without file systems (for future use), as long as you remember to perform the `mkfs` command on them before attaching them to your file system by using either the mount command or the /etc/fstab table.

Congratulations! Your disk has been physically added to your system and partitioned, and you've added file systems to it. Now the disk is ready to join the rest of the file system — simply use the mount command or the /etc/fstab file, which we describe earlier in this chapter.

# Living with Floppy Disks

Floppy disks are treated a little differently than hard disks, mostly due to their size and fragility. They are not normally mounted and used for hours and days on to hold gigabytes of data. More often, floppy disks are used to transfer data to another computer or back to a few files.

Although you can create Linux file systems on floppy disks, using them in other ways is more advantageous. For example:

- Floppy disks can be mounted as DOS file systems, which can then be accessed with the standard Linux utilities such as cp and ls.
- Floppy disks can be used as raw devices with commands such as tar and cp.
- Floppy disks can permit the use of special utilities that read and write to disks.

# Chapter 13: File System Management

On Linux systems, the block special file for the first floppy drive is /dev/fd0. The default density is 1,440 kilobytes. We assume that you are using standard, 3-½-inch preformatted floppy disks.

The following commands mount a floppy disk and write a DOS file to it; (replace any-dosfile.txt with a real filename):

```
mount /dev/fd0 /floppy
cp any-dosfile.txt /floppy
umount /floppy
```

![](img/96a9ce6a13d8d15ed05f867f41574278_258_0.png)

This is one way to move files back and forth to an MS-DOS (Windows 3.1, 98, or NT) machine. You can add the file to a floppy disk, insert the floppy in the MS-DOS machine, and the MS-DOS machine can read the file from the disk. By mounting a floppy disk created on an MS-DOS machine, you can read and manipulate the files using Linux.

The mtools package installed on your system enables you to access DOS disks and files without first mounting the floppy disk and adding it to your file system. Table 13-1 presents some mtools commands, which are probably familiar to users.

| Table 13-1 mtools Utilities | What It Does |
| :--- | :--- |
| mformat | Formats a floppy disk in DOS format |
| mlabel | Labels a floppy disk |
| mcd | Changes the current directory on a floppy disk |
| mdir | Lists the directory contents on a floppy disk |
| mtype | Displays a DOS file's contents |
| mcopy | Copies files between a DOS floppy disk and Linux |
| mdel | Deletes files on a floppy disk |
| mren | Renames files on a floppy disk |
| mmd | Creates a subdirectory on a floppy disk |
| mrd | Removes a directory from a floppy disk |
| mattattrib | Changes file attributes |

# Configuring CD-ROM

You treat CD-ROM drives similar to — not exactly like — disk drives. The special file for CD-ROMs in Linux is usually /dev/cdrom, /dev/hdc, /dev/hdb, or /dev/sr0, depending on factors such as the CD-ROM's type, how it is connected to the controller, and its device number.

![](img/96a9ce6a13d8d15ed05f867f41574278_259_0.png)

The most common type of CD-ROM is ATAPI, and Linux recognizes SCSI CD-ROMs normally. If you installed the system, the CD-ROM will have been recognized by Linux and is probably called /dev/cdrom.

We mention that CD-ROMs are "not exactly like" other drives because they are read-only (which means you can't change their contents) and typically have only one file system. Therefore you don't partition a CD-ROM, nor do you make a file system before mounting it. You simply have to mount where you want the CD-ROM which it is attached to. We assume your CD-ROM drive is /dev/cdrom, which is really just a pointer to another special device. This extra pointer (called a link) enables you to call the CD-ROM by the name /dev/cdrom instead of having to call it /dev/sda or /dev/hdc on some systems (because it happens to be an IDE-based device).

Following is the command to mount a CD-ROM on your Linux system:

```
mount -r -t iso9660 /dev/cdrom /cdrom
```

Now you know about every type of disk storage that you'll see on a Linux system. You know how to identify the types of disk storage and partition them. You also know how to create file systems for them and how to mount and dismount file systems while the system is running. The Linux system dismounts file systems automatically when you shut the machine down — if you have put all of the necessary information into the /etc/fstab file — and mounts them when you start the system up. So, as far as disk systems go, you should be all set.

# Chapter 14: Customizing Linux

In This Chapter

- Finding out about different types of memory
- How much RAM your system has
- Checking out the performance of your disks
- Rebuilding your kernel

Your Linux system is a mélange of hardware and software, and you have choices about both. So how do you tune your system for good performance? Follow this chapter, that is.

Tuning operating systems can become a life-consuming task. If you're obsessed with squeezing more from your hardware and software, you won't have time for anything else. Take advantage of the tips in this chapter, take a deep breath, and get on with the rest of your life.

# Tuning Your Linux System

UNIX-like systems don't have many knobs and buttons you can change to make them faster or better. Linux, however, has a few special features that you can tweak for better performance. More importantly, if you follow a few guidelines, you will help your Linux system perform at its best.

# You can never have enough memory

Although too much memory is theoretically possible, most people have too little in their systems. Today, memory is so inexpensive that few excuses justify not having enough. Not having enough RAM is a holdover from memory prices such as $3,000 per megabyte. I paid $400 for 4 kilobytes (.004MB) of main memory about the same time I purchased a pickup truck for $2,000.

![](img/96a9ce6a13d8d15ed05f867f41574278_260_0.png)

# Real versus virtual memory

When we talk about *real memory*, we are referring to the semiconductor RAM (random-access memory) in your machine. You may have as little as 4MB or as much as 32MB of RAM in your machine. Some power users have 1GB (1 billion bytes) of RAM in their PCs.

If semiconductor RAM is the only type of memory you have, Linux and all programs running under Linux have to fit in that RAM. Although 32MB sounds like a lot, it fills up quickly.

Virtual memory uses hard disk drive (which is cheaper than RAM) to make Linux think you have more RAM. Virtual memory offers two big benefits:

- Programs and files can run at the same time.
- Programs and files can exceed the size of actual RAM.

The disk space that simulates real memory is called *swap space*. (When you installed Linux, you were probably asked to set up a swap space.) Here's how the swap space is used:

- When Linux needs more RAM to start a new application or open an application to expand, some disk space may be substituted for the necessary RAM. Existing RAM is copied onto the swap space. This frees RAM for the new data.
- When Linux needs the information from the swap space, it must make room in RAM. Therefore, Linux may write some other program's data to the swap space before recalling data. This is called *demand-paging*, because the data is in RAM only when a *demand* exists for it to be there. Otherwise, data tends to stay on the swap area of the disk.

# Do I have enough RAM?

The `procinfo` and `vmstat` commands can help determine whether you have enough RAM. Using these commands by themselves or with each other can tell you whether you are overutilizing your RAM memory. If so, your CPU is waiting for RAM to be available.

Measuring performance with `vmstat`

The `vmstat` command displays information about memory utilization, the status of the process, the status of the I/O system, and CPU utilization. It also
