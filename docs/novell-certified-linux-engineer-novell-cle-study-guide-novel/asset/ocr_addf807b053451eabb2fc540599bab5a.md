On most Linux systems, however, there are three partitions by default, as shown in Figure 2.6.

```
```
Br1: # fdisk /dev/sda

Command (m for help): p

Disk /dev/sda: 295 heads, 63 sectors, 522 cylinders
Units = cylinders of 16065 * 512 bytes

 Device Boot     Start   End Blocks Id System
/dev/sda1 *          1     2 16033+ 83 Linux
/dev/sda2           3    68 530145 82 Linux swap
/dev/sda3         69   522 3646755 83 Linux

Command (m for help): ```
```

# ### FIGURE 2.6
Default Linux partitions.

+   - **/boot**—This partition is an EXT2, EXT3, or ReiserFS partition, and it is usually 50MB to 100MB in size. This partition is represented by the first entry in the list of partitions shown in Figure 2.6. Notice that it is the only partition marked as bootable. It contains the Linux startup files. Because it is a bootable partition, it must reside within the first 1,024 cylinders of the hard disk drive, although this usually isn't a problem. Most Linux install programs can automatically partition your hard disk for you, and they will ensure that this partition resides where it should on the disk. This becomes an issue if you decide to manually partition the drive, or if you are creating a dual-boot system.

+   - **/**—This partition is an EXT2, EXT3, or ReiserFS partition and is mounted at the root directory of the hierarchical file system. It contains the Linux system files, utilities, and user files. It is represented by the third partition displayed in Figure 2.6.

+   - **Swap**—If you're familiar with Windows, you know that every version since Windows 3.0 creates a swap file on the hard drive. Linux does things a little bit differently. Instead of a file in the file system, Linux uses a dedicated swap partition. This is the second partition shown in Figure 2.6. Again, if you let your Linux install program partition your drive for you, it should automatically determine the proper size for you. If you manually partition your hard drive, the general rule of thumb is that the swap partition should be at least as big as the amount of RAM in the system.