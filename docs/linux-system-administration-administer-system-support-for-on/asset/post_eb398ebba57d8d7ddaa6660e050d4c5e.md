
![](img/8ad518fddafc7f5e73715a2604b61d50_354_0.png)

> Take special care to keep the syntax of this command accurate. Reversing the syntax just given, for example, would dump the contents of the floppy drive to the /zImage file. I probably don't have to tell you not to do it. But don't do it.

## Backing Up with cpio

The cpio command copies files in and out of an archive and from directory to directory. It works really nicely with the find command, so you can assemble some nice commands that will backup for you.

The find command has an option of -cpio that will let you archive the files you found. For example, you found all the .rhosts files. You want to archive these files onto your tape drive so you have record of which users are being sloppy:

```
find / -name .rhosts -cpio /dev/rmt0;
```

Listing 10-3 illustrates using the cpio command for backup.

### Listing 10-3: Using cpio for backup

```
# cpio -help

Usage: cpio [-o|--create] [-OacvABLV] [-C bytes] [-H format] [-M message]
    [-0 [user@]host::archive] [-F [user@]host::archive]
    [--file=[user@]host::archive] [--format=format] [--message=message]
    [-null] [--reset-access-time] [-verbose] [-dot] [--append]
    [-block-size=blocks] [--dereference] [-io-size=bytes] [--quiet]
    [--force-local] [--help] [-version] < name-list > archive
    cpio [-i|--extract] [-bcdfmnrtuvBSV] [-C bytes] [-E file] [-H format]
    [-M message] [-R [user]::[group]] [-I [user@]host::archive]
    [-F [user@]host::archive] [--file=[user@]host::archive]
    [-make-directories] [--nomatching] [--preserve-modification-time]
    [--numeric-uid-gid] [--rename] [-list] [-swap-bytes] [-swap] [-dot]
    [-unconditional] [-verbose] [-block-size=blocks] [-swap-halfwords]
    [-io-size=bytes] [-pattern-file=file] [-format=format]
    [-owner=[user]::[group]] [-no-preserve-owner] [--message=message]
    [-force-local] [-no-absolute-filenames] [-sparse] [-only-verify-crc]
    [-quiet] [-help] [-version] [pattern...] < archive
    cpio [-p|--pass-through] [-OadmuvLV] [-R [user]::[group]]
    [-null] [--reset-access-time] [--make-directories] [-link] [--quiet]
    [--preserve-modification-time] [-unconditional] [-verbose] [-dot]
    [--dereference] [-owner=[user]::[group]] [-no-preserve-owner]
    [-sparse] [-help] [-version] destination-directory < name-list
```

If you wanted to make a backup of your entire disk to another hard drive, you could do something like this:

```
# find / -cpio /dev/hbd
```

You can also use the cpio command alone. With the -o option, you can read output into the cpio command.

```
# ls -R /home | cpio -o > /dev/rmt0
```

This would take a recursive listing of the /home directory and redirect the output to the first tape drive.

## Restoring Files

When you’ve made backups, you’ll soon be glad you did. If one of your users accidentally deletes his home directory, you don’t have to panic. If you’re using tar, you can simply correct the problem.

```
# tar -xvfZ /zipdrive/backup-home-dir.tar.gz /opt/restore
```

![](img/8ad518fddafc7f5e73715a2604b61d50_355_0.png)

Even if you know the contents of the backup data, it doesn’t hurt to have a separate restore section so you don’t overwrite anything you didn’t mean to get rid of.

If you’re using the dd command, it’s something similar. Again, make sure you don’t reverse the if and the of devices.

```
# dd if=/dev/rmt0 of=/opt/restore
```

For cpio, the command takes a different syntax than the example above for creating the backup. This will restore a specific file from the tape drive.

```
# cd /opt/restore
# cpio -id filename < /dev/rmt0
```

## Power Management

How do you deal with power outages? Start with the basics: Get an uninterruptible power supply (UPS) for your desktop computer and keep your laptop’s batteries fully charged.

### UPS Status

For UPS battery status, the `upsd` daemon is designed to monitor the UPS. There are some tools currently available at <http://sunsite.unc.edu/pub/Linux/system/ups>. There are a couple other monitoring utilities like Genpower that have automated shutdown and low battery detection. Table 10-3 lists many currently available tools.

**TABLE 10-3 UPS POWER MANAGEMENT TOOLS**

