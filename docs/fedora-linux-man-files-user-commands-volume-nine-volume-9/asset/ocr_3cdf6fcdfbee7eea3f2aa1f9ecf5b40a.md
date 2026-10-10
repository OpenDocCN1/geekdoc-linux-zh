power, then the guest may experience data corruption.

For such guests, you should consider using **cache=writethrough**. This ans that the host page cache will be used to read and write data, but write notification will be sent to the guest only after QEMU has made sure to flush each write to the disk. Be aware that this has a major impact on performance.

The host page cache can be avoided entirely with **cache=none**. This will attempt to do disk I/O directly to the guest’s morory. QEMU may still perform an internal copy of the data. Note that this is considered a writeback mode and the guest os st handle the disk write cache correctly in order to avoid data corruption on host crashes.

The host page cache can be avoided while only sending write notifications to the guest when the data has been flushed to the disk using **cache=directsync**.

In case you don’t care about data integrity over host failures, use **cache=unsafe**. This option tells CQEMU that it never needs to write any data to the disk but can instead keep things in cache. If anything goes wrong, like your host losing power, the disk storage getting disconnected accidentally, etc. your image will most probably be rendered unusable. When using the **-snapshot** option, unsafe caching is always used.

Copy-on-read avoids accessing the sa backing file sectors repeatedly and is useful when the backing file is over a slow network. By default copy-on-read is off.

Instead of **-cdrom** you can use:

```
```text
qe-system-i386 -drive file=file,index=2,dia=cdrom
```
```

Instead of **-hda, -hdb, -hdc, -hdd**, you can use:

```
```text
qe-system-i386 -drive file=file,index=0,dia=disk qe-system-i386 -drive file=file,index=1,dia=disk qe-system-i386 -drive file=file,index=2,dia=disk qe-system-i386 -drive file=file,index=3,dia=disk
```
```

You can open an image using pre-opened file descriptors from an fd set:

```
```text
qe-system-i386 -add-fd fd=3,set=2,opaque="rdwr:/path/to/file" -add-fd fd=4,set=2,opaque="r donly:/path/to/file" -drive file=/dev/fdset/2,index=0,dia=disk
```
```

You can connect a CDROM to the slave of ide0:

```
```text
qe-system-i386 -drive file=file,if=ide,index=1,dia=cdrom
```
```

If you don’t specify the “file=” argument, you define an empty drive:

```
```text
qe-system-i386 -drive if=ide,index=1,dia=cdrom
```
```

You can connect a SCSI disk with unit ID 6 on the bus #0:

```
```text
qe-system-i386 -drive file=file,if=scsi,bus=0,unit=6
```
```

Instead of **-fda, -fdb**, you can use:

```
```text
qe-system-i386 -drive file=file,index=0,if=floppy qe-system-i386 -drive file=file,index=1,if=floppy
```
```

By default, *interface* is “ide” and *index* is automatically incremented: