| Device | Mount | Type | Options | Dump | Pass |
|---|---|---|---|---|---|
| /dev/hda3 | / | ext3 | defaults | 0 | 1 |
| none | /proc | proc | defaults | 0 | 0 |
| none | /dev/pts | devpts | gid=5,mode=620 | 0 | 0 |
| none | /dev/shm | tmpfs | defaults | 0 | 0 |
| /dev/hda2 | swap | swap | defaults | 0 | 0 |
| /dev/hdc | /mnt/cdrom | iso9660 | noauto,owner,kudzu,ro | 0 | 0 |
| /dev/fd0 | /mnt/floppy | auto | noauto,owner,kudzu | 0 | 0 |
| /dev/hda1 | /mnt/windows | vfat | defaults | 0 | 0 |

# CD-ROM and Floppy Defaults

Red Hat creates entries in the fstab file for any CD-ROM and floppy devices you may have. It also creates directories where these drives can be mounted. For Red Hat, these are /mnt/cdrom for your CD-ROM and /mnt/floppy for your floppy disk. If you have several CD-ROMs or floppy drives, directories are created for them with sequential numbers. So on Red Hat, a second CD-ROM drive will use a directory named /mnt/cdrom1.

# Partition Labels: e2label

Red Hat uses file system labels for ext2 and ext3 file systems on hard disk partitions. Thus in the /etc/fstab file previously shown, the first entry would use a label for its device name, as shown here. In this case, the label is the slash, /, indicating the root partition. You could change this device's label with e2label, but be sure to also change the /etc/fstab entry for it.

```
LABEL=/   /   ext3   defaults   0   1
```

For ext2 and ext3 partitions, you can change or add a label with the e2label tool or tune2fs with the -L option. Specify the device and the label name. If you change a label, be sure to change corresponding entries in the /etc/fstab file. Just use e2label with the device name to find out what the current label is. In the next example, the user changes the label of the /dev/hda3 device to TURTLE:

```
e2label /dev/hda3 TURTLE
```

# Windows Partitions

You can mount either MS-DOS, Windows 95/98/ME, or Windows XP, NT, and 2000 partitions used by your Windows operating system onto your Linux file structure, just as you would mount any Linux file system. You have to specify the file type of vfat for Windows 95/98/ME, and msdos for MS-DOS. Windows XP, NT, and 2000 use the ntfs file type. You may find it convenient to have your Windows partitions automatically mounted when you start up your Linux system. To do this, you need to put an entry for your Windows partitions in your /etc/fstab file and give it the defaults option, or be sure to include an auto option. You make an entry for each Windows partition you want to mount, and then specify the device name for that partition, followed by the directory in which you want to mount it. The /mnt/windows directory would be a logical choice (be sure the windows directory has already been created in /mnt). The next example shows a standard Windows partition entry for an /etc/fstab file. Notice the last entry in the /etc/fstab file example is an entry for mounting a Windows partition.

```
/dev/hda1 /mnt/windows vfat defaults 0 0
```