| Utility | File | Description |
| :--- | :--- | :--- |
| Apcd | apcd-0.5.tar.gz | Monitor APC SmartUPS in "smart" mode |
| Apcupsd | apcupsd-3.3.0.bin.linux.tar.gz | UPS power management in "dumb" mode for APCC Products |
| DumpUPSd | dumbupsd-0.1.tar.gz | Provides scripts for startup and shutdown for dump UPS |
| Genpower | genpower-1.0.1.tgz | Highly configurable UPS monitor |
| Powerd | powerd-2.0.tar.gz | Network-aware daemon that powers up and powers down hosts connected to dumb UPSs |
| SmartUPS | smartups-1.1.tgz | X11 Load monitor for SmartUPS |
| Upsd | ups.tar.gz | Program to interact with Powerbox UPS |
| Upsd Power Monitor Daemon | upsd-1.0.tgz | Monitor APC BackUPS or SmartUPS in "dumb" mode |
| Usyd | usyd-2.0.0.tgz | Uninterrupted power supply monitor |

### Laptop Battery Status

Power-management support can be compiled directly into the Linux kernel. This means, for example, that you can shut down a laptop without having to turn it off manually. (In addition to kernel support, you can get utilities from <http://sunsite.unc.edu/pub/Linux/system/power>.) Table 10-4 lists laptop power management tools.

**TABLE 10-4 LAPTOP POWER MANAGEMENT TOOLS**

| Utility | File | Description |
| :--- | :--- | :--- |
| Apm Daemon | apmd-2.4.tar.gz | Monitors battery status via Advanced Power Management |
| Apm X | apmx-0.00.tgz | Monitors battery power via percentage, charging, and battery off-line status |
| Tkbattery | tkbattery-1.0.tgz | X-based low-battery warning monitor |
| Xbatcheck | xbatcheck-1.2.tar.gz | X-based battery monitor with critical power alarm |
| X Battery Status Viewer | xbatstat-0.5.2.tar.gz | Monitoring Battery Status via /proc/apm that requires XFORMS-0.81 |
| Xbattery | xbattery-1.0.tar.gz | Monitors battery and AC-power status in an X window |

You have a variety of programs you can use for power management on laptops. These include *apmd*, which is a daemon for monitoring battery power. For monitoring it under X, you can use *apmx*. A highly configurable battery monitor is *tkbattery*, which uses APM like the previous two programs listed above. Additionally, there are three other tools that let you monitor your battery status and even your AC power in X. They are *xbatcheck*, *xbatstat*, and *xbattery*.

## Rescue Disks

If you're playing around with your system, or your system happens to just crash for no apparent reason (this happens to all of us), you should have a rescue disk of some sort.

You can always use the command *make zdisk* from your kernel for a boot disk, but a rescue disk is always good to have handy. There are quite a few utilities available for download at http://sunsite.unc.edu/pub/Linux/system/recovery/, or you can use the *rawrite* command to the *rescue.gz* image onto a floppy disk as well. Table 10-5 gives you an overview of some utilities that increase your options for creating rescue disks.

In the *sunsite.unc.edu/pub/Linux/system/recovery/images/* directory, you can find *cramdisk* — which have both boot disk and RAM disk on one floppy — that provide rescue support for parallel-port Zip drives, PPP, Lynx, and other networking utilities. They can work with hosts that have at least 4MB of memory.

To modify an old saying, it may be good to be system administrator, but it's better to be a well-prepared one with lots of options.

**TABLE 10-5 UTILITIES FOR CREATING RESCUE DISKS**

| Utility | File | Description |
| :--- | :--- | :--- |
| The Linux Bootkit | Bootkit-1.01.tar.gz | Dialog-driven package for creating and maintaining emergency boot, root, and utility diskettes |
| CatRescue | CatRescue101E.tgz | Emergency boot-floppy generator |
| Search and Rescue Set | SAR-2.25.tar.gz | Used with your kernel to create the rescue flopppy |
| Disk recovery tools for ext2fs | disc-recovery-utils-1.0.tgz | Disk and inode recovery tools for the Second Extended File System |
| Fspace | f space.tgz | A statically linked utility that tells you how much free space you have |
| Genromfs | Genromfs-0.1.tar.gz | Create ROM-only file systems – useful for building both rescue and boot disks |
| Pico Rescue Disk | Pico.boot-0.95.tar.gz | Rescue disk with the pico editor and other tools |
| Rescue disk | Rescue02.zip | Recovery disk that can restore tape backups (made with the 1.3.84 kernel) |
| Rescue boot/root disk | Resque_disk-2.0.22.tar.gz | Contains some basic utilities and file system types |
| Small Shell | sash.tar.z | A small, statically linked shell for recovery scripts |
| Sbin utilities | sbin.tar.z | Statically linked /sbin utilities so you don’t need the dynamic libraries |
| The ln utility | sln.tar.z | A statically linked ln utility, so you don’t need the dynamic libraries |
| Tom’s Root/Boot Rescue disk | Tomsrtbt-1.4.68.tar.gz | Loads as much Linux as possible on a RAM disk |
| Yard | yard-1.15.tar.gz | Perl tool scripts for creating custom rescue disks |
| Yard-prefabs | yard-prefabs-2.tgz | Prefabricated disk contents for yard (currently contains only Slackware) |
