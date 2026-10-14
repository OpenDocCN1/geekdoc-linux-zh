
The `fsck` utility (usually pronounced FIZZ-check) checks the integrity of your file systems, making certain that each inode is correctly linked to a file, that the blocks of each file can be found, and so forth. The `fsck` utility can also repair minor file system problems. `fsck` is a front end that uses checking programs specific to the file system type that you want to check. For example, if you run `fsck` on a standard `ext3` file system, `fsck` uses the program `fsck.ext2` to check the file system (`ext2` and `ext3` are so similar that the same program is used for both).

In older Linux systems, the `fsck` program was run automatically after a file system had been mounted a certain number of times (20 was the default). That is no longer the case, and `fsck` does not check your file systems unless you explicitly start it yourself. It's a good idea to do this every few months on a busy system to make certain no hard disk errors are creeping in.

The challenge is that `fsck` must be run on a file system that is not mounted. In order to check your root Linux file system, you must start your computer from a removable disk and run `fsck`. Conversely, if you have multiple data partitions (for example, a separate partition for the `/home` directory), you might be able to unmount and check that file system when users are unlikely to need access to it.

Creating a removable disk that you can use for this type of system check or other troubleshooting needs is described in Chapter 15, “Advanced Topics and Troubleshooting.”

To use `fsck`, you simply supply the device name you want to have checked. For example:

```
fsck /dev/hda1
```

If you don’t supply a device name, `fsck` tries to check all of the file systems listed in the `/etc/fstab` file, which is described later in this section. The superblock of an `ext3` file system maintains information about how many times the file system has been mounted since it was last checked by `fsck` and the last date and time it was checked.

## Creating New File Systems

As a Linux system grows, it often requires additional storage space. As you will learn in Chapter 13, you can use backup systems to remove unused information and store it on compact disc, streaming tape, or other devices. Nevertheless, the amount of “live” storage needed often grows to exceed an administrator’s original expectations. In fact, part of planning a Linux system in an organization is knowing in advance what steps to take when the system must be expanded. If these steps are outlined in advance, a system administrator is less likely to make choices that create obstacles to efficient system upgrades later on.

Adding a file system generally means adding a hard disk device to your system and making that hard disk available to Linux by formatting and mounting it. This is done for the root file system as part of the Linux installation process. But in that case, the installation utility takes care of most of the details. In this section you will learn how to set up additional file systems stored on a hard disk, CD-ROM, or other devices.

You can install new file systems that are permanent (loaded each time you start Linux) or temporary (loaded only occasionally, as needed). File systems can be stored on a device with removable media (such as a cartridge) or fixed media (such as a hard disk).

To install a new hard disk or other peripheral device, consult your hardware manual. Once the hard disk or other device is installed, you can use the Linux `fdisk` command described in the next section to examine its partitions, creating new Linux partitions as needed. Before any hard disk can be used as a native Linux file system, it must have Linux partitions defined.

## Using the fdisk Utility

Almost all file system devices use either an IDE or SCSI interface to communicate with your computer (this includes file systems stored on USB hard disks, which use the SCSI device names in Linux, such as `/dev/sda4`).
