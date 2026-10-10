# ## The Fedora Rescue Disc

Fedora provides a rescue disc hidden in the installation DVD. To use it, insert the disc and reboot the computer, booting from the DVD just as you did when you installed Fedora originally. At the intro screen, press the F1 key to see all the available choices, but simply enter `Linux rescue` at the LILO boot prompt to enter rescue mode, like so:

```
boot: linux rescue
```

You will learn more about the rescue mode later in this section, but feel free to explore it at any time. A graphical interface is not available, so you need to bone up on your command-line skills. If necessary, you can perform all the operations discussed in this section from rescue mode.

# ## Backing Up and Restoring the Master Boot Record

The Master Boot Record (MBR) is the first 512 bytes of a hard disk. It contains the boot loader code in the first 446 bytes and the partition table in the next 64 bytes; the last two bytes identify that sector as the MBR. The MBR can become corrupted, so it makes sense to back it up.

This example uses the dd command as root to back up the entire MBR. If the boot loader code changes from the time you make this image and restore the old code, the system will not boot when you restore it all; it is easy enough to keep a boot floppy disk handy and then rerun LILO if that is what you are using.

To copy the entire MBR to a file, use this:

```
# dd if=/dev/hda of=/tmp/hdamb bs=512 count=1
```

To restore the entire MBR, use this:

```
# dd if=/tmp/hdamb of=/dev/hda bs=512 count=1
```

To restore only the partition table, skipping the boot loader code, use this:

```
# dd if=/tmp/hdamb of=/dev/hda bs=1 skip=446 count=66
```

Of course, it would be prudent to move the copy of the MBR to a floppy disk or other appropriate storage device. (The file is only 512 bytes in size.) You will need to be able to run dd on the system to restore it (which means that you will be using the Fedora rescue disc, as described later, or any equivalent to it).

# ## Manually Restoring the Partition Table

A different way of approaching the problem is to have a printed copy of the partition table that can then be used to restore the partition table by hand with the Fedora rescue disc and the fdisk program.