for different situations. The location of an operating system is specified using an ARC (Advanced RISC Computing) path, which is discussed below.

# Understanding the ARC Path

ARC, or Advanced RISC Computing, paths are used to tell NTLDR where to find an installed operating system. In the simplest of terms, the ARC path provides a roadmap for NTLDR to follow, which should lead to a valid installation of Windows 2000. A simple ARC path is shown below:

```
multi(0)disk(0)rdisk(0)partition(1)\WINNT
```

The ARC path from above is described in detail in Table 3.4.
The most important piece of information in the ARC path is the use of multi(x) or scsi(x). When using the multi(x) option, the rdisk(z) parameter specifies which disk is being accessed. When using the scsi(x)

| Table 3.4 ARC Path Components |  |
|---|---| 
| Switch | Description | 
| multi(x) or scsi(x) | Specifies the adapter or disk controller to which the boot disk is connected. The scsi option is used when a SCSI controller without a BIOS is installed. The multi option is used for all non-SCSI controllers and SCSI controllers with a BIOS installed. The value x represents the load order for the controller. As each controller is initialized, it is assigned a number beginning with 0. You must specify the correct controller or the system will fail to boot. | 
| disk(y) | This specifies the SCSI ID when the scsi option is used. The value y is always 0 if the multi option is used. | 
| rdisk(z) | This identifies the disk(s) connected to non-SCSI disk controllers. | 
| partition(a) | This specifies which partition is to be searched. The value a starts with 1 and specifies which disk partition is to be booted from. Disk partitions are numbered in order, beginning with primary partitions and then logical drives in an extended partition. | 
| \WINNT | Specifies the subdirectory in the partition that contains the operating system. |