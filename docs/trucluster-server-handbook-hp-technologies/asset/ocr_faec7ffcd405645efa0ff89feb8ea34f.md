```
Sep 14 18:07:30 kyle vmunix: This cluster member is missing the TCS-UA license PAK
```

# A.1.10  CFS Boot Error When Mounting `cluster_root`

The first booting member gets CFS errors when trying to mount `cluster_root`. You may see an error message similar to:

```
WARNING: Magic number on ADVFS portion of CNX partition on quorum disk is not valid
```

This could be a problem with the quorum disk itself or a path to the quorum disk. See the Cluster Administration manual (Chapter 11).

# A.1.11  CFS Boot Error When Mounting Boot Partition

When booting a member into an existing cluster, you may see an error:

```
cfs_mountroot: CFS server already exists for node boot partition
```

This usually is an indication that the `boot_partition` is currently mounted by another cluster member. Unmount the `boot_partition`.

# A.1.12  Can’t unmount a File System that No Longer is Served by a Cluster Member

Use “`cfsmsg -e`” to see if the file system is being serviced. If it is “Not Served,” you can use the “`cfsmsg -u`” command to forcibly unmount the domain. See Chapter 11 of the *TruCluster Server Cluster Administration* manual for details.

# A.1.13  AutoFS File Systems Become Busy or Unresponsive

Forcibly unmount the AutoFS intercept points and autofs file systems served by the member. See Chapter 7 of the *TruCluster Server Cluster Administration* manual for details.