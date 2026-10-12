To see how multivolume archives work, log in as root, place one disk in the floppy drive, and type the following tar command:

```
tar cvfM /dev/fd0 /usr/doc/ghostscript*
```

Note the M option in the option letters, which tells tar to create a multivolume archive. The tar command prompts you for a second floppy when the first one fills to capacity. Take out the first floppy and insert another floppy when you see the following prompt:

```
Prepare volume #2 for `/dev/fd0` and hit return:
```

When you hit Enter, the tar program continues with the second floppy. In this example, you need only two floppies to store the archive. For larger archives, the tar program continues to prompt for floppies in case more floppies are needed.

To restore from this multivolume archive, type cd /tmp to change the directory to /tmp and then type:

```
tar xvfM /dev/fd0
```

The tar program prompts you to feed the floppies as necessary.

![](bbox=[0.16, 0.52, 0.28, 0.62])

Use the du -s command to determine the amount of storage you need to archive a directory. For example, here’s how you can get the total size of the /etc directory in kilobytes:

```
du -s /etc
8040      /etc
```

The resulting output shows that the /etc directory requires at least 8,040K of storage space to back up. If you plan to back up on multiple high-density floppies, you need about 8,040/1,200 = 7 floppies.

# Backing up on Tapes

![](bbox=[0.04, 0.73, 0.13, 0.85])

Although backing up on tapes is as simple as using the right device name in the tar command, you do need to know some nuances of the tape device to use it well. When you use tar to back up to the device named /dev/st0 (the first SCSI tape drive), the tape device automatically rewinds the tape after the tar program finishes copying the archive to the tape. The /dev/st0 device is called a rewinding tape device because it rewinds tapes by default.