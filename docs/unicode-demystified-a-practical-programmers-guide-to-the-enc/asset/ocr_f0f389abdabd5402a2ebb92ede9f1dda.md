# df

Displays disk space usage

df [options] (filesystem-list)

The df (disk free) utility reports on total and free space on each mounted device. By default, the report is in terms of 1-kilobyte blocks.

Arguments When you call df without an argument, it reports on the free space on each of the currently mounted devices.
The filesystem-list is an optional list of one or more pathnames that specify the filesystems you want to report on. The df utility permits you to refer to a mounted filesystem by its device pathname or by the pathname of the directory it is mounted on.

# Options

+   --type=fstype -t f Reports information only about the filesystems of type ftype, such as DOS or NFS
--inodes -i Reports the number of inodes that are used and free instead of reporting on blocks.
--human-readable -h Displays sizes in K (kilobyte), M (megabyte), and G (gigabyte) blocks.
--megabytes -m Displays sizes in I-megabyte blocks.
--local l Displays local filesystems only.

Following, df displays information about all the mounted filesystems on a machine:

# Examples

```
$ df
Filesystem k-blocks Used Available Use% Mounted on
/dev/hda2 151720 53264 137854 4% /
/dev/hda1 15522 4846 9875 33% /boot
/dev/hda8 101928 110268 85026 11% /free
/dev/hda9 101928 30624 929900 3% /free2
/dev/hda10 1136540 78992 994120 7% /free3
/dev/hda5 4032092 1988080 183918 52% /home
/dev/hda7 1011928 60 960464 0% /tmp
/dev/hda6 2522048 824084 1569848 34% /usr
zach:/c 2096160 1811392 284768 86% /zach_c
zach:/d 2096450 1935097 161633 92% /zach_d
```