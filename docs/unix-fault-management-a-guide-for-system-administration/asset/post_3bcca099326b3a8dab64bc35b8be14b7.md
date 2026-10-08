
## Figure 4-13 Using SyMON dynamic reconfiguration to replace a failed memory board.

![](img/eae88b61ada165139a1d9b546a34140b_115_0.png)

offline. In contrast, slot 0 is associated with a permanent memory bank and can’t be disconnected while the system is running.

## Setting Up Monitoring and Reconfiguration

From the Enterprise SyMON console, Bill loads the Config-Reader and Dynamic Reconfiguration modules to ensure that he will be notified of hardware faults, so that he can handle the faults without having to take the system down. The Config-Reader module is located under Hardware and the Dynamic Reconfiguration module is located under local applications (shown in Figure 4-7, earlier in this chapter).

## Memory Board Failure Occurs

When a critical memory fault occurs, the icon for the system on the SyMON console indicates the alarm. Bill looks at the Alarm window to see more details about the event. He notices that a memory board has failed. Using the Logical View, like the one shown in Figure 4-14, he locates the failed memory board. Using the Physical View, like the one shown earlier in Figure 4-5, he locates the exact location of the physical board in the system.

## Fixing the Failure and Restoring Service

Bill accesses the Dynamic Reconfiguration screen from the SyMON console. First, he selects the failed memory slot and clicks the Disconnect button to unconfigure and disconnect the board. Next, he replaces the failed board and then connects the board by clicking the Connect button; he leaves it temporarily unconfigured, however, while he performs a memory test using the Test Memory button, to ensure that the new board is functional. Finally, Bill clicks the Configure button to make these memory resources available to the system.

## Figure 4-14 Using the SyMON Logical View to locate a failed memory board.

![](img/eae88b61ada165139a1d9b546a34140b_116_0.png)

Bill was able to handle a failed memory board in this environment with very little impact to the system. Sun’s dynamic reconfiguration capabilities, available from SyMON, provide a powerful feature that allows failed memory, CPU, and I/O resources to be fixed without having to bring down the system.

# Chapter 5
## Monitoring the Disks

Disk technologies provide some level of protection against failure. To reduce or eliminate system downtime due to disk failures, technologies such as Redundant Array of Inexpensive Disks (RAID) or mirroring must be used to provide data redundancy. RAID technology uses parity data to ensure that recovery is possible in the event of a disk failure. Mirroring allows multiple copies of data to be maintained. Three-way mirroring, in particular, provides added data protection during backups, because mirroring continues on the disks that are not being backed up.

With data redundancy, data is protected if an initial failure occurs, but the initial failure may result in a loss of redundancy, or a single point of failure (SPOF). Thus, a subsequent failure may result in loss of data. So, even though these technologies protect against single failures, notification of such failures is critical to reduce the risk of downtime. Fixing a failure and restoring data redundancy before the next failure occurs is key to maintaining availability. Data redundancy and fault monitoring do not replace the need for a regular backup strategy.

Although RAID and mirroring may protect against a single hardware failure, many other potential events exist that may affect the availability of data on the disk and increase the risk of downtime. The key to eliminating the risk of failure and downtime is to monitor your critical disk resources. You must know which resources to monitor and what tools are available to do that monitoring. This chapter addresses monitoring of disk resources, from the hardware device level up to filesystem resources. It does not cover backup, recovery, or tape storage devices.

## Identifying Important Disk Monitoring Categories

As already mentioned, redundancy is the best way to protect against initial failures. The key to high availability is to always maintain redundancy so that a disk fault does not adversely affect system and data availability. Sometimes, however, this isn't enough. If the resources aren't performing normally, availability can be affected by degraded performance, too.

Regardless of whether you have your disks configured for high availability, monitoring can help protect against failures. Although redundancy helps to provide protection from an initial hardware failure, monitoring needs to be done to protect not only against a second failure, but also against other failures that may affect availability.

The events and measures that you can use to maintain availability are broken down into several categories of system monitoring:

