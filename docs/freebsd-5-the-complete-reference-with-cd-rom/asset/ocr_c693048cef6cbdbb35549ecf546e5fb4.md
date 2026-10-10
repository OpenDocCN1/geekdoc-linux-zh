For instance, the following sequence changes the partition type code for the first partition in the preceding output:

```
The data for partition 1 is:
sysid 11, DOS or Windows 95 with 32 bit FAT
start 63, size 4192902 (2047 Meg), flag 0
beg: cyl 0/ head 1/ sector 1;
end: cyl 260/ head 254/ sector 63
Do you want to change it? [n] y
Supply a decimal value for "sysid (165=FreeBSD)" [11] 165
```

> **Note**  *Although typing* `fdisk -s /dev/ad0` *produces partition type codes in hexadecimal (base 16), the prompts when you type* `fdisk -u /dev/ad0` *show and expect entry of the partition type codes in decimal (base 10). Table 4-1 shows partition type codes in both formats.*

Some OSs, such as Linux, don’t use partition type codes, except possibly during installation. For these Linux, you must configure them to ignore the FreeBSD slice. Most Linux distributions do this by default, so this shouldn’t be a problem with Linux. If you want to access your FreeBSD partitions from Linux, though, you have to activate Linux’s support for FreeBSD slices and filesystems, as described in the upcoming section, “Accessing FreeBSD Filesystems from Other OSs.” Accessing FreeBSD partitions from another BSD OS, such as OpenBSD or NetBSD, is normally fairly straightforward. Typically, each BSD OS has its own slice, but you need only specify the correct slice and partition to mount a foreign BSD filesystem.

# ## Accessing Foreign Partitions from FreeBSD

Under FreeBSD, every partition has a unique identifier in the /dev hierarchy. Disk files in this hierarchy have names built up of several parts:

+   * **Device type** Hard disks have two-letter type codes for the device type. IDE disks use a code of `ad`, and SCSI disks use a code of `da`. USB drives are treated like SCSI drives, so use the `da` code for them.
+   * **Device number** Each physical disk has a number. The first disk of a type is normally numbered 0, the second is 1, and so on. For IDE disks, the device number is tied to the disk controller and position on the chain: the primary controller’s master disk is 0, the primary controller’s slave disk is 1, the secondary controller’s master disk is 2, and so on. SCSI disks are numbered sequentially starting with 0, even if the first disk’s SCSI ID is higher than this.
+   * **Slice number** The slice number is indicated by the letter s and a number from 1 to 4. These numbers usually start at 1, but some tools create slices in a peculiar