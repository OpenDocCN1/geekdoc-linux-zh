Once logged on (you are root by default), start fdisk on the first drive:

```
# fdisk /dev/had
```

Use the p command to display the partition information and compare it to the hard copy you have. If the entries are identical, you have a problem somewhere else; it is not the partition table.

If there is a problem, use the d command to delete all the listed partitions.

Now use the n command to create new partitions that will match the partition table from your hard copy. Make certain that the partition types (ext2, FAT, swap and so on) are the same. If you have a FAT partition at /dev/hda1, make certain that you set the bootable flag for it; otherwise, Windows or DOS will not boot.

If you find that you have made an error somewhere along the way, just use the q command to quit fdisk without saving any changes and start over. Without specifically telling fdisk to write to the partition table, no changes are actually made to it.

When the partition table information shown on your screen matches your printed version, write the changes to the disk with the w command; you will be automatically exited from fdisk. Restart fdisk to verify your handiwork, and then remove the rescue disk and reboot.

It helps to practice manually restoring the partition table on an old drive before you have to do it in an emergency situation.

# Booting the System from the Rescue CD

For advanced Linux users, you can use the rescue CD to boot the system (rather than boot the rescue operating system on the CD-ROM) if the boot loader code on your computer is damaged or incorrect. To use the Rescue CD to boot your system from /dev/hda1, for example, first boot the CD and press the F1 key. At the LILO prompt, enter something similar to this example. Note that you are simply telling the boot loader what your root partition is.

```
boot: linux rescue root=/dev/hda1
```

# Booting the System from a Generic Boot Floppy

If you failed to make a boot floppy or cannot locate the one you did make, any Linux boot floppy (a slightly older version or one borrowed from a friend) can be pressed into service as long as it has a reasonably similar kernel version. (The major and minor numbers match—for example, 2.6.5 would likely work with any 2.6 system, but not with a 2.4 system.) You would boot your system by manually specifying the root and boot partitions as described previously. Although you are almost guaranteed to get some error messages, you might at least be able to get a base system running enough to replace files and recover the system.