```
brw-r---- 1 root disk 3, 6 Apr 27 1995 hda6
brw-r---- 1 root disk 3, 7 Apr 27 1995 hda7
brw-r---- 1 root disk 3, 8 Apr 27 1995 hda8
brw-r---- 1 root disk 3, 9 Apr 27 1995 hda9
```

# SLAVE HARD DRIVE ON THE PRIMARY CONTROLLER

If you add a second hard drive to your computer, normally it is mounted as the slave drive on the primary controller, as shown in the following list:

```
brw-r---- 1 root disk 3, 64 Apr 27 1995 hdb
brw-r---- 1 root disk 3, 65 Apr 27 1995 hdb1
brw-r---- 1 root disk 3, 74 Apr 27 1995 hdb10
brw-r---- 1 root disk 3, 75 Apr 27 1995 hdb11
brw-r---- 1 root disk 3, 76 Apr 27 1995 hdb12
brw-r---- 1 root disk 3, 77 Apr 27 1995 hdb13
brw-r---- 1 root disk 3, 78 Apr 27 1995 hdb14
brw-r---- 1 root disk 3, 79 Apr 27 1995 hdb15
brw-r---- 1 root disk 3, 80 Apr 27 1995 hdb16
brw-r---- 1 root disk 3, 66 Apr 27 1995 hdb2
brw-r---- 1 root disk 3, 67 Apr 27 1995 hdb3
brw-r---- 1 root disk 3, 68 Apr 27 1995 hdb4
brw-r---- 1 root disk 3, 69 Apr 27 1995 hdb5
brw-r---- 1 root disk 3, 70 Apr 27 1995 hdb6
brw-r---- 1 root disk 3, 71 Apr 27 1995 hdb7
brw-r---- 1 root disk 3, 72 Apr 27 1995 hdb8
brw-r---- 1 root disk 3, 73 Apr 27 1995 hdb9
```

![](bbox=[0.16, 0.65, 0.26, 0.74])

Although the BIOS will not try to boot from any drive other than the master drive on the primary controller, you can reconfigure the BIOS to boot from another hard drive if necessary.

# MASTER HARD DRIVE ON THE SECONDARY CONTROLLER

This following list illustrates the master hard drive on secondary controller. This is the usual location to which the CD-ROM drive is mounted (in which case the partitions listed earlier are not necessary). If you connect another hard drive to /dev/hdc (instead of, say, a CD-ROM or other drive for removable media), you can partition the drive as shown earlier.