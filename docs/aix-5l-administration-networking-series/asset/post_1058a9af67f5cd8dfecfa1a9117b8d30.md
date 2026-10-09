
## NFS Capability

Extended NFS capability, formerly included only in the HANFS product, has been added to the basic HACMP architecture and is included in both HAS and HACMP/ES products, allowing you to do the following:

- Make use of reliable NFS server capability that preserves locks and dupcache (2-node clusters only).
- Specify a network for NFS mounting.
- Define NFS exports and mounts at the directory level.
- Specify export options for NFS-exported directories and filesystems.

## Highly Available Print Queues

In the event of a failover, the print jobs currently queued can be saved and moved over to the surviving node. The print spooling system consists of two directories: `/var/spool/qdaemon` and `/var/spool/lpd/qdir`. One directory contains files containing the data (content) of each job. The other contains the files consisting of information pertaining to the print job itself. When jobs are queued, there are files in each of the two directories. In the event of a failover, these directories do not normally fail over and thus the print jobs are lost.

In HACMP/ES, the plug-in `cluster.es.plugins.printserver` provides scripts to start and stop the print server process, a script to verify that configuration files are present and stored in a shared filesystem, and scripts called by the monitoring functions of HACMP/ES that check on print server process life. You can also move all of the print services directory structures to the shared disks so that the queued jobs are always available, even with HACMP classic.

## Highly Available WAN Communication Links

As of version 4.5, HACMP can provide high availability for three types of communication links:

- SNA configured over a LAN adapter
- SNA over X.25
- Pure X.25

With earlier HACMP releases, users could configure only SNA-over-LAN. (These links were termed CS/AIX communication links.) Support of the other protocols was previously available through the add-on HAWAN product.

LAN adapters are Ethernet, Token Ring, and FDDI adapters; these adapters are configured as part of the HACMP cluster topology.

X.25 adapters are usually, though not always, used for WAN connections. They are used as a means of connecting dissimilar machines, from mainframes to dumb terminals. Because of the way X.25 networks are used, these adapters are treated as a different class of devices that are *not* included in the cluster topology and *not* controlled by the standard HACMP topology management methods. This means that heartbeats are not used to monitor X.25 adapter status, and you do not define X.25-specific networks in HACMP. Instead, an HACMP daemon, **clcommnlinkd**, takes the place of heartbeats. This daemon monitors the output of the `x25status` command to make sure the link is still connected to the network.

Making a communication link highly available in HACMP involves these general steps: Define the communication adapters and links in the operating system (AIX), then define the adapters and links in HACMP, and finally add the defined communication links as resources in HACMP resource groups. Each of these steps must be carefully thought out and implemented; the communication link should be tested thoroughly outside of HACMP before you add it to the cluster resource group. For full information and instructions, see the HACMP user manuals.

### Highly Available Workload Manager Classes

AIX Workload Manager (WLM) is a systems administration resource included with AIX 4.3.3 and above. WLM allows users to set targets for and limits on CPU time, physical memory usage, and disk I/O bandwidth for different processes and applications; this provides better control over the usage of critical system resources at peak loads. As of version 4.5, HACMP allows you to configure WLM classes in HACMP resource groups so that the starting, stopping, and active configuration of WLM can be under cluster control.

For complete information on how to set up and use Workload Manager, see the AIX 5L Workload Manager (WLM) Redbook at `http://www.ibm.com/redbooks/`. For complete information on making WLM classes highly available resources in an HACMP cluster, see the HACMP user manuals.

### Highly Available Tape Drives

HACMP 4.5 allows you to configure highly available tape drives. To make a tape drive highly available, you first define it as a resource, including specifying start and stop scripts, and then you add the resource to a cluster resource group. Sample scripts are available in the `/usr/(/es/)/sbin/clusterc/samples/tape` directory. These sample scripts rewind the tape drive explicitly.

After adding a resource to a resource group, verify that the configuration is correct and then synchronize shared tape resources to all nodes in the cluster.

### Emulation Tools

HACMP includes emulation capability for running cluster event emulations and for testing error notification methods.

### Event Emulation

The HACMP Event Emulator is a utility that emulates cluster events and dynamic reconfiguration events by running event scripts that produce output but that do not affect the cluster configuration or status. The Event Emulator follows the same procedure used by the Cluster Manager given a particular event, but it does not execute any commands that would change the status of the Cluster Manager; thus it allows you to test a cluster's reaction to a particular event just as though the event actually occurred. You can run the Event Emulator through SMIT or from the command line.

