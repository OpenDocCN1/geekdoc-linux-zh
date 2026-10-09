
options (-d -X66) enables UltraDMA mode 2 for drives that support UltraDMA burst timing feature. These options can dramatically increase your drive performance. I have seen 20 MB/sec transfer rates with these options on various new EIDE/ATA drives.

There is another option, -u, that can be very useful for increasing overall system performance. This option enables the drive driver to unmask other interrupts during processing of a drive interrupt, which means that the operating system can attend to other interrupts, such as the network I/O or serial I/O, while waiting for a drive-based data transfer to finish.

There are many other options that you can set and experiment with by using hdparm; however, be very cautious about most of the options because there is a good chance that you may corrupt data. Always backup data before playing with the hdparm tool. Also, after you have found that a set of options work well, you should put the hdparm command with options in the /etc/rc.d/rc.local script so that they are set every time you boot the system. For example, I have added the following line in the /etc/rc.d/rc.local file in one of my newer Linux systems:

```
hdparm -m16 -c3 -u -d -X66 /dev/hda
```

Now that you have tuned your hard drive for better performance, let's look at how you can tune the file system that acts as the interface to your drives. Because Red Hat Linux uses the ext2 file system, I discuss tuning issues for it in the “Tuning Linux's ext2 File System” section below.

## Ethernet card

The last piece of hardware that resides in your computer system and can have an impact on your server performance is the network adapter card. I assume that your Web server is going to be connected to an Ethernet network somewhere. The adapter card you use should be of reasonably high quality and fast. For example, if the Ethernet network to which you are hooking up your Web server handles either 10Mbps or 100Mbps nodes, get a 100Mbps adapter card from a brand-name vendor.

The rest of the hardware that may become a factor in your server performance is discussed in the network section of this chapter.

## Tuning Linux's ext2 File System

You can skip this section if you do not use Linux for Apache server. It is not the greatest file system in the world, but it works reasonably well. For years the ext2 file system has been the de facto file system for Linux, and so that's the file system I cover in this book.

### Changing the block size of the ext2 filesystem

One of the ways you can improve the ext2 file system’s performance is by changing the default block size from 1024 to a multiple of 1024 (usually less than 4096) for servers with mostly large files. To find out what kind of files you have on a particular ext2 partition do the following:

- 1. As root, change to the top directory of the ext2 partition.
- 2. Run the following commands, which really comprise a small script that uses the `find` and `awk` utilities. This command-line script will display all the files and their sizes and finally provide you with a total and average size of the entire partition.

```
find . -type f -exec ls -l {} \; | \
awk 'BEGIN {tsize=0;fcnt=1;} \
{ printf("%03d File: %6d size: %d bytes\n",fcnt++, $9,
$5); \
tsize += $5;} \
END { printf("Total size = %d\nAverage file size = %.02f\n",
tsize, tsize/fcnt);}'
```

- 3. After you know the average size of the file system, you can determine whether you should change the block size. If you discover that your average file size is 8192, which is $2 \times 4096$, you can change the block size to 4096.
- 4. Unfortunately, you cannot alter the block size of an existing ext2 file system without rebuilding it. So, you have to back up all your files from the file system and then rebuild the file system by using the `/sbin/mke2fs /dev/partition -b 4096` command. For example, if you have backed up the `/dev/hda7` partition and want to change the block size to 4096, use the `/sbin/mke2fs /dev/hda7 -b 4096` command.

Changing the block size to a higher number than the default (1024) may yield significant performance in raw read speed because of a reduced number of seeks and also because the `fsck` session during boot may be faster, because there may be less file fragmentation, and for other reasons. However, increasing the block size blindly (that is, without knowing the average file size) can result in wasted space. If the average file size is 2010 bytes on a system with 4096 byte blocks, each file will waste on an average 2086 bytes (4096 − 2010)! So know your file size before messing with the block size.

### Tuning the ext2 file system with e2fsprogs

The default ext2 file system can be tuned using the e2fsprogs suite. In this section, I will discuss how you can install this suite of programs and use them in tuning, performing routine checks, and repairing your disks.

