
Select the file system type for the /var file system.
1) UFS -- UNIX File System
2) AdvFS -- Advanced File System

Enter your choice: 2

Finally, we verify our disk partition selections for our Tru64 UNIX system disk’s file systems.

```
You have requested this file system layout:
* root file system on dsk0a, type AdvFS
* /usr file system on dsk0g, type AdvFS
* /var file system on dsk0h, type AdvFS
* first swapping area (swap1) will be on dsk0b
* no second swapping area (swap2)
```

```
Is this the correct file system layout (y/n) ? y
```

Table 5-1 contains the partition layout for the system disk that we just configured.

## Tru64 UNIX Operating System Disk Layout

| Mount Point | File System | Partition Size | Partition |
|---|---|---|---|
| root (/) | root_domain#root | 512 MB | dsk0a |
| /usr | usr_domain#usr | 4.0 GB | dsk0g |
| /var | var_domain#var | 2.0 GB | dsk0h |
| swap | swap | 4.5 GB | dsk0b |

**Table 5-1: Standalone O/S Disk Partition Layout**

It should be noted that while we were using an 18.2 GB hard disk drive for the system disk, we were not using the guidelines from HP for the layout of the system disk. HP recommends that for a system disk over 3 GB, the system’s root (/) should be 384 MB and the swap should be 384 MB (if not larger)[5]. It has been our experience that for the original system disk of a system that will be used as the basis for building a cluster, the system’s root (/) should be at least 512 MB and the swap should be two to three times the size of memory. As this system has 1.5 GB of memory, swap is created to be 4.5 GB in size. For this system disk, though, we won’t get too concerned about the swap size. It’s likely to be used only long enough to build the cluster, or if we need a standalone operating system disk to troubleshoot a cluster problem.

5. Table 6-7: Recommended Partition Table by Disk Capacity, Tru64 UNIX Installation Guide.

So should you follow our example or use what HP recommends? What HP has published in their documentation are guidelines based on input from the designers, developers, and customers of Tru64 UNIX and TruCluster Server. What we present is based mostly on experience. We believe that you should start with HP’s recommendations, deviating when necessary based on what you know about your system’s expected workload.

## 5.4.7 Confirm the Selections Before Starting the Installation

This next section will allow you to verify or modify any earlier selections made for the installation.

```
You have now answered all questions needed to install the operating system. Press CTRL/C to cancel the installation; or type 'history' to modify your earlier answers; or press RETURN to proceed with installation:
```

In our case, we were satisfied with all our selections so we continue with the installation.

## 5.4.8 Create the File Systems and Install the Software Subsets

There really isn’t much for us to do except monitor the creation of all the file systems and the loading of the software subsets that we had selected. So grab lunch or enjoy a long coffee break…

```
Continuing installation...
Restoring the existing disk label on device dsk0
Creating the root file system on device dsk0a
Creating the usr file system on device dsk0g
Creating the var file system on device dsk0h
Creating the swap1 file system on device dsk0b

The installation procedure will now load a total of 85 software subsets on your disk partitions. This total includes the following products:
* 85 Base Operating System subsets

This process will take from 45 to 120 minutes to complete depending on your distribution media and processor type.

LOADING THE BASE OPERATING SYSTEM SOFTWARE SUBSETS
```

## 5.4.10 Configure and Build the UNIX Kernel

Earlier, when we were prompted for kernel configuration options, we selected to do a customized kernel. In this section of the Installation, we are given the opportunity to identify exactly which options are needed for our system’s kernel.

If we had selected “All Options” or “Mandatory Only” for the Kernel configuration options, we would not be receiving this dialogue at all. We believe that by selecting only those options that we use, we should have a smaller and better performing kernel.

```
*** KERNEL CONFIGURATION AND BUILD PROCEDURE ***
*** KERNEL OPTION SELECTION ***

Selection   Kernel Option
---------------------------------------------
    1       SCSI Devices
    2       NTP V3 Kernel Phase Lock Loop (NTP_TIME)
    3       Kernel Breakpoint Debugger (KDBUG)
    4       Packetfilter driver (PACKETFILTER)
    5       IP-in-IP Tunneling (IPTUNNEL)
    6       IP Version 6 (IPv6)
    7       Point-to-Point Protocol (PPP)
    8       STREAMS packet module (PCKTM)
    9       Data link Bridge (DBRI V2.0 Service Class 1)
   10       X/Open Transport Interface (XTI), TIMOD, TIRDWR
   11       Digital Versatile Disk File System (DVDFS)
   12       ISO 9660 Compact Disc File System (CDfs)
   13       Audit Subsystem
   14       All of the above
   15       None of the above
   16       Help
   17       Display all options again

Enter your choices, choose an overriding action or
press <Return> to confirm previous selections.
```

```
Choices (for example, 1 2 4-6): 2 4 8 11 13
```

```
You selected the following kernel options:
        NTP V3 Kernel Phase Lock Loop (NTP_TIME)
        Packetfilter driver (PACKETFILTER)
        STREAMS packet module (PCKTM)
        Digital Versatile Disk File System (DVDFS)
        Audit Subsystem
```

```
Is that correct? (y/n) [y]: y
```