> NOTE The Event Emulator requires that both the Cluster SMUX peer daemon (clsmuxpd) and the Cluster Information Program (clinfo) be running on your cluster.

### Error Emulation

HACMP provides a utility for testing your error notify methods. After you have added one or more error notify methods with the AIX Error Notification facility, you can test your methods by emulating an error. By inserting an error into the AIX error device file (/dev/error), you cause the AIX error daemon to run the appropriate prespecified notify method. This allows you to determine whether your predefined action is carried through, without having to actually cause the error to occur.

When the emulation is complete, you can view the error log by typing the erpt command to be sure the emulation took place. The error log entry has either the resource name EMULATOR or a name as specified by the user in the Resource Name field during the process of creating an error notify object. You can then determine whether the specified notify method was carried out.

### More Information

For more information and the latest manuals for HACMP and other high-availability products, see the following Web pages from IBM:

- http://www.ibm.com/servers/aix/products/ibmwa/high_avail_network/hacmp.html
- http://www.ibm.com/servers/eserver/pseries/library/hacmp_docs.html

### CHECKLIST

The following is a checklist for the key points in HACMP and clustering:

- Show how HACMP works and how to use it.
- Plan a cluster.
- What does HACMP actually do?
- Setup the hardware to create a cluster.
- Tune AIX for HACMP.
- Define and configure the resources to create a cluster.
- Synchronize the cluster.
- Define traditional IP address takeover (IPAT).
- Choose a resource group policy.
- Identify the administrative tasks for an HACMP system.

# PART XIII

Storage Area Networks and Network Attached Storage

## 29 SAN, NAS, and iSCSI Consolidated Storage

This page intentionally left blank.

# CHAPTER 29

## SAN, NAS, and iSCSI Consolidated Storage

The key concepts for storage these days are smaller, denser, and faster. In the forty-plus years of disk storage, one constant has remained the same. The rate at which you can read or write data on a disk is still dependent on how fast the disk platters spin. No electronics, adapters, or drivers can overcome the spindle speed dilemma. However, by making the platters smaller and denser while spinning the platter faster, IBM has achieved extraordinary results. As of this writing, the spindle speed has reached 15,000 RPM and the storage capacity of a single disk drive is up to 200GB and 200GB, with 400GB drives expected soon. In addition to these advancements in disk storage, write performance is enhanced by a large write cache available in many disk subsystems, and sequential data read performance is enhanced by a read-ahead cache. However, the read-ahead cache does not help for random disk reads.

At the other extreme are the micro-drives, which are about the size of a U.S. quarter. Currently, these drives have a storage capacity of 1GB or so. These micro-drives are coming to the market to replace flash memory cards for digital cameras and camcorders.

But what is the key to all of this increased storage capacity on such a small footprint? Well, there are really two keys at work. The first is the advancement in drive head technology with Giant Magneto-Resistive technology heads. These new drive heads are made of layered metallic coatings of magnetic material capable of reading and writing up to 40GB of data per square inch. The second area of advancement is in the material used to coat the disk platter. New breakthroughs by IBM and their business partners have made the disk platters more dense and able to store more data per square inch.

With this combination, how can you lose?

Compare these advancements with the past. For example, in 1956 the largest disk drive was 5MB. But this is not amazing part, this 5MB disk drive was three feet long and weighed over 200 pounds! These were the days when the IBM Customer Engineer (CE) could drive to your shop and fix the disk drive before it had a chance to spin down. Those were the days!

Leaving that aside, let's look at the latest in storage. If you have not noticed lately, storage is moving away from the server and onto networks. The old approach of each server having its own dedicated attached disk storage is gone. The new conception is that there will be no more wasted storage dedicated to a single server. The new storage paradigm is to have storage pools, managed by a vendor/OS-neutral network storage manager. This trend, called Enterprise Data Management, aims at consolidating the data into an environment that is more compatible with data sharing across a large variety of servers and operating systems.

### STORAGE CONSOLIDATION

Consolidation of data involves some new techniques to handle all of the copies of the same data that are required for the business. The production data is gold, so it must be protected at all cost. This is where the first copy comes in, the backup copy. A typical system usually consists of producing a split mirror backup. This is where the gold data is synced to a backup copy of the data, which is a mirror image. Then the mirror is broken so that the now static point-in-time backup copy can be copied to tape for off-site storage. Different shops have different options for what to do with the backup copy
