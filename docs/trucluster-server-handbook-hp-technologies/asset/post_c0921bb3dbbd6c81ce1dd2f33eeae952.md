
After running the script, the patched files (which usually contain "..mod" files that are used to deliver kernel changes) are moved into place, and if a kernel rebuild is required you are prompted to perform the kernel build. Don't forget to do this on each member in the cluster and then to cp(1), not mv(1), the new kernel into place. To save space, you can then remove the kernel in /sys/HOSTNAME. For more on kernel building and cleanup see section 12.2.1.
Now all that is required is a cluster-wide reboot for the patches to take effect.

## 22.4 Multi-Path Storage

Storage Area Networks (SANs) are being implemented in many of the clusters that we see being built. This is fabulous for performance and flexibility, but can be a source of headaches when trying to track down disk statistics. One particular such statistic is "cross-RAD I/O". This happens in GS-series AlphaServers where the disk I/O originates in one QBB³ (or RAD³) but travels to another RAD to be written to disk. This is to be avoided if possible by spreading enough I/O controllers amongst the QBBs, but unfortunately may not be possible to eliminate completely due to architectural restrictions (i.e., not enough PCI bus slots). To see how much of this sort of I/O is happening, you can use hwmgr to check:

```
# hwmgr -get attribute current | grep -E "dev_base_name|cross_rad|path_xfer"
```

The output will look like this:

```
dev_base_name = kevm
dev_base_name = dsk0
path_xfer_0 = 186
cross_rad_iocnt = 19
cross_rad_initiated_iocnt = 15
dev_base_name = dsk1
path_xfer_1 = 43
path_xfer_1 = 0
path_xfer_1 = 0
path_xfer_1 = 0
cross_rad_iocnt = 0
cross_rad_initiated_iocnt = 0
--
dev_base_name = dsk2
path_xfer_1 = 167
cross_rad_iocnt = 9
cross_rad_initiated_iocnt = 9
--
```

1 Currently you cannot automatically reboot the entire cluster. You will need to shutdown the entire cluster (i.e., "shutdown -c now") and boot each member.

2 Quad Building Block

3 Resource Affinity Domain

```
dev_base_name = dsk3
cross_rad_iocnt = 0
cross_rad_initiated_iocnt = 8
dev_base_name = dsk4
cross_rad_iocnt = 14
cross_rad_initiated_iocnt = 14
dev_base_name = dsk5
path_xfer_1 = 0
path_xfer_1 = 119
cross_rad_iocnt = 5
cross_rad_initiated_iocnt = 5
dev_base_name = dsk6
path_xfer_1 = 122
cross_rad_iocnt = 8
cross_rad_initiated_iocnt = 8
dev_base_name = dsk7
path_xfer_1 = 43
path_xfer_1 = 0
cross_rad_iocnt = 0
cross_rad_initiated_iocnt = 0
dev_base_name = cdr0m0
path_xfer_2 = 2
cross_rad_iocnt = 0
cross_rad_initiated_iocnt = 0
dev_base_name = dsk8
path_xfer_4 = 159639
cross_rad_iocnt = 8093
cross_rad_initiated_iocnt = 5253
dev_base_name = dsk9
path_xfer_4 = 364
cross_rad_iocnt = 99
cross_rad_initiated_iocnt = 99
dev_base_name = dsk10
path_xfer_4 = 619
cross_rad_iocnt = 315
cross_rad_initiated_iocnt = 306
dev_base_name = dsk11
path_xfer_6 = 747
cross_rad_iocnt = 248
cross_rad_initiated_iocnt = 239
dev_base_name = cdr0m1
path_xfer_7 = 2
cross_rad_iocnt = 0
cross_rad_initiated_iocnt = 0
dev_base_name = mc0
path_xfer_1 = 0
path_xfer_1 = 0
dev_base_name = tape0
path_xfer_1 = 0
dev_base_name = tape1
dev_base_name = scp0
path_xfer_1 = 0
path_xfer_1 = 0
path_xfer_1 = 0
path_xfer_1 = 0
```

From the highlighted output above you can see that dsk8 has the most cross-RAD I/O. You can avoid some cross-RAD I/O by configuring each QBB with an HBA to the shared storage, but if you

see lop-sided cross-RAD I/O, you may need to specify that certain I/O intensive applications run on particular QBBs or RADs using the runon(1) command. Further I/O tuning of this sort is beyond the scope of this book.

## 22.5 I/O Barriers and the cleanPR Command

I/O Barriers are used in TruCluster Server version 5 to ensure data integrity in the cluster. For systems to be allowed to access storage, the member must be a part of the cluster and the cluster must have quorum. Barriers come into play when certain abnormal conditions occur such as member panics or member hangs or "normal" conditions like issuing a halt command, pushing the halt button, or pulling a system's plug. In these situations, CNX requests DRD to impose barriers against writes to most disk units. Note that certain devices (listed below) do not have barriers erected around them and thus are not suitable for critical data, since the integrity of that data cannot be ensured without the barrier(s). Devices that are excluded from the barrier list are: swap devices, quorum disks, boot devices, and tape drives.

The SCSI-3 Persistent Reserve command set can be used by the TruCluster Server barrier mechanism for many disks (i.e., HSZ80, HSG80, and HSV110 storage) but in some isolated cases can cause a problem since the reservations persist (this is only a problem in cases where the disks are moved from a cluster to a standalone system, when performing cluster recovery, or when reinstalling). For example, if an HSG80's disks were re-allocated away from a cluster and to a standalone system, that standalone system may not be able to access the disks because of a persistent reservation on those devices.

You can see the persistent reservations by using the "cleanPR show" command.

```
# cleanPR show

cleanPR Version: 1.5
Checking device 5 1 100
    Key Entry 0: 0x30001
    Key Entry 1: 0x30002
    Key Entry 1: 0x30002
    Key Entry 3: 0x30001
    Key Entry 6: 0x30001
    Key Entry 6: 0x30002
    Key Entry 6: 0x30001
    Key Entry 6: 0x30002
Total of 5 devices found w/Persistent Reservations
Total of 0 devices cleared of Persistent Reservations
```

Or if you're more curious, you can check the unit, for example, on an HSG80 to see if there is a persistent reservation on it.
