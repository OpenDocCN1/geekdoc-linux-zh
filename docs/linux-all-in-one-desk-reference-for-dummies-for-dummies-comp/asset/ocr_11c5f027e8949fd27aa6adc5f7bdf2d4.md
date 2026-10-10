# ## 204
### Navigating the File System with Linux Commands

Log in as **root** (or type **su** - to become **root**), insert the DVD-ROM in the DVD drive, and then type the following command:

```
mount /dev/hdc /media/cdrom0
```

This command mounts the file system on the device named `/dev/hdc` (an IDE DVD/CD-ROM drive) on the `/media/cdrom0` directory (which is also called the *mount point*) in the Linux file system.

After the `mount` command successfully completes its task, you can access the files on the DVD-ROM by referring to the `/media/cdrom0` directory as the top-level directory of the disc. In other words, to see the contents of the DVD-ROM, type

```
ls -P /media/cdrom0
```

When you're done using the DVD-ROM — and before you eject it from the drive — you have to unmount the disc drive with the following `umount` command:

```
umount /dev/hdc
```

![](bbox=[0.13, 0.49, 0.23, 0.56])

You can mount devices on any empty directory on the file system. However, each distribution has customary locations with directories meant for mounting devices. For example, some distributions use directories in `/mnt` whereas others use the `/media` directory for the mount points.

# ### Commands for checking disk-space usage

I want to tell you about two commands — `df` and `du` — that you can use to check the disk-space usage on your system. These commands are simple to use. The `df` command shows you a summary of disk-space usage for all mounted devices. For example, when I type `df` on a PC with many mounted storage devices, here’s what I get as output of the `df` command:

| Filesystem | 1K-blocks | Used | Available | Use% | Mounted on |
|---|---|---|---|---|---|
| /dev/hdb6 | 28243372 | 2377232 | 25872080 | 9% | / |
| tmpfs | 383968 | 12 | 383956 | 1% | /dev/shm |
| /dev/hda5 | 5766924 | 1422232 | 4051744 | 26% | /usr/boot |
| /dev/hda7 | 6258100 | 2989200 | 2951004 | 51% | /debian/boot |
| /dev/hda9 | 5766924 | 1422232 | 4051744 | 26% | /ubuntu |
| /dev/hda10 | 5766924 | 1872992 | 3600984 | 35% | /mepla |
| /dev/hda11 | 6258100 | 2989200 | 2951004 | 51% | /debian |
| /dev/hdb1 | 19585800 | 1370172 | 18188238 | 8% | /android |
| /dev/hdb2 | 16897676 | 10593364 | 5434312 | 66% | /windows/C |
| /dev/hdb1 | 107426620 | 9613028 | 97813592 | 9% | /windows/D |

The output is a table that lists the device, the total kilobytes of storage, how much is in use, how much is available, the percentage being used, and the mount point.