### Installing *e2fsprogs*

To tune the ext2 file system, you need to install the *e2fsprogs* utility package as follows:

- 1. Download the `e2fsprogs-version.src.rpm` (replace `version` with the latest version number) source distribution from `www.rpmfind.net`. I downloaded the `e2fsprogs-1.19-0.src.rpm` package. You can also get the source from the *e2fsprogs* project site at `http://e2fsprogs.sourceforge.net`.
- 2. Run the `rpm -ivh e2fsprogs-version.src.rpm` command to extract the source into `~/usr/src/redhat/SOURCES/` directory. The source RPM drops a `e2fsprogs-version.tar.gz` file that needs to be extracted using the `tar xvzf e2fsprogs-version.tar.gz` command. This creates a subdirectory called `e2fsprogs-version`.
- 3. Change to the new subdirectory.
- 4. Run `mkdir build` to create a new subdirectory and then change to that directory.
- 5. Run `../configure` script to configure the source tree.
- 6. Run the `make` utility to create the binaries.
- 7. Run the `make check` command to ensure that everything is built correctly.
- 8. Run the `make install` command to install the binaries.

After you have installed the *e2fsprogs* utilities you can start using them as discussed in the following sections.

### Tuning your file system with `tune2fs`

You can use the `tune2fs` utility to tune various aspects of an ext2 file system.

> You should never apply the ext2 utilities on a mounted ext2 and you should always back up your data whenever you are modifying anything belonging to a file system.

The following section discusses how to use the `tune2fs` utility (part of the *e2fsprogs* package) to tune an unmounted ext2 file system called `/dev/hda7`. If you use one or more of the settings discussed below, don’t forget to change the partition name (`/dev/hda7`) to the appropriate name. First, let’s look at what `tune2fs` shows as the current settings for the unmounted `/dev/hda7` by running the following command:

```
/sbin/tune2fs -l /dev/hda7
```

The output should be similar to this:

```
tune2fs 1.19, 13-Jul-2000 for EXT2 FS 0.5b, 95/08/09
Filesystem volume name:   <none>
Last mounted on:          <not available>
Filesystem UUID: 5d06c65b-dd11-4df4-9230-a10f2da783f8
Filesystem magic number: 0xEF53
Filesystem revision #: 1 (dynamic)
Filesystem features: filetype sparse_super
Filesystem state: clean
Errors behavior: Continue
Filesystem OS type: Linux
Inode count: 1684480
Block count: 13470471
Reserved block count: 673523
Free blocks: 13225778
Free inodes: 1674469
First block: 1
Block size: 1024
Fragment size: 1024
Blocks per group: 8192
Fragments per group: 8192
Inodes per group: 1024
Inode blocks per group: 128
Last mount time: Thu Feb 15 17:51:19 2001
Last write time: Thu Feb 15 17:51:51 2001
Mount count: 1
Maximum mount count: 20
Last checked: Thu Feb 15 17:50:23 2001
Check interval: 155520000 (6 months)
Next check after: Tue Aug 14 18:50:23 2001
Reserved blocks uid: 0 (user root)
Reserved blocks gid: 0 (group root)
First inode: 11
Inode size: 128
```

The settings that I discuss in the list below are bolded above:

- **Errors behavior:** This setting dictates how the kernel behaves when **errors** are detected in the file system. There are three possible values for this setting—*continue*, *remount-ro* (readonly). In other words, the default setting is to continue running even if there is an error.
- **Mount count:** The number of times you have mounted this file system.
- **Maximum mount count:** This means that after the maximum number of read/write mode mounts the file system will be subject to a *fsck* checking session during the next boot cycle.
- **Last checked:** This setting shows the last date on which a *fsck check* was performed. The check interval for two consecutive *fsck sessions*.
- **Check interval:** This is only used if the maximum read/write mount count is not reached during the interval. In other words, if you don't unmount the file system for 6 months, then even though the mount count will be only 2, the *fsck* check will be forced because the file system exceeded the check interval.
- **Next check after:** This is the **next fsck** check date.
