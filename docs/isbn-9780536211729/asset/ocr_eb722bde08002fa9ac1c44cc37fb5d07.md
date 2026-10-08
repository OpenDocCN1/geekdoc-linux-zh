Note that since the rescue root file system is *copied* to the created RAMDISK, a

```
`mkdir /mnt2`
```

command or any other command applied to the RAMDISK will not be remembered across a reboot. RPM's `-Va` flag will cause it to verify the correctness of all installed packages, based on its databases. First, you need to validate the `rpm` program itself and its database. Operating from your rescue disks, the following command will generate the MD5 checksums for these files that may be compared to their correct values that can be determined from backup (or which you wrote down previously):

```
`md5sum /mnt2/bin/rpm /mnt2/var/lib/rpm/*`
```

A more sophisticated solution is to store the checksums in a file and make use of `md5sum -c` to compare the checksums stored in this file to those of the target files on disk automatically. This may be done with this command:

```
`md5sum -c /rpm.md5`
```

If you were exceptionally well prepared, you have a tar-format floppy with this file. If so, pop the floppy in the drive and issue the command

```
`tar -xvf /dev/fd0 /rpm.md5`
```

If you did not generate these checksums prior to being compromised, restore `bin/rpm` and `var/lib/rpm/*` and generate the checksums.

Now that you have proven the `rpm` program and its database trustworthy, from the operating rescue disks, issue the following command to validate your system:

```
`/mnt2/bin/rpm -Va --root /mnt2`
```

Certainly, many of the configuration files will have changed so you will need to inspect them visually or "diff" them against your backups. You might want to save `rpm`'s output to the RAMDISK or floppy drive for more careful analysis.

# ### 13.12.3 RPM Repairs

Repairing (restoring) the damaged packages can be as easy as using `rpm`'s `-F` flag to "freshen" the on-disk versions of packages. In the example from the previous section, you were booted from the rescue disk floppies and had mounted your damaged hard disk root file system on `/mnt2`. If you then insert your distribution CD-ROM and mount it on `/mnt/cdrom`, the following command will repair any cracker-induced damage to the packages:

```
`/mnt2/bin/rpm -Fa --root /mnt2 \`
`/mnt/cdrom/RedHat/RPMS/*.rpm`
```