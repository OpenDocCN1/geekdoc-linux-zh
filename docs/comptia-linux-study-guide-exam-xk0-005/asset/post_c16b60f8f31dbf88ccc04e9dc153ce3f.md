
indexing files and folders and tracking file access. The `mkfs` program creates all the index files and tables necessary for the specific filesystem.

![](img/c0a399aca0d18f8822d714ad0a173123_409_0.png)

Be very careful when specifying the partition device filename. When you format a partition, any existing data on the partition is lost. If you specify the wrong partition name, you could lose important data or make your Linux system unable to boot.

## Mounting Filesystems

Once you've formatted a drive partition with a filesystem, you can add it to the virtual directory on your Linux system. This process is called *mounting* the filesystem. You can either manually mount the partition in the virtual directory structure from the command line or allow Linux to automatically mount the partition at boot time. The following sections walk through both of these methods.

## Manually Mounting Devices

To temporarily mount a filesystem to the Linux virtual directory, use the *mount* command. The basic format for the *mount* command is:

```bash
mount -t fstype device mountpoint
```

Use the *-t* command-line option to specify the filesystem type of the device:

```bash
$ sudo mount -t ext4 /dev/sdb1 /media/usbl
$ 
```

If you specify the *mount* command with no parameters, it displays all of the devices currently mounted on the Linux system. Be prepared for a long output, though, as most Linux distributions mount lots of virtual devices in the virtual directory to provide information about system resources. Listing 11.1 shows a partial output from a *mount* command.

### Listing 11.1 Output from the mount command

```bash
$ mount
...
/dev/sda2 on / type ext4 (rw,relatime,errors=remount-ro,data=ordered)
/dev/sda1 on /boot/efi type vfat
(rw,relatime,fmask=0077,dmask=0077,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro)
...
/dev/sdb1 on /media/usbl type ext4 (rw,relatime,data=ordered)
/dev/sdb2 on /media/usb2 type ext4 (rw,relatime,data=ordered)
rich@rich-TestBox2:~$
```

To save space, we trimmed down the output from the `mount` command to show only the physical devices on the system. The main hard drive device (`/dev/sda`) contains two partitions, and the USB memory stick device (`/dev/sdb`) also contains two partitions.

> **NOTE**
>
> The `mount` command uses the `-o` option to specify additional features of the filesystem, such as mounting it in read-only mode, user permissions assigned to the mount point, and how data is stored on the device. These options are shown in the output of the `mount` command. Usually you can omit the `-o` option to use the system defaults for the new mount point.

The downside to the `mount` command is that it only temporarily mounts the device in the virtual directory. When you reboot the system, you have to manually mount the devices again. This is usually fine for removable devices, such as USB memory sticks, but for more permanent devices it would be nice if Linux could mount them for us automatically. Fortunately for us, Linux can do just that.

To remove a mounted drive from the virtual directory, use the `umount` command (note the missing `n`). You can remove the mounted drive by specifying either the device filename or the mount point directory.

## Automatically Mounting Devices

For permanent storage devices, Linux maintains the `/etc/fstab` file to indicate which drive devices should be mounted to the virtual directory at boot time. The `/etc/fstab` file is a table that indicates the drive device file (either the raw file or one of its permanent `udev` filenames), the mount point location, the filesystem type, and any additional options required to mount the drive. Listing 11.2 shows the `/etc/fstab` file from an Ubuntu workstation.

### Listing 11.2 The `/etc/fstab` file

```bash
$ cat /etc/fstab

# /etc/fstab: static file system information.
#

# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/sda2 during installation
UUID=46a8473c-8437-4d5f-a6a1-6596c492c3ce / ext4 errors=remount-ro 0 1
# /boot/efi was on /dev/sda1 during installation
UUID=864B-62F5 /boot/efi vfat umask=0877 0 1
# swap was on /dev/sda3 during installation
UUID=8673447a-0227-47d7-a67a-e68b37dd7188 none swap sw
/ 0
```

This `/etc/fstab` file references the devices by their `udev` UUID value, ensuring that the correct drive partition is accessed no matter the order in which it appears in the raw device table. The first partition is mounted at the `/boot/efi` mount point in the virtual directory. The second partition is mounted at the root (`/`) of the virtual directory, and the third partition is mounted as a swap area for virtual memory.

You can manually add devices to the `/etc/fstab` file so that they are mounted automatically when the Linux system boots. However, if they don't exist at boot time, that will generate a boot error.

> **TIP**
>
> On Linux servers using systemd, if you only use the `/etc/fstab` file, systemd still manages these filesystems. The mount points listed in `/etc/fstab` are converted into native units when either the server is rebooted or systemd is reloaded. In fact, using `/etc/fstab` for persistent filesystems is the preferred method over manually creating a mount unit file. For more information on this process, type `man systemd-fstab-generator` at the command line.

> **NOTE**
>
> If you use the `encryptfs` filesystem type on any partitions, they will appear in the `/etc/crypttab` file and will be mounted automatically at boot time. While the system is running, you can also view all of the currently mounted devices, whether they were mounted automatically by the system or manually by users, by viewing the `/etc/mtab` file.

## Managing Filesystems

Once you've created a filesystem and mounted it to the virtual directory, you may have to manage and maintain it to keep things running smoothly. The following sections walk through some of the Linux utilities available for managing the filesystems on your Linux system.

### Retrieving Filesystem Stats

As you use your Linux system, there's no doubt that at some point you'll need to monitor disk performance and usage. There are a few different tools available to help you do that:

- `df` displays disk usage by partition.
- `du` displays disk usage by directory, good for finding users or applications that are taking up the most disk space.
- `iostat` displays a real-time chart of disk statistics by partition.
- `lsblk` displays current partition sizes and mount points.

A quick way to get a snapshot of the disk space situation on your Linux system is to use the `df` and `du` commands:

```bash
$ df -t xfs -h
Filesystem    Size Used Avail Use% Mounted on
/dev/mapper/r1-root   15G  6.6G  7.7G  47% /
/dev/sda1     1014M  351M  664M  35% /boot

$ sudo du -d 1
318632    ./boot
0         ./dev
0         ./proc
9448      ./run
0         ./sys
32400     ./etc
48        ./root
704712    ./var
5711056   ./usr
114656    ./home
369421    ./media
0         ./mnt
18856     ./opt
0         ./srv
12        ./tmp
7279241   .
$  
```

The `df` command shows the overall disk space available on the system, and the `du` command helps show what directories have the most data in them.

In addition to these tools, the `/proc` and `/sys` folders are special filesystems that the kernel uses for recording system statistics. Two directories that can be useful when working with filesystems are the `/proc/partitions` and `/proc/mounts` folders, which provide information on system partitions and mount points, respectively. Additionally, the `/sys/block` folder contains separate folders for each mounted drive, showing partitions and kernel-level stats.
