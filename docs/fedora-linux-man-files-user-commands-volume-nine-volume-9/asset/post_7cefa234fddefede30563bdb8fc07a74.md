
qe-system-1386 -soundhw sb16,adlib disk.img
qe-system-1386 -soundhw es1370 disk.img
qe-system-1386 -soundhw ac97 disk.img
qe-system-1386 -soundhw hda disk.img
qe-system-1386 -soundhw all disk.img
qe-system-1386 -soundhw help

Note that Linux’s ac97_audio OSS kernel (for AC97) module might require manually specifying clocking.

    modprobe ac97_audio clocking=48000

- **-balloon none** Disable balloon device. **-balloon virtio[,addr=addr]** Enable virtio balloon device (default), optionally with PCI address addr.

- **-device driver[,prop=[value[,...]]]** Add device driver. prop=value sets driver properties. Valid properties depend on the driver. To get help on possible drivers and properties, use -device help and “-device driver,help”. **-name na** Sets the name of the guest. This name will be displayed in the SDL window caption. The name will also be used for the VNC server. Also optionally set the top visible process name in Linux. Naming of individual threads can also be enabled on Linux to aid debugging. **-uuid uuid** Set system UUID.

Block device options:

- **-fda file**
- **-fdb file**
    Use file as floppy disk 0/1 image.
- **-hda file**
- **-hdb file**
- **-hdc file**
- **-hdd file**
    Use file as hard disk 0, 1, 2 or 3 image.
- **-cdrom file**
    Use file as CD-ROM image (you cannot use **-hdc** and **-cdrom** at the same time). You can use the host CD-ROM by using /dev/cdrom as file name.

- **-drive option[,option[,option[,...]]]** Define a new drive. Valid options are:

    - **file=file**
        This option defines which disk image to use with this drive. If the file name contains comma, you should double it (for instance, “file=my,file”) to use file “my,file”.
        Special files such as iSCSI devices can be specified using protocol specific URLs. See the section for “Device URL Syntax” for more information.

    - **if=interface**
        This option defines on which type of interface the drive is connected. Available types are: ide, scsi, sd, mtd, floppy, pflash, virtio.

    - **bus=bus,unit=unit**
        These options define where the drive is connected by defining the bus number and the unit id.

    - **index=index**
        This option defines where the drive is connected by using an index in the list of available connectors of a given interface type.

    - **media=**_media_
        This option defines the type of the media: disk or cdrom.

    - **cyls=**_c_**,heads=**_h_**,secs=**_s_**,trans=**_t_
        These options have the same definition as they have in -hdachs.

    - **snapshot=**_snapshot_
        _snapshot_ is “on” or “off” and controls snapshot mode for the given drive (see -snapshot).

    - **cache=**_cache_
        _cache_ is “none”, “writeback”, “unsafe”, “directsync” or “writethrough” and controls how the host cache is used to access block data.

    - **aio=**_aio_
        _aio_ is “threads”, or “native” and selects between pthread based disk I/O and native Linux AIO.

    - **discard=**_discard_
        _discard_ is one of “ignore” (or “off”) or “unmap” (or “on”) and controls whether _discard_ (also known as _trim_ or _unmap_) requests are ignored or passed to the filesystem. Some machine types may not support discard requests.

    - **format=**_format_
        Specify which disk _format_ will be used rather than detecting the format. Can be used to specify format=raw to avoid interpreting an untrusted format header.

    - **serial=**_serial_
        This option specifies the serial number to assign to the device.

    - **addr=**_addr_
        Specify the controller's pci address (if=virtio only).

    - **werror=**_action_**,rerror=**_action_
        Specify which _action_ to take on write and read errors. Valid actions are: “ignore” (ignore the error and try to continue), “stop” (pause qemu), “report” (report the error to the guest), “enospc” (pause qemu only if the host disk is full; report the error to the guest otherwise). The default setting is **werror=enospc** and **rerror=report**.

    - **readonly**
        Open drive file as read-only. Guest write attempts will fail.

    - **copy-on-read=**_copy-on-read_
        _copy-on-read_ is “on” or “off” and enables whether to copy read backing file sectors into the image file.

    - **detect-zeroes=**_detect-zeroes_
        _detect-zeroes_ is “off”, “on” or “unmap” and enables the automatic conversion of plain zero writes by the os to driver specific optimized zero write commands. You may even choose “unmap” if _discard_ is set to “unmap” to allow a zero write to be converted into an UNMAP operation.

By default, the **cache=writeback** mode is used. It will report data writes as completed as soon as the data is present in the host page cache. This is safe as long as your guest os makes sure to correctly flush disk caches where needed. If your guest os does not handle volatile disk write caches correctly and your host crashes or loses power, then the guest may experience data corruption.

