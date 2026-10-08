
## Monitoring Notes

If you intend to write your own SNMP application, the numeric root OID of the Printer MIB is 1.3.6.1.2.1.43.

The Printer MIB requires portions of the MIB-II and the Host Resources MIB to be implemented. Many of the tables in the Printer MIB are indexed by hrDeviceIndex, from the Host Resources MIB.

The hrDeviceStatus field in the hrDeviceTable is combined with the hrPrinterStatus and hrPrinterDetectedErrorState fields in the hrPrinterTable to determine the specific status of a printer device. For example, if the hrPrinterStatus indicates an idle status and the hrDeviceStatus indicates a running status, then the corresponding printer is functioning normally. However, if the hrPrinterStatus is idle and the hrDeviceStatus indicates a warning status, then the printer has a status of noncritical alert active.

The prtAlertTable can record the list of alerts occurring for a printer device. The prtAlertCode indicates the specific printer problem, such as a paper jam, a paper tray missing, or low toner.

## The HP-UNIX MIB

The HP-UNIX MIB is a private MIB provided by Hewlett-Packard. It is meant to be an extension to the MIB-II. The HP-UNIX MIB contains important information about the users, jobs, filesystems, memory, and processes of a system. The number of users logged in to the system and the number of jobs running are both indications of how busy the system is. The amount of free swap space or filesystem space can be a warning of potential problems. The process status can be checked to see whether a particular application is still running normally on the target system.

## MIB Definition

Listing A-6 shows the complete specification for the HP-UNIX MIB, as defined by Hewlett-Packard.

### Listing A-6 HP-UNIX MIB specification

```text
enterprises
   [11] hp
       [2] nm
       [3] system
          [1] general
             [1] computerSystem
             [2] computerSystemUpTime
             [3] computerSystemUsers
             [4] computerSystemAvgJobs1
             [5] computerSystemAvgJobs5
             [6] computerSystemAvgJobs15
             [7] computerSystemMaxProc
             [8] computerSystemFreeMemory
             [9] computerSystemPhysMemory
             [10] computerSystemMaxUserMem
             [11] computerSystemSwapConfig
             [12] computerSystemEnabledSwap
             [13] computerSystemFreeSwap
             [14] computerSystemUserCPU
             [15] computerSystemSysCPU
             [16] computerSystemIdleCPU
             [17] computerSystemNiceCPU
          [2] fileSystem
             [1] fileSystemMounted
             [2] fileSystemTable
                [1] fileSystemEntry
                   [1] fileSystemID1*
                   [2] fileSystemID2*
                   [3] fileSystemName
                   [4] fileSystemBlock
                   [5] fileSystemBfree
                   [6] fileSystemBavail
                   [7] fileSystemBsize
                   [8] fileSystemFiles
                   [9] fileSystemPfree
                   [10] fileSystemDir
          [4] processes
             [1] processNum
             [2] processTable
                [1] processEntry
                   [1] processPID*
                   [2] processIdx
                   [3] processUID
                   [4] processPPID
                   [5] processDsize
                   [6] processTsize
                   [7] processSsize
                   [8] processNice
                   [9] processMajor
                   [10] processMinor
                   [11] processPgrp
                   [12] processPrio
                   [13] processAddr
                   [14] processCPU
                   [15] processUtime
                   [16] processStime
                   [17] processStart
                   [18] processFlags
                   [19] processStatus
                   [20] processWchan
                   [21] processProcNum
                   [22] processCmd
                   [23] processTime
                   [24] processCPUTicks
                   [25] processCPUTicksTotal
                   [26] processFss
                   [27] processPctCPU
                   [28] processRssize
                   [29] processSUID
                   [30] processUname
                   [31] processTTY
          [5] cluster
             [1] isClustered
             [2] clusterTable
                [1] clusterEntry
                   [1] clusterID*
                   [2] clusterMachineID
                   [3] clusterType
                   [4] clusterCnodeName
                   [5] clusterSwapServingCnode
                   [6] clusterKcsp
                   [7] clusterCnodeAddress
                   [3] clusterCnodeID
             [2] hpxx
                [2] hp9000s300
                [3] hp9000s800
                [5] hp9000s700
             [10] hpsun
                [1] sparc
             [1] sun4
             [2] sun5
             [8] hp386
          [4] interface
             [1] ieee8023Mac
                [1] ieee8023MacTable
                   [1] ieee8023MacEntry
                      [1] ieee8023MacIndex*
                      [2] ieee8023MacTransmitted
                      [3] ieee8023MacNotTransmitted
                      [4] ieee8023MacDeferred
                      [5] ieee8023MacCollisions
                      [6] ieee8023MacSingleCollisions
                      [7] ieee8023MacMultipleCollisions
                      [8] ieee8023MacExcessCollisions
                      [9] ieee8023MacLateCollisions
                      [10] ieee8023MacCarrierLostErrors
                      [11] ieee8023MacNoHeartBeatErrors
                      [12] ieee8023MacFramesReceived
                      [13] ieee8023MacUndeliverableFramesReceived
                      [14] ieee8023MacCRCErrors
                      [15] ieee8023MacAlignmentErrors
                      [16] ieee8023MacResourceErrors
                      [17] ieee8023MacControlFieldErrors
                      [18] ieee8023MacUnknownProtocolErrors
                      [19] ieee8023MacMulticastsAccepted
             [7] icmp
                [1] icmpEchoReq
             [13] snmp
                [1] trap
                   [1] trapDestinationNum
                   [2] trapDestinationTable
                      [1] trapDestinationEntry
                         [1] trapDestination*
                [2] snmpdConf
                   [1] snmpdConfRespond
                   [2] snmpdReConfigure
                   [3] snmpdFlag
                   [4] snmpdLogMask
                   [5] snmpdVersion
                   [6] snmpdStatus
                   [7] snmpdSize
                   [9] snmpdWhatString
                [4] authfail
                   [1] authFailTable
                      [1] authFailEntry
                         [1] authIpAddress*
                         [2] authTime
                         [3] authCommunityName
             [17] openView
                [2] openViewTrapVars
                   [1] openViewSourceId
                   [2] openViewSourceName
                   [3] openViewObjectId
                   [4] openViewData
                   [5] openViewSeverity
                   [6] openViewCategory
                   [7] openViewFilter
                   [8] openViewEntity
                   [9] openViewAddress
                   [10] openViewPpid
             [1] hpOpenView
```

## Monitoring Notes

The mnemonic root OID for the HP-UNIX MIB is iso.org.dod.internet.private.enterprises.hp.nm. If you intend to write your own SNMP application, you need to know the numeric root OID of the HP-UNIX MIB is 1.3.6.1.4.1.11.2.

HP’s EMS HA Monitors product uses this MIB to monitor the current number of users and jobs on a system and the amount of free filesystem space.

This MIB can be a useful place to find information about the specific processes running on a system, such as their CPU utilization, priority, and resident set size. However, you may have a difficult time using a MIB Browser to wade through the numerous process table entries; this information is best queried from a customized SNMP application.

Note that this MIB contains information on NFS diskless clusters, but not on HP’s high availability or EPS clusters. Information on these clusters is provided in the following sections.

## HP Cluster MIB

The HP Cluster MIB is a private MIB provided by Hewlett-Packard. It defines cluster membership information for the high availability and EPS clusters.

## MIB Definition

Listing A-7 shows the complete specification for the HP Cluster MIB, as defined by Hewlett-Packard.
