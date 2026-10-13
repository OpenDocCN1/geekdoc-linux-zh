can be much simpler. For instance, the following command unmounts a CD-ROM drive that was mounted using the example given earlier:

```
umount /mnt/cdrom
```

> **Note**
> 
> If the unmounting procedure is to succeed, no one can be using the mount directory when you unmount a device or a mount directory. If anyone is accessing the mount directory, you get a busy device error, and the unmounting procedure fails. Be sure to back out of a mount directory before unmounting the device attached to it.

# AUTOMATING THE MOUNTING PROCESS

The mounting process can be automated by configuring the filesystem table file (/etc/fstab). You can do this by adding the drive device in question to the automount filesystem table contained in the /etc/fstab file.

When you start the system, Linux mounts certain devices automatically. The /etc/fstab file contains information about these devices that is necessary to have them mounted without interaction from the system administrator.

The /etc/fstab file offers two kinds of functionality. Entries in the fstab file can be configured to have specific filesystems mounted automatically each time the system boots. Furthermore, by defining an entry in the /etc/fstab file, you don't have to supply the entire mount command when mounting a filesystem manually. For example, if your CD-ROM drive has its own entry in /etc/fstab that contains all the information necessary for it to mount, the following command can be used to mount the drive:

```
mount /mnt/cdrom
```

Each filesystem is described on a separate line in the /etc/fstab file. Each entry contains all the information that you type at the command prompt, as well as a few other options that change the way the drive is mounted.

The entry in the /etc/fstab file for an ATAPI-IDE CD-ROM looks similar to the following:

```
/dev/hdc /mnt/cdrom iso9660 ro,noauto, 0 0
```

Each line entry has six space-delimited fields. The description of these fields is outlined in Table 9.6.

**TABLE 9.6 — FIELD DESCRIPTIONS OF THE /etc/fstab FILE**

| Field | Description |
|---|---|
| `/dev/hdc` | The actual device name or partition to be mounted. |
| `/mnt/cdrom` | The mount point. When mounted, data on this filesystem is accessible via this directory name. |