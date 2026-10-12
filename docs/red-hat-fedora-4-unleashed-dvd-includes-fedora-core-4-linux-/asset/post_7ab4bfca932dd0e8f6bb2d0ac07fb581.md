
> **CAUTION**
>
> Fedora and Red Hat have modified their supplied version of `fdisk` to limit the number of IDE partitions to 15 to match the limit for SCSI disks. That’s a problem if you already have more than 15 IDE partitions and `fdisk` will simply delete those partitions without warning if you use it! If you have less than 15 partitions, there will be no problem. If this causes a problem for you, compile your own `fdisk` from pristine sources and file a bug report with Fedora/Red Hat.

> **NOTE**
>
> Zip disks are typically delivered with a single partition numbered 4. This has some arcane relevance to Apple computer users, but is of no importance to Linux users who are free to use any valid number they choose.

## The `fdisk` Command

The Linux `fdisk` command edits the partition table.

You must be the superuser (root) before you can run `fdisk` (also said in Linux shorthand as "run `fdisk` as root"). Only hard drives (IDE and SCSI) can be accessed with `fdisk`, and you must use the device name as an argument. USB hard drives are accessed under SCSI emulation and are treated just as if they were SCSI devices. For example, to open `fdisk` and use it on the first IDE hard drive on the system, you would type this:

```
# fdisk /dev/hda
```

and you would see something like this:

```
# fdisk /dev/hda
```

The number of cylinders for this disk is set to 4982. There is nothing wrong with that, but this is larger than 1024, and in certain setups could cause problems with software that runs at boot time:

- 1) software that runs at boot time (e.g., old versions of Lilo)
- 2) booting and partitioning software from other OSes (e.g., DOS FDISK or the OS/2 FDISK)

Pressing the m key displays the help screen as follows:

Command (m for help): m

Command action
- a   toggle a bootable flag
- b   edit bsd disklabel
- c   toggle the dos compatibility flag
- d   delete a partition
- l   list known partition types
- m   print this menu
- n   add a new partition
- o   create a new empty DOS partition table
- p   print the partition table
- q   quit without saving changes
- s   create a new empty Sun disklabel
- t   change a partition's system id
- u   change display/entry units
- v   verify the partition table
- w   write table to disk and exit
- x   extra functionality (experts only)

Pressing the p key will display the volume's partition information as follows (note that your drive information will be different):

Command (m for help): p

```
Disk /dev/hda: 255 heads, 63 sectors, 4982 cylinders
Units = cylinders of 16065 * 512 bytes

Device Boot Start End Blocks Id System
/dev/hda1 * 1 383 3076416 b Win95 FAT32
/dev/hda2 384 387 32130 83 Linux
/dev/hda3 388 1025 5124735 83 Linux
/dev/hda4 1026 4982 31784602+ 5 Extended
/dev/hda5 1026 1042 136521 82 Linux swap
/dev/hda6 1043 1552 4096543+ 83 Linux
/dev/hda7 1553 4102 20482843+ 83 Linux
/dev/hda8 4103 4500 3196903+ 83 Linux
/dev/hda9 4501 4982 3871633+ 83 Linux
```

Older versions of fdisk would default to /dev/hda. The author of fdisk decided that wasn't a good thing, so now you must always type the device name.

