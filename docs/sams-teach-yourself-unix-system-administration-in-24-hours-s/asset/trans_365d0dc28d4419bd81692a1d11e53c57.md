
One nice touch here is that the single-user mode boot-up reminds you that the root filesystem is mounted read-only (which means that it's safe to run fsck without risk of corruption), where the fsck and mount commands are, and how to proceed.

2. Running fsck demonstrates the universality of this utility even across completely different Unix platforms and different filesystem layouts (this is an HFS+ system rather than an ext2 system):

```
localhost# /sbin/fsck
** /dev/rdisk0s5
** Checking HFS Plus volume
** Checking Extents Overflow file.
** Checking Catalog file.
** Checking multi-linked files
Orphaned indirect node temp105533
** Checking Catalog hierarchy.
** Checking volume bitmap.
** Checking volume information.
** Repairing volume.

**** FILE SYSTEM WAS MODIFIED ****

**** REBOOT NOW ****
```

The next step is to remount the filesystem read-write, and continue booting by exiting this interactive shell:

```
localhost# /sbin/mount -uw /
localhost# exit
```

Although the specifics of the output from single-user mode boot vary from platform to platform, the general concept is identical: to drop you, the system administrator, into a minimal command shell so you can run any necessary diagnostics. Exiting the shell continues the boot process and should leave the system running as normal.

One of the most common places you'll encounter the fsck program is when the system has a corruption problem and drops into single-user mode upon rebooting. Although you can explicitly switch into this mode, many Unix systems, upon encountering errors with the automatic fsck run at boot-time, will automatically switch to this mode and leave you on your own.

As you have seen, fsck is rather straightforward, so its occasional cryptic output isn't too intimidating, and you can easily work and fix any disk problems encountered. Right?

## Don't Panic!

Finally, if you do encounter any disk corruption, don't immediately panic and start breathing oddly. Instead, there are a couple of steps you can take to minimize the danger:

- 1. Kick off all the users and drop down into single-user mode. On most systems all this will happen automatically if you type `init 1` while logged in as root (see Hour 13). Beware: Users don't get any warning; they just get the boot, and quick!
- 2. Now that you've minimized the danger of further corruption, take a deep breath and pat yourself on the back because *you've been keeping really good backups, haven't you?*
- If you have a good backup regimen, the worst you should lose are the changes introduced that day, which isn't too bad. If you aren't backing up your system, now's a good time to start panicking.
- 3. Take a deep breath.
- 4. Make sure that the disk you need to check isn't mounted by using mount (see Hour 10, "Adding Disks to Your System").
- 5. Run `fsck -v` on the corrupt disk and see what the damage is.
- 6. Run `fsck` a second, and even a third time, until it reports no problems or corruption.
- 7. Reboot the machine with `shutdown -r now` and keep your fingers crossed.

If you have the unusual situation of the corruption not fixing itself, it might be time to try copying as much of the material as possible to a different device (you'll have varying levels of success, alas). The next step is to use `fsck -c` to have it check for—and identify—bad blocks. Then, run `fsck` again to see if that solves the problem.

In extreme cases you might need to completely reformat the disk with `fdisk`, but in more than 20 years of using Unix I've never encountered this particular situation. It's *very* rare to have this level of problem with a filesystem.

```
init 1
```

```
shutdown -r now
```

![](img/5ced0c78d748bd190e9027e5549a3622_209_0.png)

## Summary

Compared to other operating systems, Unix is remarkably stable and reliable. It's not at all uncommon to hear of systems that have been running for months, if not years, without a single reboot.

![](img/5ced0c78d748bd190e9027e5549a3622_210_0.png)

> The main server for The Internet Mall, running Red Hat Linux, never crashed in almost three years of busy 24/7 operation. The only times it was rebooted was because we were working on it or needed to relocate it from one facility to another. Unix is very reliable!

When things do go south, however, your best friend will prove to be fsck. The fsck command really has a remarkable capability to fix almost anything that can go wrong with a Unix filesystem, and many sysadmins have spent their entire careers using the -y flag and not even paying attention to the specific error messages.

## Q&A

**Q** Where did the ext3 filesystem come from?

**A** The layout of information on hard disks has a long and quite interesting history. I'll restrain myself, however, and simply note that the immediate parent of the ext3 filesystem is the ext2 filesystem, which itself came from some groundbreaking research at UC Berkeley by Kirk McKusick, Bill Joy, and Sam Leffler on something they eventually called the Berkeley Fast File System. UC Berkeley plays a very important role in the history of Unix, with BSD and many of the most popular commands in Unix spawned from the Computer Science Research Group.

**Q** Why don't popular PC disk maintenance utilities require you to unmount the disk?

**A** Actually, if you get into real trouble with your disks, you'll find that most of these utility programs require you to reboot off the included CD-ROM. The purpose of this is so that the disk-fix utility can unmount the disk before it begins to try and fix it, just like our friend fsck.

**Q** If you have fsck parallelizing (that is, checking multiple disks at the same time) and one of the disks turns out to have an error, how do you know what's going on?

**A** That's actually one of the few limitations of the parallel approach to checking disks. Fortunately, the authors of fsck thought this through and almost all parallel versions offer a "serialize" flag that forces the program to check disks one at a time rather than all at once. On Linux, for example, the -s flag does just that.

## Workshop

### Quiz

- 1. What’s the most common Linux filesystem? Mac OS filesystem? Commercial Unix filesystem?
- 2. Superstition or not, most Unix sysadmins do what after they run fsck and find errors?
- 3. On a filesystem with 512-byte blocks, what’s the minimum actual disk space used by a file that’s 1025 bytes in size?
- 4. The Unix equivalent of the PC “File Allocation Table” (that’s what “FAT” stands for on those FAT* filesystems) is called?
- 5. When the fsck program doesn’t think that a check is required of the filesystem, it refers to that disk as being in what state?
- 6. Though it’s called single-user mode, can you really use a computer in that state?

### Answers

- 1. The most common Linux filesystem is ext2 with ext3 continuing to grow in popularity; on the Mac it’s HFS+ (Hierarchical File System Plus), and on commercial Unix systems it’s the FFS (Berkeley Fast File System).
- 2. Run fsck again.
- 3. If the file is 1025 bytes in size and it gets stored in 512-byte blocks, the minimum size possible is three 512-byte blocks, or 1536 bytes.
- 4. The superblock.
- 5. Disks that don’t need checking are “clean.”
- 6. No. On almost all Unix systems, networking, a windowing environment, and other necessities of modern Unix interaction, aren’t started yet. It’s an unfortunate name because it’s really administrative mode.

In the next hour, we’ll format and mount a new disk on the system, exploring partition tables, fdisk, newfs and other helpful tools.

## Hour 10

![](img/5ced0c78d748bd190e9027e5549a3622_213_0.png)

### Adding Disks to Your System

The last hour explored the fsck command and how it can be used to diagnose and fix problems with hard disks. This hour will address the other half of the disk issue—how to add new disks, format them, and hook them up to your Unix system. It's a set of commands you won't need too often, I expect, but when you are ready, this shows the sequence needed.

With personal computer systems, the steps involved in adding and accessing a new disk tend to be hidden, but with Unix, a new disk needs to be formatted, partitioned, checked, then mounted somewhere in the filesystem.

Indeed, PC and Macintosh systems have a very primitive multiple disk configuration capability: On the PC, for example, a primary disk is C:, a CD-ROM drive is E:, and a floppy drive is A:. Add a new disk, and it's probably configured as D: or F:. On the Macintosh, all new disks appear on the desktop with mnemonic names—a small improvement, but they're still all at the topmost level of the filesystem.
