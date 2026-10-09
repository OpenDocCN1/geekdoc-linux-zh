# SYSTEM ADMINISTRATION

# Display Mounted File Systems in a Tabular Format

```
$ mount | column -t
```

The output of the mount command is not formatted in an easy-to-read manner. To make each column line up, pipe the output of the mount command to "column -t". By default mount displays all mounted filesystems, even the pseudo-filesystems like /proc and /sys. To limit output to a filesystem type, use the -t option and provide a type.

```
$ mount -t ext4
/dev/mapper/sys-lv_root on / type ext4 (rw)
/dev/sda1 on /boot type ext4 (rw)
$ mount -t ext4 | column -t
/dev/mapper/sys-lv_root on / type ext4 (rw)
/dev/sda1 on /boot type ext4 (rw)
```