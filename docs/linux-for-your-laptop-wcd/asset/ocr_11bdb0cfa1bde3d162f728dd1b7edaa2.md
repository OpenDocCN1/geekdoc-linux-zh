![](bbox=[0.06, 0.08, 0.58, 0.43])

# Step-by-Step Installation of Red Hat Linux

This section details a step-by-step installation of the latest version of Red Hat Linux. As you know by now, there are many different ways to install Linux and different Linux distributions. This section details one way to install Linux—by booting using a boot disk with an inserted CD-ROM.

The easiest way to install Linux is to boot directly from CD-ROM. You'll need to make sure your notebook's BIOS supports booting from CD, and that the CD-ROM device is listed as the first device, as shown in Figure 5.5.

You'll generally find boot images included on your Linux CD under the /images directory. To quickly create a boot disk using Linux, mount the CD, insert a blank floppy disk, and use the Linux dd command like this:

```
# mount /mnt/cdrom
# dd if=/mnt/cdrom/images/boot.img of=/dev/fd0
```

This will create a boot disk. You can then reboot to perform your installation. If you're using DOS, use the RAWRITE command (found under the /dosutils directory) to create your boot disk.

# Installation

When the installer boots, you'll see the first installation screen, as shown in Figure 5.6.