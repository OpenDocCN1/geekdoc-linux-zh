`LIL-` The descriptor table in the map file is corrupt. This can either be caused by a geometry mismatch or by moving `/boot/boot.b` without reinstalling LILO.

`LILO` All parts of LILO have been successfully loaded.

# Resolving Causes of Error

The most common causes of geometry errors are neither physical defects nor invalid partition tables, but rather routine installation errors. Geometry errors result in particular when the 1024-cylinder limit is not taken into consideration (see Section *The 1024-Cylinder Limit* on the next page).

In most cases, problems can be remedied by taking the following measures:

+   1. Install the LILO data below the 1024-cylinder limit (if this already has not taken place). This applies to the Linux kernel required, the directory contents of `/boot`, and to the boot sector to adopt the LILO boot code.

+   2. As root, reinstall LILO using the `lilo` command. `lilo` will issue an informative log if you increase the verbosity and create log files by entering:

```
earth: # lilo -v -v -v >/boot/lilo.log 2>/boot/lilo.logerr
```

If the boot configuration is correct, `/boot/lilo.logerr` should be empty. You should be able to follow exactly how LILO saves the locations of its files and which BIOS device numbers LILO uses for related hard disks in `/boot/lilo.log`.

+   3. Check the consistency of the hard disk geometry. This actually pertains to up to four aspects:
+   
+      (a) **Geometry used by LILO** — See the log file mentioned above, which is influenced by the disk setting in `lilo.conf`. See the information on page 101.
+   
+      (b) **Geometry recognized by the Linux kernel** — See the boot messages in `/var/log/boot.msg` or the output of the `dmesg` command. This is influenced by kernel parameters (to a certain degree). See Section *(E)IDE controllers and ATAPI devices* on page 248.
+   
+      (c) **Geometry on which the partition table is based.** See the output of `fdisk -l`. It is influenced by `fdisk` expert commands and poses an extreme risk to your data. It is highly recommended to fully back up your data first.