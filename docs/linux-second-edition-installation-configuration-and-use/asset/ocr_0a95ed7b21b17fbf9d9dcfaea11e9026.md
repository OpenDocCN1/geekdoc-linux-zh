# CONFIGURATION AND ADMINISTRATION

+   The kernel components Multiple devices and RAID-0 must be available (either directly integrated in the kernel or as modules). This is the case with all current distributions. If not, the kernel must be recompiled. The corresponding options can be found in the Block devices group.)

+   Finally, you need the commands mmadd, mdcreate, mdrun, and mdstop. Usually the corresponding package will still need to be installed. (In SuSE, the package is mdutils (series april), in RedHat, it is raidtools).

With the current Linux distributions, different versions of the RAID commands are swapped. Up to version 0.4 (used, for example, by SuSE 6.0), the commands are mdx and the configuration file is /etc/mdtab. From version 0.5 onward (with RedHat 5.2 and higher), the commands are radix; the configuration file has a new syntax and is located in /etc/raidtab. This section takes both cases into account; you simply need to execute the command that matches your version.

In some older distributions, these are not automatically created. This can be remedied by means of the following commands:

```
root knod /dev/md0 b 9 0
root knod /dev/md1 b 9 1
root knod /dev/md2 b 9 2
root knod /dev/md3 b 9 3
root clown root.disk /dev/md*
root chmod 660 /dev/md6
```

The first step towards the RAID-0 partition is to combine two (or more) unused partitions (in the following example /dev/sda10 and /dev/hdc10) into one multi-disk device (/dev/md0):

```
root mdadd /dev/md0 /dev/sda10 /dev/hdc10 # up to version 0.4
root raidrun /dev/md0 /dev/sda10 /dev/hdc10 # since version 0.5
```

The partitions specified in mdadd should be of the same size. If this is not the case, stripping only works for part of the total capacity of the partitions, that is, theoretically possible gain in speed can be achieved partially.

Subsequently, it must be stated that this new device is to be addressed as a RAID-0 partition (-p0). As page size, the default value of 4 Kbytes is used (that is, data across the hard disks in 4-Kbyte blocks). If required, a different page size can be specified by means of -cnk.

```
root mdrun -p0 /dev/md0 # up to version 0.4
root raidrun -p0 /dev/md0 # since version 0.5
```

As the next step, a file system must be created on the new virtual partition /dev/md0. (Caution: all data stored in the partitions specified in mdadd is lost!)

```
root mk2efs /dev/md0
```

Now, the mount command can be used to mount the new partition into the Linux file system. The partition is accessed via the /striped device – obviously, you may use another name instead.