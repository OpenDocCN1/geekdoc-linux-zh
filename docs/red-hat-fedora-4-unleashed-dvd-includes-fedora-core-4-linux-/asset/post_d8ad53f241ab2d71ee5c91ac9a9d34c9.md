
## Performance Tuning

Squeezing extra performance out of your hardware might sound like a pointless task given how cheap commodity upgrades are today. To a certain degree that is true—for most of us, it is cheaper to buy a new computer than to spend hours fighting to get a 5% speed boost. But what if the speed boost were 20%? How about if it were 50%?

The amount of benefit you can get by optimizing your system varies depending on what kinds of tasks you are running, but there is something for everyone. Over the next few pages we will be looking at quick ways to optimize the Apache web server, both the KDE and Gnome desktop systems, both MySQL and PostgreSQL database servers, and more.

Before we start, you need to understand that *optimization* is not an absolute term: If we optimize a system, we have improved its performance, but it is still possible it could further be increased. We are not interested in getting 99.999% performance out of a system because optimization suffers from the law of diminishing returns—the basic changes make the biggest differences, but after that it takes increasing amounts of work to obtain decreasing speed improvements.

## Hard Disk

Many Linux users love to tinker under the hood to increase the performance of their computers, and Linux gives you some great tools to do just that. Whereas Moms tell us, “Don’t fix what’s not broken,” Dads often say, “Fix it until it breaks.” In this section, you learn about many of the commands used to tune, or “tweak,” your file system.

Before you undertake any “under the hood” work with Linux, however, keep a few points in mind. First, perform a

### IN THIS CHAPTER

- Hard Disk
- Kernel
- Apache
- MySQL
- Reference

benchmark on your system before you begin. Linux does not offer a well-developed benchmarking application, but availability changes rapidly. You can search online for the most up-to-date information for benchmarking applications for Linux. If you are a system administrator, you might choose to create your own benchmarking tests. Second, tweak only one thing at a time so you can tell what works, what does not work, and what breaks. Some of these tweaks might not work or might lock up your machine.

Always have a working boot floppy handy and remember that you are personally assuming all risks for attempting any of these tweaks.

### Using the BIOS and Kernel to Tune the Disk Drives

One method of tuning involves adjusting the settings in your BIOS. Because the BIOS is not Linux and every BIOS seems different, always read your motherboard manual for better possible settings and make certain that all the drives are detected correctly by the BIOS. Change only one setting at a time.

Linux does provide a limited means to interact with BIOS settings during the boot process (mostly overriding them). In this section, you will learn about those commands.

Other options are in the following list, and are more fully outlined in the BOOTPROMPT HOWTO and the kernel documentation. These commands can be used to force the IDE controllers and drives to be optimally configured. Of course, YMMV (Your Mileage May Vary) because these do not work for everyone.

- `idex=dma`—This will force DMA support to be turned on for the primary IDE bus, where x=0, or the secondary bus, where x=1.
- `idex=autotune`—This command will attempt to tune the interface for optimal performance.
- `idex=ata66`—If you have ATA66 drives and controllers, this command will enable support for it.
- `hdx=ide-scsi`—This command will enable SCSI emulation of an IDE drive. This is required for some CD-RW drives to work properly in write mode and it might provide some performance improvements for regular CD-R drives as well.
- `idebus=xx`—This can be any number from 20 to 66; autodetection is attempted, but this can set it manually if dmesg says that it isn't autodetected correctly or if you have it set in the BIOS to a different value (overclocked). Most PCI controllers will be happy with 33.
- `pci=biosirq`—Some motherboards might cause Linux to generate an error message saying that you should use this. Look in dmesg for it; if you do not see it, you don't need to use it.

These options can be entered into `/etc/lilo.conf` or `/boot/grub/grub.conf` in the same way as other options are appended.

### The hdparm Command

The hdparm utility can be used by root to set and tune the settings for IDE hard drives. You would do this to tune the drives for optimal performance.

