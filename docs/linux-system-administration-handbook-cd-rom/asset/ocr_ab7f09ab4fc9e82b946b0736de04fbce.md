# 2.1 LILO

needs (you'll enter a number for which video mode you choose), you can replace the ask parameter with the number you choose. One important line here is the image section. This line tells LILO which file to boot. Some Linux installations configure the kernel to be in the root partition (/) and some the kernel in the /boot directory. You should be sure which setting you want to use when configuring LILO. A feature of the image line is you can boot multiple versions of the kernel all using the same Linux installation. For example, if you're developing new kernels and want to have a “safe” kernel around that you know boots correctly, you can create a “safe” entry in LILO. Its configuration would look something like this:

```
# Create a safe entry for Linux.
image = /boot/vmlinuz.safe  # Boot this file. Make sure it exists!
label = safe                # The label for this is "safe"
root = /dev/hda2            # Specify the root partition just in case
vga = ask                   # Not really needed, but helpful
append = "hdc=cdrom"      # Make sure Linux knows about the CD-ROM
```

In the event that a kernel you build doesn't work correctly and you are unable to boot it, you can just enter “safe” in the LILO prompt and boot the older kernel. Note that this will not help if there is some problem related to the kernel, like hardware failure or serious partition corruption.
Once /etc/lilo.conf file is configured to your liking, you can run the /sbin/lilo command as root to install the configuration file. The next time you boot the machine, you will see the LILO boot prompt. If at some future time you need to remove LILO from your system, you can do this from DOS (and presumably Windows 95 as well) with the fdisk /mbr command. This tells fdisk to reinstall the Master Boot Record (MBR) to the first partition of the first drive.

# rdev Command

The rdev command allows you to change parameters without using LILO. For example, you can use the dd command to put a Linux kernel on a diskette, move it to another machine to boot. To change the root partition, you can just use the following command:

```
rdev kernel root
```

Where the kernel is the kernel file and root is the new root partition you want to use, if the kernel is on a floppy diskette (used dd to put it there or make floppy when compiling the kernel), the command would look like this: