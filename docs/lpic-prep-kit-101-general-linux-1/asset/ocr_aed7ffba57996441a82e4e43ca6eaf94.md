The command to create a tar file containing all the files in the `pwd` is

```
tar cf myarchive.tar .
```

This command causes the contents of the `pwd`, including any subdirectories, to be tarred into the file `myarchive.tar`. The `c` switch creates the `tar` file, and the `t` modifier provides the name for this new archive. The trailing dot (.) is used to specify the current working directory.

In addition, you can use the `f` option to specify the device name, as in

```
tar cf /dev/tape /
```

This command creates an archive of the entire root filesystem to the tape device. This overwrites any existing contents on the tape with the new archive, so be sure there is not anything on the tape you need to keep.

When creating an archive on a tape device, you usually have to specify the blocking factor by using the `b` modifier, as in the following example:

```
tar cvfb /dev/tape 20 /
```

The blocking factor times 512 bytes instructs `tar` as to how much data can be written at a time. A blocking factor of 20 can be used with most tape devices. When reading tapes, you do not need to specify the block size.

# Key Concept

> When a modifier requires an argument, the argument is listed after all modifiers are specified. These arguments must be in the same order as the modifiers are listed.

If your backup will span multiple tapes or disks, you will need to specify the media's length, as well as indicate that this will be a multi-volume archive. This can be a problem when backing up a large amount of data, especially if you are also are compressing the backup.

When backing up to floppy disks, your backup probably will span multiple floppies. You will need to specify the size of the floppy and tell `tar` that the backup will span multiple disks, as in the following:

```
tar cnfM /dev/fd0 1200 /home/*
```

This command tells `tar` to create a `tar` file on the floppy device (`/dev/fd0`), which is 1200 bytes in size and contains all the files in the `/home` directory. The `M` tells `tar` that this archive will span multiple volumes. When the first one is full, you will have to manually change the backup media.