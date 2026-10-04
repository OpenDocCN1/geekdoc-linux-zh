are no old binary files lying about in the source tree to interfere with the compilation of your chosen kernel configuration.

When these have completed successfully, which may take a minute or two, you should go on to start the compilation proper:

```
# make zImage
```

Having entered this command you should now go and take a break because, depending on your processor speed and the amount of memory you have on your system, it could take quite a while to run. A 486DX2/66 with 16 Mb of memory takes about 20 minutes, a 386SX/16 with 4 Mb takes several hours.

Once completed, the system will have generated a ready to install, compressed kernel image in the file:

```
/usr/src/linux/arch/i386/boot/zImage
```

# 7.4.3 Installation

In order to test the new kernel you should make a bootable floppy disk from it, using the procedure you saw in Section 7.3.4 to configure the root filesystem partition name into it first.

If all goes well when you boot the machine from the new floppy disk then you can consider setting up the new kernel to boot from the hard disk, if you wish. Probably the easiest and safest way to do this is to set up an extra kernel in your lilo.conf file and re-run lilo.

The lilo.conf file can be modified as follows:

```
# LILO configuration file
# Global section
boot = /dev/hda
delay = 50

# DOS bootable partition section
other = /dev/hda1
    label = dos
    table = /dev/hda

# New Linux bootable partition section
image = /vmlinuz
    root = /dev/hda3
    label = linux
    read-only

# Old Linux bootable partition section
```