command must be given to the kernel as arguments for the install to begin properly. Red Hat Linux/Alpha supports two varieties of hard drive partitioning:

+   - Standard *fdisk*-style partitioning; this has the usual oddities (such as extended partitions) and is done in the same way as on Intel platforms (using Linux *fdisk*. This is the partitioning style you must use if you are using the ARC console.

+   - BSD-style disk-labelling. It is normal to make the first partition on a disk-labelled hard drive the swap partition. We don't recommend using BSD disk-labelling unless it is absolutely necessary.

# 3.4.3  Finishing Up

After the install is finished and your system is fully configured, you will be asked to reset your computer. This indicates that your system has been successfully installed.

# 3.5  Booting your Red Hat Linux/Alpha system

To boot Red Hat Linux from MILO, you must use the **boot** command. The command differs slightly depending on where your root partition is. For example, if your root partition is the second partition on your first SCSI hard drive, you would boot as follows:

```
boot sda2:vmlinux.gz root=/dev/sda2
```

If instead your root partition is the third partition on your second IDE drive, you would use this command:

```
boot hdb3:vmlinux.gz root=/dev/hdb3
```

For information on these commands and on automating the boot process, please read the MILO HOWTO in Appendix E.