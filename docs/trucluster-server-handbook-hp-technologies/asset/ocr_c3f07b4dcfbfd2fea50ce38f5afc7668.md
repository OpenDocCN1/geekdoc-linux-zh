used for your users' applications and application data, and the file systems required for a data base (if you have a data base installed).

In any event, creation and allocation of RAID sets takes careful planning prior to implementation. If you invest the time to plan appropriately, you can be guaranteed that the planning will reap large rewards in terms of availability and scalability.

# 4.2.4.7 Spare Set for Your RAID Sets

Before we end this section on Hardware RAID configuration, let's discuss one last and sorely overlooked topic – the use of Spare Sets to support the RAID configuration. We have seen countless situations where the RAID configuration and implementation were absolutely beautiful except when it came to having an online Spare Set. Please remember that any hardware RAID set built on a RAID controller should always have a Spare Set with at least one disk drive in it. What is the purpose of the drive(s) in the Spare Set? If a drive that is a member of a RAID set fails, a good drive in the Spare Set will automatically take the place of the failed drive. This is one of those high availability issues that are too often overlooked.

Here is an example of adding two disk drives to a Spare Set.

```
HSG> add spareset disk10400
HSG> add spareset disk20400
```

# 4.2.5 Getting Storage Devices Seen at the Console – wwidmgr

Now that we have all our storage sets configured for the cluster's system disks, there will be a point where we will need to see and access each cluster member's boot_partition or boot disk from the system console. Unfortunately, this is not something that happens automatically. When will this need to be done? After the complete installation and configuration of Tru64 UNIX but before the installation of TruCluster Server. During the installation and operation of TruCluster Server, it is necessary to see and to access each cluster member's boot disk from each cluster member's system console.

We will use wwidmgr commands from the system console to view and to make viewable each cluster member's boot disk. How is this done and what are we really looking for? We are looking for the identifier or the wwid of the cluster member's boot_partition disk that we created on the RAID storage array.

Before we start using wwidmgr commands, please note that if the cluster member is an AS1200, AS4x00, AS8x00, GS60, GS60E, or GS140, the console must be set to diagnostic mode.

> 9 This only applies to the use of Fibre Channel based storage (HSG60 or HSG80 controllers). This step can be skipped if using SCSI-based storage.