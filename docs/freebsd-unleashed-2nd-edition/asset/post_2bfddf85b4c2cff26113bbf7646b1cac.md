
The sixth, or rightmost, column in /etc/fstab is the Pass# field. The pass number is a flag for fsck; numbers above 0 indicate the order in which the filesystems should be checked. The root filesystem has a pass number of 1, meaning that it is checked first; mounts with a pass number of 2 are checked next, in as parallel a manner as the hardware permits. A pass number of 0 means that the filesystem should not be checked; this is what you want for CD-ROMS, floppies, swap partitions, and other resources that can’t become corrupted or it doesn’t matter if they do become corrupted.

A fuller discussion of backup and restoration procedures can be found in Chapter 19, “FreeBSD Survival Guide,” in which dump will be covered in more detail, along with other backup/mirroring methods such as CVSUp.

## Checking and Repairing Filesystems with fsck

The fsck (Filesystem Consistency Check) program is the equivalent of Microsoft ScanDisk and other disk utilities, at least as far as its role in the boot process and its interactive nature go. The fsck program runs at boot time just before mounting the filesystems out of /etc/fstab, to make sure that all the filesystems are “clean” and eligible for mounting. This is the “preen” mode that is called with the -p option. But fsck also exists to repair any inconsistencies that it finds and to clean filesystems that have not been marked “clean” by a proper shutdown method.

The most likely place you’ll encounter fsck is at boot time, no matter what role it plays in your life. In the happiest circumstances, it runs invisibly just after all the devices have been identified, and all you see are a few lines like this:

```
/dev/ad0s1e:
103469 files, 858450 used, 9066025 free
(25777 frags, 1130031 blocks, 0.3% fragmentation)
```

> **NOTE**
> 
> Don’t worry about the “fragmentation” figure that fsck prints out. It looks pretty dire, but be aware that even fragmentation of 2 to 3 percent (which is the highest you’ll likely see) is miniscule compared to the kind of fragmentation that occurs under Windows. It is not unusual to see a DOS/FAT disk with 50 percent or more fragmentation; that is why defragmenting utilities sell so well in the desktop market. Unix filesystems, however, are designed with mechanisms to keep related sectors together on the fly, so fragmentation is kept to a minimum. You won’t ever need to defragment a Unix hard drive. See “Blocks, Files, and Inodes,” later in this chapter, for a closer look at the mechanics of data storage and fragmentation.

You may run into trouble, however, if the system has not been shut down cleanly—if power has failed or someone has hit the power switch without running shutdown first. Unix filesystems keep track of their structural information by writing that metadata to the disk in a synchronous manner, which may take multiple write cycles. If the system goes down while it's in the middle of the write sequence, the metadata becomes corrupted, and the filesystem cannot be used until it is made consistent again. This is what **fsck** is for.

If a filesystem is brought up in this "unclean" state, **fsck** drops into its investigative mode. It then walks through the filesystem block by block, examining the metadata and making sure it is consistent. This can take a very long time, depending on the size of the filesystem and the speed of the disk. When **fsck** finds an inconsistency that it cannot repair automatically while guaranteeing data integrity (see `man fsck` for details), **fsck** prompts you about whether you want to fix it. In most cases, you do. However, if you are being prompted, it's most likely that the inconsistency is so severe that you will have lost some data—usually the file or files being written at the time of the crash, which tends to mean that data loss is fairly small.

After **fsck** finishes running, you may be dropped to a **#** prompt. Type **boot** to continue booting or **reboot** to go through the entire boot process again. Going through a reboot might be a good idea, just to make sure it will come up cleanly without intervention. You don't want to lock the server in a cabinet and drive away, only to have it not come up the next time it crashes.

Boot time is not the only place for **fsck**, though. You also can run it from the command line at any time on mounted filesystems, although it's a bad idea to do so when the system is fully up and running! It's important that the filesystem in question not be changing while you're trying to give it a consistency check. If you have to run **fsck** on one of your system's main devices, take the precaution of dropping to single-user mode:

```
# shutdown +5
```

This command closes down multiuser mode five minutes after you issue the command. Naturally, everything from this point on has to be done at the physical console. You can't remotely administer the system in single-user mode!

> **TIP**
> 
> You can also shut down the system immediately, rather than after a pause, with the **shutdown now** command.

With the system in this quiescent state, you can now use **fsck** to your heart's content. This may be necessary if during runtime you find a message in your **dmesg** output (part of the daily monitoring scripts that get sent to *root*) that says it found a bad inode or file descriptor, and you want to go directly to the root of the problem without rebooting. After you run **fsck** on one or all of your devices (use **fsck** syntax such as `fsck -p /dev/ad1s1g`), you can then simply exit from the single-user shell (type **exit**) to bring up the rest of the multiuser system.

One case in which it is safe to use fsck while still in multiuser mode is when you're trying to mount a second disk with a noncritical or new filesystem that you're attempting to add. The fsck that runs at boot time will only check the filesystems that are listed in /etc/fstab. Rather than adding the new device to the fstab file and rebooting, you can simply try to mount the device. If the mount fails, telling you that you need to run fsck, do so with the syntax shown previously. Then try mounting the disk again. This mount can be done safely in multiuser mode because nobody will be writing to a device that hasn't been mounted!

> **NOTE**
> 
> FreeBSD's fsck is similar in functionality to that of the fsck used on similar operating systems; however, it does lack one or two nice interface features, such as the progress bar on the Linux fsck. Be assured, though, that the core features behave almost exactly the same way.

## Journaling Filesystems and Soft Updates

Many different solutions to the synchronous-write issue have been developed. You hear about journaling (or logging) filesystems, for example, which keeps a log of all metadata writes before they are executed. This log dramatically speeds up fsck because it no longer needs to comb the entire filesystem—it knows where the inconsistencies are and how to fix them.

FreeBSD does not include support for journaling filesystems; what it does have, though, is Soft Updates. Whereas journaling filesystems work by maintaining a log file of write actions, Soft Updates (which is built into the GENERIC, or default, kernel as of FreeBSD 4.5) provides a potentially superior technique. Soft Updates uses precalculated, ordered writes to eliminate the need for an external log; at the same time, Soft Updates protects the integrity of the metadata to provide filesystem consistency as good as or better than that offered by journaling. It has performance advantages over journaling as well; a filesystem can be brought up immediately at boot time, and the consistency checking is done afterward through the use of automated snapshots in a background task.

Soft Updates can be enabled on any or all of your filesystems. A toggle option in the Disk Label Editor (the utility you use to divide your disk into subpartitions and assign them to different mount points, as discussed in the section “Creating the Disk Labels,” in Chapter 18) lets you set Soft Updates on whichever partitions, or filesystems, you wish. Soft Updates is particularly effective when used on filesystems that contain frequently changing data, such as /var and /usr.

In FreeBSD 5.0, a daemon called diskcheckd supports Soft Updates. Enabled by default, diskcheckd runs in the background and performs periodic filesystem integrity scans, thus dramatically reducing the reliance on fsck at boot time and the risks associated with abrupt shutdowns. The configuration file is /etc/diskcheckd.conf; see man diskcheckd
