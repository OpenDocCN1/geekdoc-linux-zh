
might hit the upper limit. The `df -i` command will give you information on your inode usage:

```
$ df -i
Filesystem Inodes IUsed IFree IUse% Mounted on
/dev/sda  520192  17539  502653  4% /
```

In this example, the root partition has 520,192 total inodes but only 17,539 are used. That means you can create another 502,653 files on that file system. In the case where 100% of your inodes are used, only a few options are at your disposal. You can try to identify a large number of files that you can delete or move to another file system; you can possibly archive a group of files into a tar archive; or you can back up the files on your current file system, reformat it with more inodes, and copy the files back.

### The File System Is Read-Only

Every now and then you may encounter a file system that isn't full, but it won't let you write to it all the same. When you do try to copy a file or save a file, you get an error that the file system is read-only. The first step is to see if you can, in fact, remount the file system read-write; so for instance, if the `/home` partition were read-only, you would type

```
$ sudo mount -o remount,rw /home
```

Chances are, though, if you get this error, it's because your file system has encountered some sort of error and has decided to remount read-only to protect itself from further damage. This sort of problem happens more frequently on virtual machines in part, I imagine, to the extra level of abstraction between its virtual disk and the physical hardware. When there's some hiccup between the two, the file system detects a serious error and protects itself. To know for sure, examine the output of the `dmesg` command, specifically for lines that begin with `EXT3-fs error`. You should see lines in the output that reference the errors ext3 found and a log entry that states Remounting filesystem read-only.

So what do you do if this happens to you? If the file system is not the root partition and you can completely unmount it, you can try to unmount it completely and then remount it. If it’s the root partition, or remounting doesn’t work, unfortunately you will have to reboot the system so it can check and remount the file system cleanly. If after a reboot the file system still won’t mount cleanly, then move on to the next section.

### Repair Corrupted File Systems

There are a number of scenarios in which a file system might get corrupted through either a hard reboot or some other error. Normally Linux will automatically run a file system check command (called `fsck`) at boot to attempt to repair the file system. Often the default `fsck` is enough to repair the file system, but every now and then a file system gets corrupt enough that it needs manual intervention. What you will often see is the boot process drop out after a `fsck` fails, hopefully to a rescue shell you can use to run `fsck` manually. Otherwise, track down a rescue disk you can boot from (many distribution install disks double as rescue disks nowadays), open up a terminal window, and make sure you have root permissions (on rescue disks that use `sudo`, you may have to type `sudo -s` to get root).

One warning before you start `fscking` a file system: Be sure the file system is unmounted first. Otherwise, `fsck` could potentially damage your file system further. You can run the `mount` command in the shell to see all mounted file systems and type `umount <device_name>` to unmount any that are mounted (except the root file system). Since this file system is preventing you from completing the boot process, it probably isn’t mounted, so in this example let’s assume that your /home directory is mounted on a separate partition at /dev/sda5. To scan and repair any file system errors on this file system, type

```
# fsck -y -C /dev/sda5
```

The `-y` option will automatically answer Yes to repair file system errors. Otherwise, if you do have any errors, you will find yourself hitting Y over and over again. The `-C` option gives you a nice progress bar so you can see how far along fsck is. A complete fsck can take some time on a large file system, so the progress bar can be handy.

Sometimes file systems are so corrupted that the primary superblock cannot be found. Luckily, file systems create backup superblocks in case this happens, so you can tell fsck to use this superblock instead. You aren't likely to automatically know the location of your backup superblock. For ext-based file systems you can use the mke2fs tool with the -n option to list all of the superblocks on a file system:

```
# mke2fs -n /dev/sda5
```

> **WARNING** Be sure to use the -n option here! Otherwise, mke2fs will simply format your file system and erase all of your old data.

Once you see the list of superblocks in the output, choose one and pass it as an argument to the -b option for fsck:

```
# fsck -b 8193 -y -C /dev/sda5
```

When you specify an alternate superblock, fsck will automatically update your primary superblock after it completes the file system check.

### Repair Software RAID

The hard drive is one of the pieces of hardware most likely to break on your server, and if you run a system that uses Linux software RAID, it's good to know how to repair the RAID. The first step is figuring out how to detect when a RAID has failed. On a modern software RAID install, the system should have mdadm configured to email the root user whenever there is a RAID problem (if you want to change this, edit the MAILADDR option in /etc/mdadm/mdadm.conf and run /etc/init.d/mdadm reload as root to load the changes). Otherwise you can view the /proc/mdstat file:

```
$ cat /proc/mdstat
Personalities : [linear] [multipath] [raid0] [raid1] [raid6] [raid5] [raid4] [raid10]
md0 : active raid5 sdb1[0] sdd1[3](F) sdc1[1]
16771584 blocks level 5, 64k chunk, algorithm 2 [3/2] [UU..]
unused devices: <none>
```

Here you can see that sdd1 is marked with an (F) stating it has failed, and on the next line of output, the array shows two out of three disks ([3/2] [UU..]).
The next step is to remove the disk from /dev/md0 so that you can swap it out with a new drive. To do this, run mdadm with the --remove option:

```
$ sudo mdadm /dev/md0 --remove /dev/sdd1
```

The drive must be set as a failed drive for you to remove it, so if for some reason mdadm hasn’t picked up the drive as faulty but you want to swap it out, you might need to set it as faulty before you remove it:

```
$ sudo mdadm /dev/md0 --fail /dev/sdd1
```

The mdadm command supports chaining commands, so you could fail and remove a drive in the same line:

```
$ sudo mdadm /dev/md0 --fail /dev/sdd1 --remove /dev/sdd1
```

Once you remove a drive from an array, it will be missing from /proc/mdstat:

```
$ cat /proc/mdstat
Personalities : [linear] [multipath] [raid0] [raid1] [raid6] [raid5] [raid4] [raid10]
md0 : active raid5 sdb1[0] sdd1[1]
16771584 blocks level 5, 64k chunk, algorithm 2 [3/2] [UU..]
unused devices: <none>
```

Now you can swap out the drive with a fresh one and partition it (either a hot-swap if your system supports that, or otherwise by powering the system down and swapping the hard drives). Be sure that when you replace drives you create new partitions to be equal or greater in size than the rest of the partitions in the RAID array. Once the new partition is ready, use the --add command to add it to the array:

```
$ sudo mdadm /dev/md0 --add /dev/sdd1
```

Now mdadm will start the process of resyncing data. This can take some time, depending on the speed and size of your disks. You can monitor the progress from /proc/mdstat:

```
$ cat /proc/mdstat
Personalities : [linear] [multipath] [raid0] [raid1] [raid6] [raid5] [raid4] [raid10]
md0 : active raid5 sdd1[3] sdb1[0] sdc1[1]
16771584 blocks level 5, 64k chunk, algorithm 2 [3/2] [UL_]
[>....................] recovery = 2.8% (170112/6385792)
finish=1.6min speed=85056K/sec
unused devices: <none>
```

> **NOTE**
> If you get tired of running cat /proc/mdstat over and over, you can use the watch command to update it every few seconds. For instance, to run that command every 5 seconds you could type
> `$ watch -n 5 "cat /proc/mdstat"`
> Just hit Ctrl-C to exit out of the watch command when you are done.
