# # Root password
rootpw --encrypted $1$/n3yjyDV$AWOBzGRq/1AxRyHx1JSM1

Note that not the output of a sample ks.cfg is shown. However, you can see that this file will feed kickstart directions for an install, including an encrypted root password to be installed on the target Red Hat system.

The next step is to copy your new ks.cfg to a boot disk created using one of the Red Hat boot floppy images (under the images directory on the first Red Hat Linux CD-ROM). You can do this with Linux using the mount and cp commands. For example, take your Red Hat boot disk (created according to directions in the section “Making an Installation Boot Diskette in Chapter 3), insert it into your PC, and then use the mount command (as root) like so:

```
# mount /mnt floppy
```

If Red Hat has mounted your floppy automatically, you'll receive an error message such as /dev/fd0 already mounted. You can then simply copy ks.cfg file to the floppy like so:

```
# cp ks.cfg /mnt/floppy
```

You can verify the contents of the floppy using the ls command like this:

```
# ls /mnt/floppy
boot.msg general.msg inititrd.img ks.cfg llinux.sys
options.msg param.msg rescue.msg snake.msg splash.lss
syslinux.cfg syslinux.png vmlinuz
```

Then unmount the floppy using the umount command like so:

```
# umount /mnt/floppy
```

Remove the disk. It is now ready for use. When you use the disk to boot a PC, after booting, the install boot image you'd like to perform a kickstart install like this:
linux ks=floppy

The installer will then use the specifications outlined in the Kickstart Configurator and saved in ks.cfg to install Red Hat Linux.

# Reference

The following is a list of references you can use to learn a bit about partitioning, installation tools, and installing Red Hat Linux and Linux variants on a variety of hardware-. You'll also find information about installation on hardware for embedded and mainframe solutions.