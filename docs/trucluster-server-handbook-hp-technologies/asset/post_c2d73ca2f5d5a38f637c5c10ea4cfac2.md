
## Tru64 UNIX Cluster Hooks:
Device Naming & Hardware Management

In the last chapter, we showed how the directory hierarchy had been altered in Tru64 UNIX, starting with version 5.0, to ease the transition from a standalone environment to a clustered one. In this chapter, we will dig a little deeper into this modified hierarchy as we explore how device locations have been altered as well.

We will cover the following:
- Device Special File Names and Locations
- Worldwide Identifiers (WWID)
- Hardware Management Databases
- The Hardware Manager (hwmgr) Command
- The Device Special File (dsfmgr) Command

| Section |
|---|
| 7.1 |
| 7.2 |
| 7.3 |
| 7.4 |
| 7.5 |

## 7.1 Device Special File Names and Locations

In Tru64 UNIX prior to version 5.0, all devices were located in the /dev subdirectory. In version 5.0 and above, this has changed; to the casual observer, though, it will look the same. It bears mentioning up front that the device special file naming convention for storage devices has changed. Gone is the bus-target-lun (b-t-l) mnemonic for disks and cdrom devices; gone is the cryptic tape device naming convention. Table 7-1 shows the device special file naming changes.

Why did the b-t-l naming convention get replaced? First, to enable Tru64 UNIX to support multiple paths to a device, and second, to enable every member in a cluster to see the same device by the same device special file name regardless of its physical location. How is this accomplished? We will answer that question in the next section.

### Device Special File Naming

|  | Version 4 and below |  |  |  |  | Version 5.0 and above |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|---|
|  | directory (/dev) | base name | LUN* | instance | partition or density | directory (/devices) | base name | instance | partition or density |  |
| CDROM | . | rz [a-h] | n | [ac] |  | /disk | cdrom | n | [ac] | block |
|  | . | rrz [a-h] | n | [ac] |  | /rdisk | n | [ac] | character |
| Disk | . | rz [a-h] | n | [a-h] |  | /disk | dsk | n | [a-h] | block |
|  | . | rrz [a-h] | n | [a-h] |  | /rdisk | n | [a-h] | character |
| Tape | . | rmt [a-h] | n | [almh] |  | /tape | tape | n | d[0-7] | rewind |
|  | . | rrmt [a-h] | n | [almh] |  | /ntape | n | d[0-7] | no rewind |
| CCL | . | rz [a-h] | n | c |  | /cport | scp | n |  |  |
| Changer | . | mc [a-h] | n | [a-h] |  | /changer | mc | n |  |  |
| LSM | ./vol/dg | user-defined volume name |  |  |  | /vol/dg | user-defined volume name |  |  | block |
|  | ./rvol/dg |  |  |  |  | /rvol/dg |  |  |  | character |
* n = device number
* - if LUN 0, this field is optional

# Table 7-1: Device Special File Naming

Another fundamental change that has occurred is the location of the device special files. Storage devices have been relocated to the /devices directory tree. The /dev file is now a CDS link pointing to a member-specific /dev directory and contains member-specific devices (e.g., the console, keyboard, mouse, pseudo terminals, etc.). Figure 7-1 shows the device directory hierarchy.

Let’s explore the hierarchy. First, what are the device files in the root (/) directory?

```
# file /dev*
/dev:  symbolic link to cluster/members/{memb}/dev
/devices:  directory
```

Notice that /dev is now a CDS link, whereas /devices is actually a cluster-common directory. If we look more closely at what is in /devices we see that the storage device directories are located there. This is done because storage devices are shared in a cluster.

![](img/a0df85c2e542a8d6c913113908553aa4_167_0.png)

# Figure 7-1: Device Directory Hierarchy

```
# file /devices/*
/devices/changer: directory
/devices/cport: directory
/devices/disk: directory
/devices/dmapi: directory
/devices/ntape: directory
/devices/rdisk: directory
/devices/rvol: directory
/devices/tape: directory
/devices/vol: directory
```

Although the directory hierarchy has changed, it looks the same. That is to say we can still cd(1) to /dev, and all devices, including the storage device directories, are there. However, the storage device directories are actually symbolic links to the /devices directory.

```
# find /dev/ -type l -ls | awk '{ print $11,$12,$13 }'
/dev/none -> ../devices/none
/dev/cport -> ../../../../devices/cport
/dev/disk -> ../../../../devices/disk
/dev/rdisk -> ../../../../devices/rdisk
/dev/tape -> ../../../../devices/tape
/dev/ntape -> ../../../../devices/ntape
/dev/changer -> ../../../../devices/changer
/dev/dmapi -> ../../../../devices/dmapi
/dev/vol -> ../../../../devices/vol
/dev/rvol -> ../../../../devices/rvol
```

## 7.2 Worldwide Identifiers (WWID)

In the previous section, we discussed the device special file naming change and why it changed from the b-t-l naming convention of previous Tru64 UNIX releases. We said that we would tell you how unique cluster-wide naming was accomplished in the next section, and here we are. Unique device special file names are accomplished by using a SCSI worldwide identifier (WWID) to identify storage devices on a standalone system or in a cluster.

Every device is assigned a name the first time it is detected by the operating system. The name starts with a base name (dsk, cdrom, tape, etc.) followed by a number. The numbering begins with zero. Once the device has been recognized, it can be relocated to another bus or another target, etc., and the name remains the same. A WWID is a unique identifier, not unlike a serial number, that most SCSI devices should have. There are exceptions, however, and these include how Tru64 UNIX identifies units from HSZ RAID controllers and older SCSI devices.
