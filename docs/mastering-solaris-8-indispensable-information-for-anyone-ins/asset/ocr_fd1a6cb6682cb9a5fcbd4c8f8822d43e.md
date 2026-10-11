different). For a system with a single diskette and CD-ROM, you would see the following if you used the ls command:

```
ls -L -1 /vol1/dev
total 0
dr-xr-xr-x 4 root      root   512 Nov 30 14:21  aliases
dr-xr-xr-x 3 root      root   512 Nov 30 11:47  diskette0
dr-xr-xr-x 3 root      root   512 Nov 29 17:03  dsk
dr-xr-xr-x 3 root      root   512 Nov 30 11:47  rdiskette0
dr-xr-xr-x 3 root      root   512 Nov 29 17:03  rdsK
```

You can use the `ls` command again on each of these four device subdirectories to return the diskette name or the CD-ROM name.

# ## Mount Points and Symbolic Links

Unix uses the `/f1oppY` and `/cdrom` mount points to provide access to floppy and CD-ROM devices, and the `/vol1/dev/diskette0` and `/vol1/dev/dsk/c0t2d0` subdirectories are mapped to these mount points. When you use these mount points under `rmount`, you can then access a diskette or CD using the `/f1oppY/<diskettename>` or `/cdrom/<cdname>` mount point. Because the mount points can be used from any location if the disk is formatted, even remote systems if you make these devices available to other users over the network, this simplifies your naming convention. Unformatted disks are only available locally and not from the mount points.

In addition to mount points, you can create symbolic links to removable media. The symbolic links for file system access are as follows:

```
/f1oppY/f10ppy0 → /f1oppY/<diskettename> → /vol1/dev/diskette0/<diskettename>
/cdrom/cdrom0 → /cdrom/<diskname> → /vol1/dev/dsk/c0t2d0/<diskname>
```

Here are the symbolic link for raw device access:

```
/f1oppY/rf10ppy0 → /f1oppY/<diskettename> → /vol1/dev/rdiskette0/<diskettename>
/cdrom/rcdrom0 → /cdrom/<diskname> → /vol1/dev/rdsK/c0t2d0/<diskname>
```

Therefore, you can use the name `cdrom/cdrom0` to access a CD's file system without having to know the name or location of the disk.

Not all CD-ROMs are formatted using only the HFS format. Some disks contain two or more partitions, or slices, and those slices can contain a UFS, SPARC or UFS_x86 slice. This scenario of having multiple disks slices often happens when a disk is set up to install applications for which there will be three slices: Slice0, UFS, SPARC