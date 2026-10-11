# ## How GRUB Treats Disks

GRUB isn't able to tell the difference between IDE and SCSI disks; it just reads the BIOS entries and goes on from there. To make things more predictable, it detects and uses IDE disks before SCSI disks.

The numbering of disks and partitions is a little different from other boot loaders. The following is a representation of the first hard disk and the first partition on that disk:

```
(hd0,0)
```

GRUB numbers its disks from 0, with 0–3 usually being the IDE disks. The partitions are numbered similarly, with 0–3 being the primary partitions and 4 always being the first logical partition on the disk.

The following is the designator for the first floppy on the systems:

```
(fd0)
```

![](bbox=[0.08, 0.42, 0.2, 0.48])

Multiple partitions aren't possible on a floppy, so no partition designator is necessary.

# ## Setting Up GRUB

Installation consists of running the *grub-install* script with parameters or running *grub* and setting up the boot loader while in GRUB.

Here's an example of installing to the first hard disk:

```
grub-install /dev/hda
```

This simply installs the boot loader into the MBR of the first hard disk.

Here's an example of installing to a /boot directory:

```
grub-install -root-directory=/boot /dev/hda
```

This is necessary for a system that uses a small /boot partition to hold the boot files and to avoid the 1024-cylinder problem.

# ## Another GRUB Install Option

You don't have to use the *grub-install* script—you can set up GRUB from the *grub>* prompt. In other words, you might be using a different boot loader and decide to install GRUB without knowing some details, such as the location of the GRUB stage loaders.