- Disk configuration: Includes monitoring for the addition or removal of disk resources, as well as ensuring that the proper software and firmware versions are installed. Tracking configuration changes can help when you are troubleshooting problems later. Ensuring that a device is using the correct version of firmware can also eliminate problems.
- Fault management: Includes monitoring any kind of errors or events that may occur on the hardware, the physical disk devices. This category covers device errors, such as media errors, read errors, seek-time errors, and bad blocks, as well as component failures, such as FRU failures, controller failures, RAID failures, fan failures, and more.
- Resource management: Includes monitoring the resources that provide storage space on disks. Filesystem space, mount points, logical volumes, mirrored copies, and physical volume links are all important disk resources to monitor. At the filesystem level, you must ensure that sufficient filesystem space is available for applications to run successfully. All filesystems must be mounted and available to their users. Filesystems are often configured using logical volumes. When data is mirrored, it is the logical volumes that are mirrored. Monitoring data mirrors can be critical to maintaining redundancy and increasing availability. Physical volumes and the links to those volumes are considered disk resources.
- Performance management: Includes monitoring disk performance metrics, such as disk read and write throughput rates. Swap rates are also important, because they can be used to identify resource contention, which can affect availability. Disk performance resources can be monitored to ensure that I/O traffic is balanced across the available disk resources.

The following sections list various tools that you can use to monitor the disk resources listed in the preceding categories. These tools include basic commands, system instrumentation available through standard interfaces, event monitors, diagnostic tools, and performance monitors.

## Using Standard Commands and Tools

Many UNIX commands exist to check configuration, status, and resource information. These tools generally report on only a snapshot in time. You can periodically track configuration changes or test the status of disk devices or resources by writing and using custom scripts that include these (and other) commands.

### bdf and df

The bdf and df commands can be used not only to see the mounted filesystem configuration, but also to report filesystem usage and capacity information. You can use this command to do the following:

- Monitor filesystem space, to avoid filesystem capacity limits
- Check that the necessary filesystems are mounted
- View the relationship between the filesystem mount points and associated logical volumes

Listing 5-1 shows the output of bdf.

### diskinfo

The diskinfo command can be used to get device information for CS/80, Subset/80, and Hewlett-Packard Small Computer Standard Interface (SCSI) disk devices. Using this command, an operator can check disk access. In this way, the disk is pinged to see whether it is okay. You can use diskinfo to get device status and configuration information. Listing 5-2 shows some sample output.

### fsck

The fsck command performs filesystem consistency checks and interactive repair. If it finds inconsistencies, it provides a mechanism to repair the inconsistencies in the filesystem. You should run this tool if you suspect a corrupt filesystem, or just run it periodically for preventative maintenance.

Using fsck with the -m option checks whether the filesystems have any errors that need to be corrected. If they do not, it reports that the filesystems are already mounted, as shown in Listing 5-3.

Using fsck with the -n option generates a more detailed report. Blocks, pathnames, and reference counts are checked. Listing 5-4 shows a portion of an fsck report containing information on multiple filesystems. Note that it shows an error with /dev/vg00/rvo15.

Listing 5-1 Output from the bdf command for monitoring filesystem space.

```
Filesystem             kbytes     used   avail %used Mounted on
/dev/vg00/rvo13     102400   18723   78457  19% / 
/dev/vg00/rvo11     47829    6438   36608  15% /stand
/dev/vg00/rvo18    155648   51011   98168  34% /var
/dev/vg00/rvo17    307200  228550   73747  76% /usr
/dev/vg00/rvo16     49152   1214   45007   3% /tmp
/dev/vg00/rvo15    102400   84310   16981  83% /opt
/dev/vg00/rvo14    921600  446758  445205  50% /home
```

Listing 5-2 Output from the diskinfo command.

```
# diskinfo /dev/rdsk/c0t5d0
SCSI describe of /dev/rdsk/c0t5d0: 
        vendor:  SEAGATE 
        product id: ST34572WC 
        type: direct access 
        size:  4194157 Kbytes 
        bytes per sector: 512
```