Once a kernel patch and associated support programs, the hdparm program is now included with Fedora Core. You should only experiment with the drives mounted read-only because some settings can damage some file systems when used improperly. The hdparm command also works with CD-ROM drives and some SCSI drives.

The general format of the command is this:

```
# hdparm command device
```

This command runs a hard disk test:

```
hdparm -tT /dev/hda
```

You will need to replace /dev/hda with the location of your hard disk. hdparm will then run two tests—cached reads, and buffered disk reads. A good IDE hard disk should be getting 400–500MB/sec for the first test, and 20–30MB/sec for the second. Note down your scores, then try this command:

```
hdparm -m16 -d1 -u1 -c1 /dev/hda
```

That enables various performance-enhancing settings. Now try executing the original command again—if you see an increase, then you should run this command:

```
hdparm -m16 -d1 -u1 -c1 -k1 /dev/hda
```

The extra parameter tells hdparm to write the settings to disk so they will be used each time you boot up—ensuring optimal disk performance in the future.

The man entry for hdparm is extensive and contains useful detailed information, but since the kernel configuration selected by Fedora Core already attempts to optimize the drives, it might be that little can be gained through tweaking. Because not all hardware combinations can be anticipated by Fedora Core or by Linux and performance gains are always useful, you're encouraged to try.

> **TIP**
>
> You can use the hdparm command to produce a disk transfer speed result with
>
> ```
> # hdparm -tT device
> ```

> Be aware, however, that although the resulting numbers appear quantitative, they are subject to several technical qualifications beyond the scope of what is discussed and explained in this chapter. Simply put, do not accept values generated by hdparm as absolute numbers, but only as a relative measure of performance.

System-wide tweaks to hdparm are formally handled through the /etc/sysconfig/harddisks files, but this file's use is poorly documented and, therefore, of little use.

> **TIP**
>
> You may find that your system turns off DMA for any CD-RW drives detected via a shell script command in `rc.sysinit`. This might not be appropriate for your hardware, so you can turn it back on simply by adding the line `options ide-cd dma=1` to `/etc/modules.conf`.

## File System Tuning

Never content to leave things alone, Linux provides several tools to adjust and customize the file system settings. The belief is that hardware manufacturers and distribution creators tend to select conservative settings that will work well all the time, leaving some of the potential of your system leashed—that’s why you have chosen Fedora Core Linux Unleashed to help you.

The Linux file system designers have done an excellent job of selecting default values used for file system creation and the 2.6 version of the Linux kernel now contains new code for the IDE subsystem that significantly improves I/O (input/output) transfer speeds over older versions, obviating much of the need for special tweaking of the file system and drive parameters if you use IDE disks. Although these values work well for most users, some server applications of Linux benefit from file system tuning. As always, observe and benchmark your changes.

> **Synchronizing the File System with sync**
>
> Because Linux uses buffers when writing to devices, the write will not occur until the buffer is full, until the kernel tells it to, or if you tell it to by using the `sync` command. Traditionally, the command is given twice, as in the following:
>
> ```
> # sync ; sync
> ```
>
> It is really overkill to do it twice. Still, it can be helpful prior to the unmounting of certain types of media with slow write speeds (such as some USB hard drives or PCCMIA storage media), but only because it delays the user from attempting to remove the media too soon, not because two syncs are better than one.

## The mke2fs Command

`mke2fs -O sparse_super` will create a file system with sparse superblocks, reducing the space allocated to root for file system repair. This is not a performance enhancement per se, but it will free up additional space on a drive. This command only works on pre-2.2 kernels and is included here because a number of existing references don’t make that distinction. With kernel version 2.2, the sparse superblock option has been moved to tune2fs, and this feature is turned “on” by default, so you will always create any new file systems with sparse superblocks.

`mke2fs -b blocksize` will set the block size. The block size chosen can also have an effect on the performance of the file system. A larger block size works better with large files and vice versa. There doesn’t seem to be any hard and fast rule about this, and most advice is