> **TIP**
>
> The fdisk command is only dangerous to explore if you write the changes to the partition table. Because you are specifically asked whether you want to do this, poke around to satisfy your curiosity and avoid pressing the w key when you're done; just use q to quit. Armed with this knowledge, do not feel too shy if you're curious about the partition table. But if you really do not want to take a chance on breaking anything, play it safe and use the -l (that's the letter L, not the numeral 1) as in
>
> ```
> # fdisk -l /dev/hda
> ```
>
> fdisk happily prints the contents of the partition table to the screen (often referred to as stdout, or standard output) and exits without placing you in the edit mode.

It is always a good idea to keep a hard copy of your edited partition table. You can redirect the output of `fdisk -l` to a file:

```
# fdisk -l device > mypartitiontable.txt
```

or send it to the printer with:

```
# fdisk -l device | lpr
```

In the first example, a redirector symbol (>) is used to redirect the listing from stdout to a file. In the second example, we used a pipe (|) to send the output directly to the printer (assuming that you have one connected).

Now that you are running fdisk as root, you can create a partition table. We will assume that you have installed a brand-new drive as /dev/hdb (the Primary Slave IDE device) and want to partition the entire drive as a single partition. Launch fdisk with:

```
# fdisk /dev/hdb
```

Use the n key to create a new partition, and fdisk will prompt you for the beginning cylinder:

```
First Cylinder (1-9729, default 1) :
```

Press the Enter key to accept the default of 1. Now, fdisk prompts:

```
Using the default value of 1
Last Cylinder or +size or +sizeM or +sizeK (2-9729, default 9729) :
```

Here, you can give the size in cylinders, the size in kilobytes, the size in megabytes, or accept the default value (which is the last cylinder on the disk). Press the Enter key to accept the default.

```
Using default value of 9729
```

And we are back at the fdisk prompt:

```
Command (m for help) :
```

Enter the w command to write the new partition table to the disk, and fdisk will exit, returning you to the command prompt.

## The parted Command

In the past, Red Hat used a partition editor during its installation process named Disk Druid; the underlying code for Disk Druid has been replaced by GNUparted (also known simply as parted, the name of the command itself). GNUparted is the GNU partition editor and a very powerful utility. You use parted to create, delete, move, resize, and copy ext2, ext3, and FAT32 partitions. Although GNUparted displays a GUI interface during the installation process, it really is a console utility. GNUparted can be used from the command line.

### Creating the File System on the Partitioned Disk

After you have partitioned the disk for a specific file system, you can create the file system on it. In the DOS world, this two-part process is described by DOS as low-level formatting (creating the partitions and partition table) and formatting (creating the file system). In the Unix world, the latter is known as creating a file system. In this section, you learn how to create a file system in Linux.

An unformatted disk storage device (a floppy disk, hard disk drive, or removable media) typically arrives to you with a low-level format, which has been done with a tool such as `fdisk` or `superformat`. Although the disk might have a boot block and partition information, it typically lacks the file structure needed for a file system.

> **NOTE**
> If you are preparing to create a file system on any device other than a floppy disk, examine it with `fdisk` or another utility of your choice and modify the partition table accordingly (following the instructions you saw in the preceding sections of this chapter).

To create the file system structure, you need to do what is sometimes referred to as a high-level format. For FAT file systems, this is accomplished by the `format` command. In Linux, you use the `mke2fs -j` command to create an ext3 file system.

> **NOTE**
> If you are creating a Reiser file system, use the `mkreiserfs` command. To create a DOS file system, use the `mkdosfs` command. Other commands for other file systems include
>
> - `mkfs.bfs` — The SCO file system
> - `mkfs.ext2` — The ext2 file system
> - `mkfs.minix` — The minix file system
> - `mkfs.msdos` — The MS-DOS file system
> - `mkfs.vfat` — The FAT32 file system

### Using mke2fs to Create the File System

The `mke2fs` command is used to create both the ext2 and the ext3 file systems. At its simplest, the command is used as:

```
# mke2fs partition
```

such as:

```
# mke2fs /dev/hdc4
```

Here are some of the most useful options for `mke2fs`:

- `-c` — This option checks for bad blocks during file system creation.
- `-N` — This option overrides the default number of inodes created. (The default number is usually a good choice, but you might need to use this option to allow additional usable disk space.)
- `-m` — This option frees up some space on the disk, but you do so at your peril. By default, the system allocates 5% of the blocks to the superuser—to be used in file recovery during `fsck`. You can lower that allocation, but you might not leave enough blocks for `fsck` to recover enough files.
- `-L` — This option gives the volume a label, which is useful if you need to be reminded what the file system is used for; it also provides some flexibility in identifying volumes in `/etc/fstab`.
- `-S` — This option is a last-ditch effort for recovering a broken file system; it writes only the superblock and descriptors, leaving the information in the inodes unchanged. Always run `fsck` after using this option.

As you can see, `mke2fs` offers a few options to make more space available for the regular users. But that extra space always comes from the superuser’s space for recovering damaged files. The default settings accommodate most users, so think carefully before using one of these options. Hard disks are getting less expensive all the time, so adding another might be a better solution.

### Using `mkfs.ext3`

To make a new `ext3` file system, you use the `mke2fs` command with the `-j` or `-J` option, or call the command as `mkfs.ext3`. Use the `tune2fs` command on an existing `ext2` file system to add journaling. You learn how to convert an existing `ext2` file system into an `ext3` file system later in this chapter. Here, x represents a partition:

```
# tune2fs /dev/hdx -j
```

Some arguments you can use with this command include:

- `-j` — This option adds an `ext3` journal to the new file system using the default values. Note that you must be using a kernel that has `ext3` support to actually make use of the journal.
- `-J journal_options` — This option overrides the default `ext3` journal parameters so that you can choose the options you desire. The following journal options are comma separated and can take an argument using the `=` sign.
    - `size=journal_size` — This option creates a journal of `journal_size` megabytes. With a minimum size of 1,024 blocks, it cannot be more than 102,400 blocks. There must be enough free space in the file system to create a journal of that size.
    - `device=external_journal` — This option associates the file system with a journal not contained within the file system (one that must have already been created with the command `mke2fs -o journal_device journal_name`); in other words, the journal and the data files do not have to be on the same device.
