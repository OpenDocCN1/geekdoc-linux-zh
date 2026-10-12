
## Chapter 10: Understanding System Administration

- 10. If you are using the entire hard disk, use the last cylinder number shown. Otherwise, choose the ending cylinder number or indicate how many megabytes the partition should have.
- 11. To create more partitions on the hard disk, repeat steps 6 through 10 for each partition.
- 12. Type `w` to write changes to the hard disk. At this point, you should be back at the shell.
- 13. To make a file system on the new disk partition, use the `mkfs` command. By default, this command creates an ext2 file system, which is useable by Linux. To create an ext3 file system on the first partition of the second hard disk, type the following:

    ```bash
    # mkfs -t ext3 /dev/hdb1
    ```

    If you created multiple partitions, repeat this step for each partition (such as /dev/hdb2, /dev/hdb3, and so on).

    > **TIP:** If you don't use -t ext3 as shown above, an ext2 file system is created by default. Use other commands, or options to this command, to create other file system types. For example, use `mkfs.vfat` to create a VFAT file system, `mkfs.msdos` for DOS, or `mkfs.reiserfs` for Reiser file system type. The `tune2fs` command, described later in this section, can be used to change an ext2 file system to an ext3 file system.

- 14. Once the file system is created, you can have the partition permanently mounted by editing the /etc/fstab and adding the new partition. Here is an example of a line you might add to that file:

    ```bash
    /dev/hdb1    /abc    ext3    defaults    1 1
    ```

    In this example, the partition (/dev/hdb1) is mounted on the /abc directory as an ext3 file system. The defaults keyword causes the partition to be mounted at boot time. The numbers 1 1 cause the disk to be checked for errors. Add one line like the one shown above for each partition you created.

- 15. Create the mount point. For example, to mount the partition on /abc (as shown in the previous step), type the following:

    ```bash
    # mkdir /abc
    ```

    Create your other mount points if you created multiple partitions. The next time you boot Fedora, the partition will be automatically mounted on the /abc directory, as well any other partitions you added.

After you have created the file systems on your partitions, a nice tool for adjusting those file systems is the tune2fs command. Using tune2fs, you can change volume labels, how often the file system is checked, and error behavior. You can also use tune2fs to change an ext2 file system to an ext3 file system so the file system can use journaling. For example:

```
# tune2fs -J /dev/hdb1
tune2fs 1.35-WIP, (07-Dec-2003)
Creating journal inode: done
This filesystem will be automatically checked every 38 mounts or
180 days, whichever comes first. Use tune2fs -c or -i to override.
```

By adding the -j option to tune2fs, you can change either the journal size or attach the file system to an external journal block device. After you have used tune2fs to change your file system type, you probably need to correct your /etc/fstab file to include changing the file system type from ext2 to ext3.

### Using RAID disks

RAID (Redundant Arrays of Independent Disks) is used to spread the data used on a computer across multiple disks, while appearing to the operating system as if it is dealing with a single disk partition. Using the different RAID specifications, you can achieve the following advantages:

- **Improved disk performance** — RAID0 uses a feature called *striping*, where data is striped across multiple RAID partitions. Striping can improve disk performance by spreading the hits on a computer’s file system across multiple partitions, which are presumably on multiple hard disks.
- **Mirroring** — RAID1 uses partitions from multiple hard disks as mirrors. That way, if one of the partitions becomes corrupted or the hard disk goes down, the data exists on a partition from another disk because it has continuously maintained an exact mirror image of the original partition.
- **Parity** — Although striping can improve performance, it can increase the chance of data loss, since any hard-disk crash in the array can potentially cause the entire RAID device to fail. Using a feature called *parity*, information about the layout of the striped data is kept so that data can be reconstructed if one of the disks in the array crashes. RAID3, 4, and 5 implement different levels of parity.

During installation of Fedora, you can use the Disk Druid window to create RAID0, RAID1, and RAID5 disk arrays. The following procedures describe how to set up RAID disks during installation.

