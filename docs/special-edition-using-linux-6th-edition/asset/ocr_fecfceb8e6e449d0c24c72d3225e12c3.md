```
Cache      : 64 KB
CHS (log)  : 827 cylinders, 32 heads, 63 sectors
CHS (phys) : 1654 cylinders, 16 heads, 63 sectors
```

Each installed hard drive will have a section similar to the one listed previously. As you can see, very detailed information about the hard drive is listed with sysinfo, including the hard drive make and model. If your newly installed hard drive is not detected, it is most likely a cabling or configuration issue. The key to detecting SCSI devices is to make sure that the SCSI controller is detected. After the SCSI controller is detected, all SCSI devices need to be found. If not, the problem is most likely one of incorrect termination, conflicting SCSI ID settings, or faulty cabling.

# # Partitioning the Hard Drive

Partitioning the hard drive is done with the fdisk utility, which is very similar to the utility used on other operating systems such as DOS. A new partition can be created on the newly added hard drive by running fdisk and supplying the name of the device to be partitioned. For example, if the newly added drive is /dev/hdb, it can be partitioned as follows:

```
# fdisk /dev/hdb
```

After fdisk starts, the following directions will show you how to create and delete partitions, and how to change the partition type. After a partition is created, it becomes known to Linux by a unique device name and partition number. In the preceding example, the first partition on the drive hdb is referenced as /dev/hdb1 in Linux.

> > **Note**
> >
> > The drive devices used in this chapter follow the old naming convention. As of this writing, it is impossible to say which device names will be used with OpenLinux and the new 2.4.x kernel. The new devfs filesystem, if used, allows for only new names, mixed old and new names, and other variations. Eventually, the new device file naming convention will be used, which puts devices below their own /dev/ide/host#/bus#/target#/lun# scheme, with a parallel scheme for /dev/scsi/.../lun# (substituting numbers for the #). This change is coming to allow for the new USB and IR devices that must be accommodated.

To partition the new drive, you must know what the correct device name is in Linux. The system boot messages, as well as sysinfo, display the new device name. The device naming scheme for IDE drives is listed in Table 9.1. The naming scheme for SCSI drives is listed in Table 9.2.

**TABLE 9.1 — IDE Device Names**

| Device Scheme | IDE Controller | Jumpering |
|---|---|---|
| /dev/hda | Primary | Master |
| /dev/hdb | Primary | Slave |
| /dev/hdc | Secondary | Master |
| /dev/hdd | Secondary | Slave |