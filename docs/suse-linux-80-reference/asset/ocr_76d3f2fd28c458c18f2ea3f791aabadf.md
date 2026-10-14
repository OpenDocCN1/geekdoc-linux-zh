# Uninstalling LILO

> **Caution**
> 
> Uninstalling a boot manager is tricky. Ensure *in advance* that you are able to boot Linux and other systems with their respective boot disks. You should have fdisk installed on every boot disk, to avoid being unable to access your hard disk at all.

To uninstall LILO, copy the former content of the boot sector over LILO. This requires a valid backup of that former content. See Section *Other LILO Configuration Options* on page 99, option backupr.

> **Caution**
> 
> A boot sector backup is no longer valid if the partition in question has a new file system (for DOS users: has been formatted). The partition table of an MBR backup becomes invalid if the hard disk in question has been repartitioned in the meantime. Obsolete “backups” are time bombs. It is best to delete them as soon as possible. Unpacking old and invalid backups into system sectors is a direct route to data loss.

It is very simple to regain a DOS, Windows 95/98, or OS/2 MBR. Just enter the MS-DOS command (available since 5.0)

```
C:\> FDISK /MBR
```

or, on OS/2,

```
C:\> FDISK /NEWMBR
```

These commands only write the first 446 bytes (the boot code) into the MBR and leave partitions untouched.
For other restorations, first make a backup of the LILO sector in question — just, to be on the safe side. Now check, at least twice, whether your old backup file is the correct one and if it is exactly 512 bytes in size. Finally, write it back, but do not confuse if= and of=:

+   - If LILO resides in partition yyyy (e.g., hda1, hda2):
+     ```
+     earth:  # dd if=/dev/yyyy of=New-File bs=512 count=1
+     earth:  # dd if=Backup-Date of=/dev/yyyy
+     ```
+   - If LILO resides in the MBR of zzz (e.g., hda, sda):
+     ```
+     earth:  # dd if=/dev/zzz of=New-File bs=512 count=1
+     earth:  # dd if=Backup-Date of=/dev/zzz bs=446 count=1
+     ```