Before you begin creating RAID partitions when you install Fedora, you will probably want to start with a computer that has two or more hard disks. The reason is that, if you don’t have multiple hard disks, you won’t get the performance gains that come from spreading the hits on your computer among multiple disks. Likewise, mirroring will be ineffective if all RAID partitions are on the same disk, because the failure of a single hard disk would still potentially cause the mirrored partitions to fail as well.

For example, you might begin with 30GB of free disk space on your first hard disk (/dev/hda) and 30GB of free disk space on your second hard disk (/dev/hdb). During the Fedora installation procedure, select to partition your disk with Disk Druid. Then follow this procedure:

- 1. From the Disk Setup (Disk Druid) window, click the RAID button. A RAID Options window appears.
- 2. Select Create a Software RAID Partition, and click OK. The Add Partition window appears.
- 3. With Software RAID selected as the File System Type, choose the drive you want to create the partition on and choose the size (in megabytes). Then click OK.
- 4. Repeat steps 2 and 3 (presumably creating software RAID partitions on different hard disks until you have created all the RAID partitions you want to use).
- 5. Click the RAID button again. Select Create a RAID Device [default=/dev/md0] and click OK. The Make RAID Device window appears, as shown in Figure 10-4.

![](img/b22364e57409c2481ba806e4e6b9309c_416_0.png)

> Figure 10-4: Join multiple RAID partitions to form a single RAID device.

- 6. You need to select the following information about your RAID device and click OK:
    - **Mount Point** — The point in the file system associated with the RAID device. You might be creating the RAID device for a part of the file system for which you expect there to be a lot of hits on the hard disk (such as the /var partition).
    - **File System Type** — For a regular Linux partition, choose ext3. You can also select LVM, swap, or VFAT as the file system type.
    - **RAID Device** — The first RAID device is typically md0 (for /dev/md0).
    - **RAID Level** — Allowable RAID levels are RAID0, RAID1, and RAID5. RAID0 is for striping (essentially dividing the RAID device into stripes across RAID partitions you have selected). RAID1 is for mirroring so that the data is duplicated across all RAID partitions. RAID5 is for parity, so there is always one backup disk if a disk goes bad. You need at least three RAID partitions to use RAID5.
    - **RAID Members** — From the RAID partitions you created, select which ones are going to be members of the RAID device you are creating.
    - **Number of spares** — Select how many spares are available to the RAID device.

The new RAID Device should appear on the Disk Setup (Disk Druid) window. Click **Next** to continue with installation.

Once installation is complete, you can check your RAID devices by using a variety of tools that come with Fedora. Commands for working with RAID partitions come in the **raidtools** package. Using raidtools commands, you can list and reconfigure your RAID partitions.

### Checking system space

Running out of disk space on your computer is not a happy situation. Using tools that come with Fedora, you can keep track of how much disk space has been used on your computer, and you can keep an eye on users who consume a lot of disk space.

### Displaying system space with df

You can display the space available in your file systems using the **df** command. To see the amount of space available on all of the mounted file systems on your Linux computer, type **df** with no options:

```
$ df
Filesystem   1k-blocks    Used Available Use% Mounted on
/dev/hda3     30645460 2958356 26130408  11% /
/dev/hda2       46668   8340   35919  19% /boot
/dev/fd0         1412     13   1327   1% /mnt/floppy
```

The output here shows the space available on the hard disk partition mounted on the root partition (`/dev/hda1`), boot partition (`/dev/hda2`), and the floppy disk mounted on the `/mnt/floppy` directory (`/dev/fd0`). Disk space is shown in 1K blocks. To produce output in a more human-readable form, use the `-h` option as follows:

```
$ df -h
Filesystem   Size Used Avail Use% Mounted on
/dev/hda3     29G  2.9G   24G  11% /
/dev/hda2     46M  8.2M   25M  19% /boot
/dev/fd0      1.4M  13K  1.2M   1% /mnt/floppy
```

With the **df -h** option, output appears in a friendlier megabyte or gigabyte listing. Other options with **df** let you:

- Print only file systems of a particular type (-t *type*)
- Exclude file systems of a particular type (-x *type*)
