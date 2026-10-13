
```
# cryptsetup luksFormat /dev/sda1
WARNING!
========
This will overwrite data on /dev/sda1 irrevocably.
Are you sure? (Type uppercase yes): YES
Enter LUKS passphrase:
Verify passphrase:
```

The passphrases that you type in are not shown at the console. The command shown in Figure 6-12 displays header information from the encrypted device. Once again, in case matters. If you type in yes in lowercase, the command does not prompt for a passphrase, and the volume is not encrypted.

A couple of more steps are needed before the encrypted device is ready for formatting: it must be mapped. In other words, since the /dev/sda1 volume is now encrypted, it can't be read. However, you can create a map to a different device, which is essentially the decrypted version of the device.

First, you need a UUID for the device. The following cryptsetup command creates a UUID for the newly encrypted /dev/sda1 device:

```
# cryptsetup luksUUID /dev/sda1
```

### FIGURE 6-12
The header of a LUKS-encrypted volume

```
[root@server1 ~]# cryptsetup luksDump /dev/sda1
LUKS header information for /dev/sda1

Version:           1
Cipher name:       aes
Cipher mode:       cbc-essiv:sha256
Hash spec:         sha1
Payload offset:    4096
MK bits:           256
MK digest:         0d 3c 3e 24 2e 48 48 2e 14 14 14 ce de d7 b6 65 0c 65 6c de 4b eb 70 6b
MK salt:           22 a2 a3 35 5d 84 b1 f7 0e 5f f9 7d 75 ba ba c3
                    48 2d f0 45 fb 81 49 69 d1 8e 22 1c cf 8e e9 cf
MK iterations:     45625
UUID:              70d5f05e-b320-4c80-bc70-597f4e6b212d

Key Slot 0: ENABLED
    Iterations:             182774
    Salt:                   75 0e 1c f2 66 dd 0e 2b a6 a5 fb cb 4d a0 42 ad
                            f3 80 b3 16 07 19 34 d3 76 94 37 87 0c 4e 66 9f
    Key material offset:    8
    AF stripes:             4000
Key Slot 1: DISABLED
Key Slot 2: DISABLED
Key Slot 3: DISABLED
Key Slot 4: DISABLED
Key Slot 5: DISABLED
Key Slot 6: DISABLED
Key Slot 7: DISABLED
[root@server1 ~]#
```

Naturally, that command returns a 128-bit UUID number. Red Hat documentation recommends that you use that number as part of device file for the encrypted filesystem. You can copy that number to the local buffer by highlighting it in a console. In a GUI console, you should be able to right-click and select Copy in the pop-up menu that appears. In a text console, if the mouse is active, that UUID number should already be in the buffer.

Now type in the following command:

```
# cryptsetup luksOpen /dev/sda1 uuidnumber
```

Paste the UUID number in place of uuidnumber. If it's in the GUI console, right-click at the end of the command and click Paste in the pop-up menu that appears. If it's in the command line console, click the middle mouse button (or the left and right mouse buttons together). Alternatively, if mouse buttons are unavailable, you could run the following commands (Of course, the two commands can be combined.):

```
# cryptsetup luksUUID /dev/sda1 > sdaluuid
# cryptsetup luksOpen /dev/sda1 `cat sdaluuid`
```

> Exam Watch
> Unless required on an exam, there's no reason to use the UUID number of an encrypted device. For example, you could run the following alternative cryptographic encryption command: cryptsetup luksOpen /dev/sda1 test.

The mapped device should now appear in the /dev/mapper directory. You should now be able to format that device with a command like mkfs.ext4. The following command formats the device I created in my server1.example.com system:

```
# mkfs.ext4 /dev/mapper/test
```

You should now be able to apply the mount command on that /dev/mapper device file. Ideally, you should now set that up in the /etc/fstab file to make sure that encrypted filesystem is mounted the next time that system is booted.

If you're already jumping ahead to configuration of the encrypted filesystem in the /etc/fstab file, this UUID corresponds to the original partition and is not associated with the encrypted filesystem. To find the UUID associated with this particular encrypted filesystem, run the following command:

```
# dumpe2fs /dev/mapper/test | grep UUID
```

That UUID number can then be used to represent the encrypted volume in /etc/fstab. The following are two ways such a volume could be configured in that file:

```
/dev/mapper/test   /test   ext4   defaults   1 2
UUID=uuidnumber    /test   ext4   defaults   1 2
```

