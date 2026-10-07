+   • Join a Linux user group if there is one in your area. If there isn't one, start one. The exposure that you get to different problems will help you avoid those problems on your systems.

+   • Remember to sync after you make changes in rescue mode before you exit. This writes any residual information in the buffers to the hard drive. Not doing this may cause your "fix" to be lost after a reboot.

+   • Don't be afraid of the system. Very few things that you do are going to break the computer (except getting mad and throwing it on the floor). Experiment a bit. Log each step so that you can undo what you did. Make sure you have a boot disk or a rescue disk or CD-ROM. Of course, you don't want to delete files with reckless abandon, but it is okay to copy something to another partition and then remove the suspect file to see if it fixes the problem. If you mess up badly, boot into rescue mode and copy the files back to where they go and reboot.

The rest of the chapter looks at common problems and their solutions. We focus on questions that are asked frequently in the various Linux lists and newsgroups and that are pretty much distribution-independent. There are many frequently asked questions (FAQ) documents available that provide information about specific areas. Look for a FAQ whenever you are preparing to configure something for the first time. If there is not a FAQ, rely instead on a HOWTO, if that is available.

# Boot Problems

The problems we discuss in this section prevent the system from booting up fully. Boot problems are among the most frustrating, but they are also among the easiest to troubleshoot since the problem space is relatively restricted. If you know the boot process inside and out, the symptoms of the problem tend to point to the one or two possible solutions that produce exactly those symptoms. At that point, troubleshooting the problem becomes easy. Find some indicator of which of the possible problems you are dealing with, and fix it.

# FDISK Doesn't Recognize GNU/Hurd Partition

In anticipation of the GNU Hurd filesystem, the developers of the FDISK utility have assigned the partition code 0x63. This partition type is not currently used, so if you can't get FDISK to recognize your Hurd-owned filesystem, use the standard 0x83 if the filesystem contains an ext2 or ext3 filesystem. Do not use the new 0x63 code.

# Making a New Boot Floppy to Replace a Lost One

Sometimes in your career as a system administrator, you will come upon a system that won't boot from as usual and have to use a boot floppy to boot it. This might be that the boot record is corrupted or that the boot floppy usually used is missing. Either way, if you don't have a boot floppy, you'll have to make one.

# LILO

There are two ways to replace a lost or destroyed boot floppy with a new one:

+   • Insert an unused floppy into the first floppy drive and run (as root) lilo -b /dev/fd0. This will make an exact copy of your hard disk boot sector on that floppy so that the next time something kills your boot record, just insert that floppy and boot from it. If you're using a boot