For such guests, you should consider using **cache=writethrough**. This means that the host page cache will be used to read and write data, but write notification will be sent to the guest only after QEMU has made sure to flush each write to the disk. Be aware that this has a major impact on performance.

The host page cache can be avoided entirely with **cache=none**. This will attempt to do disk I/O directly to the guest’s memory. QEMU may still perform an internal copy of the data. Note that this is considered a writeback mode and the guest os must handle the disk write cache correctly in order to avoid data corruption on host crashes.

The host page cache can be avoided while only sending write notifications to the guest when the data has been flushed to the disk using **cache=directsync**.

In case you don’t care about data integrity over host failures, use **cache=unsafe**. This option tells QEMU that it never needs to write any data to the disk but can instead keep things in cache. If anything goes wrong, like your host losing power, the disk storage getting disconnected accidentally, etc. your image will most probably be rendered unusable. When using the **-snapshot** option, unsafe caching is always used.

Copy-on-read avoids accessing the same backing file sectors repeatedly and is useful when the backing file is over a slow network. By default copy-on-read is off.

Instead of **-cdrom** you can use:

```text
qemu-system-i386 -drive file=file,index=2,media=cdrom
```

Instead of **-hda, -hdb, -hdc, -hdd**, you can use:

```text
qemu-system-i386 -drive file=file,index=0,media=disk
qemu-system-i386 -drive file=file,index=1,media=disk
qemu-system-i386 -drive file=file,index=2,media=disk
qemu-system-i386 -drive file=file,index=3,media=disk
```

You can open an image using pre-opened file descriptors from an fd set:

```text
qemu-system-i386 -add-fd fd=3,set=2,opaque="rdwr:/path/to/file"
qemu-system-i386 -add-fd fd=4,set=2,opaque="r-only:/path/to/file"
qemu-system-i386 -drive file=/dev/fdset/2,index=0,media=disk
```

You can connect a CDROM to the slave of ide0:

```text
qemu-system-i386 -drive file=file,if=ide,index=1,media=cdrom
```

If you don’t specify the “file=” argument, you define an empty drive:

```text
qemu-system-i386 -drive if=ide,index=1,media=cdrom
```

You can connect a SCSI disk with unit ID 6 on the bus #0:

```text
qemu-system-i386 -drive file=file,if=scsi,bus=0,unit=6
```

Instead of **-fda, -fdb**, you can use:

```text
qemu-system-i386 -drive file=file,index=0,if=floppy
qemu-system-i386 -drive file=file,index=1,if=floppy
```

By default, *interface* is “ide” and *index* is automatically incremented:

```text
qemu-system-i386 -drive file=a -drive file=b
```

is interpreted like:

```text
qemu-system-i386 -hda a -hdb b
```

- **-mtdblock file** Use file as on-board Flash memory image.
- **-sd file** Use file as SecureDigital card image.
- **-pflash file** Use file as a parallel flash image.
- **-snapshot** Write to temporary files instead of disk image files. In this case, the raw disk image you use is not written back. You can however force the write back by pressing C-a s.
- **-hdachs c,h,s,[t]** Force hard disk 0 physical geometry (1 <= c <= 16383, 1 <= h <= 16, 1 <= s <= 63) and optionally force the BIOS translation mode (t=none, lba or auto). Usually QEMU can guess all those parameters. This option is useful for old MS-DOS disk images.
- **-fsdev**

```text
fsdriver,id=id,path=path,[security_model=security_model]
[,writeout=writeout] [,readonly][,socket=socket|sock_fd=sock_fd]
```

Define a new file system device. Valid options are:

- *fsdriver*

This option specifies the fs driver backend to use. Currently “local”, “handle” and “proxy” file system drivers are supported.

- *id=id*

Specifies identifier for this device

- *path=path*

Specifies the export path for the file system device. Files under this path will be available to the 9p client on the guest.

- *security_model=security_model*

Specifies the security model to be used for this export path. Supported security models are “passthrough”, “mapped-xattr”, “mapped-file” and “none”. In “passthrough” security model, files are stored using the same credentials as they are created on the guest. This requires QEMU to run as root. In “mapped-xattr” security model, some of the file attributes like uid, gid, mode bits and link target are stored as file attributes. For “mapped-file” these attributes are stored in the hidden .virtfs_xattr directory. Directories exported by this security model cannot interact with other unix tools. “none” security model is same as passthrough except the server won’t report failures if it fails to set file attributes like ownership. Security model is mandatory only for local fsdriver. Other fsdrivers (like handle, proxy) don’t take security model as a parameter.

- *writeout=writeout*

This is an optional argument. The only supported value is “immediate”. This means that host page cache will be used to read and write data but write notification will be sent to the guest only when the data has been reported as written by the storage subsystem.

- *readonly*

Enables exporting 9p share as a readonly mount for guests. By default read-write access is given.

- *socket=socket*

Enables proxy filesystem driver to use passed socket file for communicating with virtfsd.
