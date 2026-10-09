```
# growisofs -dvd-compat -Z /dev/cd0=bert.udf
```

UDF files can be huge. Go make some tea. Eventually, you’ll have a burned disk.

# Writing Images to Thumb Drives

USB thumb drives have increasingly supplanted optical disks, thanks in part to their reusability. FreeBSD supports writing disk images to thumb drives with dd(1).

Be very certain which device node is your thumb drive and which is your system hard drive. Thumb drives show up as /dev/da devices, exactly like many hard drives. Overwriting the wrong hard drive is embarrassing.3

The dd(1) command looks confusing at first glance.

```
# dd @if=inputfile @of=outputdevice @bs=1M @conv=sync
```

The if= argument ① gives the file you want to copy. The of= argument ② is the device node to copy to. The bs= flag ③ gives the amount to copy at one time. Without this, dd(1) copies in 512-byte increments. The conv= argument ④ gives dd(1) instructions about how to convert the incoming file. In this case, sync tells dd(1) to synchronize the size of the incoming and outgoing buffer. To burn bertimage.udf to thumb drive /dev/da9, I would run:

```
# dd if=bert.udf of=/dev/da9 bs=1m conv=sync
```

Wait a bit, and you’ll have an imaged thumb drive. Other uses of dd(1) might not need the conv= flag, but always use bs.

Now let’s look at some other filesystems you might find useful.

# Memory Filesystems