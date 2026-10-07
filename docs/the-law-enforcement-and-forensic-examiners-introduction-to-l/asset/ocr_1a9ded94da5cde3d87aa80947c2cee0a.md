# v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

There's a lot of information provided in the file output. We get the ID's, number of sectors (this is read from meta data, not the image size itself), serial number, and other identifiers. We'll cover images with separate partitions in a moment. This is a simple image of a file system that is not part of a partition table. You may see such images where USB drives or other removable media have been imaged.

A quick word on using the file command directly on devices. The file command will provide a response on exactly the object you refer. If you run file on /dev/sda, for example I noticed that it is a block special file. If you want to know more about the device rather than the device file, use the -s option to specify that we want to know about the device being referenced by the /dev block device. Try this on your own system.

```
root@forensic1:~# file /dev/sda
dev/sda: block special (8/0)
```

```
root@forensic1:~# file -s /dev/sda
dev/sda: DOS/MBR boot sector, Linux i386 boot LOader; partition 1 ID=0xee,start-CHS (0x0,2), end-CHS (0x3ff,255,63), startsector 1, 234441647 sectors
```

So we know what file system we are dealing with, we need to mount the image as a device to see the contents. For that we can use a loop device.

# The Loop Device

We can mount the file system(s) within the image using the loop interface. Basically, this allows you to "mount" a file system within an image file (instead of a disk) to a mount point and browse the contents. In simple terms, the loop device acts as a "proxy disk" to serve up the file system as if it were on actual media.

# Loop option to mount the command

For a simple file system image (where there not multiple partitions in the image), we can use the same mount command and the options as any other file system on a device, but this time we include the option loop to indicate that we want to use the loop device to mount the file system within the image file. Change to the directory where placed the fat_fs.raw, and follow the following (skip the mkdir command if you already created this directory in our earlier section on mounting external file systems):

```
root@forensic1:~# mkdir /mnt/analysis
```

```
root@forensic1:~# mount -t vfat -o ro,loop fat_fs.raw /mnt/analysis/
```

```
root@forensic1:~# ls /mnt/analysis/
```

151