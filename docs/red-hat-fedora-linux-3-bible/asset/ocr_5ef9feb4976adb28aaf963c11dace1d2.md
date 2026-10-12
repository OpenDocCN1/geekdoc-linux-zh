RAID partitions. RAID5 is for parity, so there is always one backup disk if a disk goes bad. You need at least three RAID partitions to use RAID5.

+   * **RAID Members** — From the RAID partitions you created, select which ones are going to be members of the RAID device you are creating.
+   * **Number of spares** — Select how many spares are available to the RAID device.

The new RAID Device should appear on the Disk Setup (Disk Druid) window. Click **Next** to continue with installation.

Once installation is complete, you can check your RAID devices by using a variety of tools that come with Fedora. Commands for working with RAID partitions come in the **raidtools** package. Using raidtools commands, you can list and reconfigure your RAID partitions.

# Checking system space

Running out of disk space on your computer is not a happy situation. Using tools that come with Fedora, you can keep track of how much disk space has been used on your computer, and you can keep an eye on users who consume a lot of disk space.

# Displaying system space with df

You can display the space available in your file systems using the **df** command. To see the amount of space available on all of the mounted file systems on your Linux computer, type **df** with no options:

```
```
$ df
Filesystem   1k-blocks    Used Available Use% Mounted on
/dev/hda3     30645460 2958356 26130408  11% /
/dev/hda2       46668   8340   35919  19% /boot
/dev/fd0         1412     13   1327   1% /mnt/floppy
```
```

The output here shows the space available on the hard disk partition mounted on the root partition (`/dev/hda1`), boot partition (`/dev/hda2`), and the floppy disk mounted on the `/mnt/floppy` directory (`/dev/fd0`). Disk space is shown in 1K blocks. To produce output in a more human-readable form, use the `-h` option as follows:

```
```
$ df -h
Filesystem   Size Used Avail Use% Mounted on
/dev/hda3     29G  2.9G   24G  11% /
/dev/hda2     46M  8.2M   25M  19% /boot
/dev/fd0      1.4M  13K  1.2M   1% /mnt/floppy
```
```

With the **df -h** option, output appears in a friendlier megabyte or gigabyte listing. Other options with **df** let you:

+   * Print only file systems of a particular type (-t *type*)
+   * Exclude file systems of a particular type (-x *type*)