Alternatively, the aforementioned mkfs.ext4 command would change the associated UUID, as confirmed by the output to the blkid command. That UUID in the blkid command output can then be used to represent the noted volume in a similar fashion.

If successful, you'll be prompted for the passphrase for any LUKS-encrypted filesystems that may have been created. One common related error is the unloading of the dm_crypt module during the system reboot process.

## CERTIFICATION OBJECTIVE 6.06

## Filesystem Management

Before you can access the files in a directory, that directory must be mounted on a partition formatted to some readable filesystem. Linux normally automates this process using the /etc/fstab configuration file. When Linux goes through the boot process, directories specified in /etc/fstab are mounted on configured volumes, with the help of the mount command. Of course, you can run that command with any or all appropriate options. So that's an excellent place to start this section.

The remainder of this section focuses on options for /etc/fstab. While it starts with the default using the baseline configuration for the standard virtual machine, it includes options for how you can customize that file for local, remote, and removable filesystems.

## The /etc/fstab File

The standard configuration file for filesystems mounted during the boot process is /etc/fstab. To look it over safely, run the less /etc/fstab command. From the example shown in Figure 6-13, different filesystems are configured on each line.

The default use of UUIDs is new for RHEL 6, as RHEL 5 used the LABEL directive. As you'll see in the next section, UUIDs can represent a partition, a logical volume, or a RAID array. In all cases, that volume should be formatted to the filesystem noted on each line. That volume is mounted on the directory in the second column. The advantage of an UUID, relative to the LABEL directive, is that the UUID is automatically created when the volume is formatted with a command like mkfs.ext4.

> *Line wrapping in the /etc/fstab file is now allowed on current versions of Linux, including RHEL 6. It is necessary to accommodate the length of the UUID.*

But to some extent, UUIDs are beside the point. As shown in Figure 6-13, there are six fields associated with each filesystem, described from left to right in Table 6-8. You can verify how partitions are actually mounted in the /etc/mtab file, as shown in Figure 6-14. Note the differences, especially the use of the device file associated with the partition, LV, or RAID array.

### FIGURE 6-13
Sample /etc/fstab

```
# /etc/fstab
# Created by anaconda on Thu Nov 25 17:53:49 2010
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=f7fe7c21-52ab-46ab-b9df-4bd856046e1bf / ext4 defaults 1 1
UUID=1c9f5ca-aff1-4a0f-b706-2de715938bef /boot ext4 defaults 1 2
UUID=ffaf9516-4066-4aed-a284-e966b936f3bf /home ext4 defaults 1 2
UUID=9f2f1fab-0a89-4f18-4a4f-c9a5bcb9cdbc swap swap defaults 0 0
tmpfs /dev/shm tmpfs defaults 0 0
devpts /dev/pts devpts gid=5,mode=620 0 0
sysfs /sys sysfs defaults 0 0
proc /proc proc defaults 0 0
~
```

### FIGURE 6-14
Sample /etc/mtab

```
[root@server1 ~]# mount
/dev/vda2 on / type ext4 (rw)
/dev/vda1 on /boot type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw,rootcontext="system_u:object_r:tmpfs_t:s0")
/dev/vda1 on /boot type ext4 (rw)
/dev/vda3 on /home type ext4 (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
/tmp on /tmp type none (rw,bind)
/var/tmp on /var/tmp type none (rw,bind)
/home on /home type none (rw,bind)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
[root@server1 ~]#
```

When adding a new partition, you could just add the device file associated with the partition, LV, or LUKS volume to the first column. The last four lines include virtual filesystems, and are discussed later in this chapter.

### TABLE 6-8
Description of /etc/fstab by Column, Left to Right

| Field Name | Description |
|---|---|
| Device | Lists the device to be mounted; you may substitute the UUID or LABEL. |
| Mount Point | Notes the directory where the filesystem will be mounted. |
| Filesystem Format | Describes the filesystem type. Valid filesystem types include ext, ext2, ext3, ext4, msdos, vfat, devpts, proc, tmpfs, udf, iso9660, nfs, smb, and swap. |
| Mount Options | Covered in the following section. |
| Dump Value | Either 0 or 1. A value of 1 means that data is automatically saved to disk by the dump command when you exit Linux. |
| Filesystem Check Order | Determines the order that filesystems are checked by the fsck command during the boot process. The root directory (/) filesystem should be set to 1, and other local filesystems should be set to 2. Removable filesystems such as those associated with CD/DVD drives should be set to 0, which means that they are not checked during the Linux boot process. |
