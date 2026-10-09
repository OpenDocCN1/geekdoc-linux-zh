
mind that because the node will not be running this heavy workload unless you are
in a failover condition, it may not be obvious—until a failure and resulting failover
of resources occurs—that it does not have the necessary processing power for high
availability.

## Disks and Volume Groups

In a cluster environment, an application moves from a failed node to a surviving node.
Since you want your application to use only the most current data, you’ll want to share
the disk subsystem between nodes. This can be done with SCSI-2, SSA, or RAID
technology. See the diagrams that follow for various cable connections. SCSI-2 has a
limit of four initiators per bus, which limits you to a maximum of four nodes per
cluster. SSA configurations vary *from two to eight* nodes per loop. An IBM Shark can
have as many as 32 nodes sharing the same volume group.

Here is a SCSI-2 “twin-tailed” configuration with a special “Y” cable to put the
terminators on the external bus:

![](img/82f851021955589d82b22750fb3b1646_624_0.png)

Here is an SSA configuration with serial cables wired in a loop:

![](img/82f851021955589d82b22750fb3b1646_624_1.png)

This configuration shows RAID using SCSI-2 (RAID is also supported with SSA
and FIBRE connections):

![](img/82f851021955589d82b22750fb3b1646_624_2.png)

Here are the basic steps you take to get the disk hardware ready for HACMP:

1. First, set up the shared disks. The ODM (Object Data Manager) requires unique names for all devices configured. Using your design, identify the volume groups, logical volumes, and fileystems that will reside on the shared disks. Assign unique and meaningful names to all logical volumes (including the *shared jfs log*).
2. If you will be using NFS, select the major number for your volume group. Run **lvmf major** on each server to identify a common unused value on all systems. Assign the major number to the volume group when you create it using the *-V* option
3. Make sure the volume group has auto*varyon* set to *no* so that HACMP, not the AIX boot process, controls the varyon of the volume group. Then create all the logical volumes in your volume group.
4. Run the *logform* command on the *jfslog* logical volumes before creating any fileystems. Then create each fileystem on a previously defined logical volume.
5. Finally, varyoff the volume group and run **importvg -V** <major number> >**Y** <volume group name> **hdiskx** to get the volume group definitions on the other nodes.
6. After importing, run **chvg -a n** (volume group name) to change the auto varyon setting to *no*.
7. Run *varyoff* and **importvg** on the next server until all of the cluster nodes have the same volume group definitions.

Proper operation of the shared fileystems can be checked by simply running a *varyonvg* of the volume group to the node and mounting the fileystems. If this test works without any errors, then unmount the fileystems and *varyoffvg* the volume group. When all nodes pass this test successfully, you are ready to set up the networks.

## Networks

HACMP uses two different networks to eliminate SPOFs. The public IP network attaches the clients to the server nodes. The private “serial” network is used by the cluster nodes to verify and troubleshoot network/node problems. A two-node cluster with traditional IP address takeover requires six IP addresses and two subnets. Each node requires a boot address (the address that AIX stores in the ODM and initially assigns to the adapter when booting AIX), a service address (commonly known to clients when the node is active), and a standby address (the backup “spare tire” that is used if the service adapter fails). In this configuration, the boot and service address must be on the *same* subnet and the standby adapters must be on *different* subnets to ensure that packets are sent and received on particular adapters.

Note that in HACMP/ES version 4.5, the same two-node cluster can use IP aliasing for better performance on failover. In this case, the configuration requires boot addresses (each pair on a separate subnet) and a service address on a different subnet from the boot addresses. (No standby adapters are used.) Therefore the alias network configuration requires six addresses and three subnets.

See the diagram in Figure 28-4 for a typical non-aliased IP network using Ethernet adapters. Notice they are connected to the same physical network; this makes the failover between adapters transparent to the client systems. This is an Ethernet network design with one service address and one standby address per node. The lower network cable is the RS232 serial network.

The serial network ensures that the nodes do not become isolated if the IP network fails. Traditionally, RS232 was used as a point-to-point serial connection between nodes for cluster messaging. If the RS-232 ports are not available, target mode SCSI (TMSCSI), or target mode SSA (TMSSA), can be used. Target mode functionality has been extended to SSA with a TMSSA device driver.

# TUNING AIX FOR HACMP

To ensure that AIX works as expected in an HACMP cluster, several default AIX settings and files must be altered. In addition, certain AIX settings may be tuned for better performance.

![](img/82f851021955589d82b22750fb3b1646_626_0.png)

## Changing Default AIX Settings

Here are some of the AIX settings that must be changed to run HACMP.

### Network Option Settings

HACMP/ES requires that the `nonlocsscroute`, `bcasting`, `ipscroutesend`, `ipscroutercv`, and `ipscrouteforward` network options be set to 1; this is automatically changed during `clstrmgrES` initialization.

### The /etc/rc.net File

By default, AIX 5.1 NFS clients do not respond to a ping on the broadcast address. Therefore, on any clients that use NFS, you need to edit the `/etc/rc.net` file to set the network option bcasting to 1.

### Placing IP Addresses in /etc/hosts and /.rhosts Files

The `/etc/hosts` file on each node in the cluster must include the IP address and an “IP label” for all service, standby, and boot adapters for all cluster nodes. The IP label is a name associated with an IP address. Your naming convention for these labels might include the AIX interface name (as in `node1ent0`) or might identify the adapter function (as in `node1svc`, `node1boot`, and so on). Here is an example of `/etc/hosts` file entries for a service and a standby adapter:

```
100.100.50.1   node1svc
100.100.51.1   node1stb
```

The `/.rhosts` file on each cluster node must list, for all nodes, the hostname and the IP labels for the service and boot adapters. (If you are using Kerberos security, this is not necessary.)

### Tuning I/O Pacing

By default, AIX is installed with high- and low-water marks set to zero, which disables I/O pacing. For an HACMP cluster to behave correctly during large disk writes, enabling I/O pacing is required. Although the most efficient high- and low-water marks vary from system to system, an initial high-water mark of 33 and a low-water mark of 24 provide a good starting point. These settings only slightly reduce write times and consistently generate correct failover behavior from the HACMP software.

### Further Tuning for HACMP

Cluster nodes sometimes experience extreme performance problems, such as large I/O transfers, excessive error logging, or lack of memory. When this happens, the cluster manager can be starved for CPU time. Misbehaving applications running at a priority higher than the cluster manager can also cause this problem.

Setting tuning parameters correctly helps avoid such performance problems. It is recommended to adjust the AIX high and low watermarks for I/O pacing and the AIX *syncd* frequency rate first. Then, if further tuning proves necessary, you can adjust certain HACMP network tuning parameters such as failure detection rate and grace period for each type of network. See the HACMP manuals for complete information on these tasks.

## CREATING A CLUSTER: DEFINING AND CONFIGURING RESOURCES

After configuring the cluster topology, you configure the highly available resources. Planning for and configuring resources takes careful thought and implementation.

The many resource types and their individual configuration instructions are discussed in detail in the HACMP manuals.

### SYNCHRONIZING THE CLUSTER

Synchronizing the cluster sends the entire cluster information contained on the local node to the remote nodes. You must synchronize cluster *topology* after defining or changing the cluster’s node, disk, network, or adapter configuration. You must synchronize cluster *resources* after defining or changing the cluster’s resource configuration.

During synchronization, a cluster verification utility runs; *clverify* checks that the configuration is valid and presents error or warning messages for any invalid or missing configuration information. This verification ensures that the AIX environment can support the cluster configuration, and that all nodes agree on the cluster topology, the network configuration, and the ownership and takeover of HACMP resources. You can add your own custom verification checks in addition to the ones HACMP automatically runs. When you make a change, or when you are first configuring HACMP, always work from the same node, and do the synchronization from the same node. If you make a change on one node and do the synchronization from a different node you overwrite the changes that you just made.

### TRADITIONAL IP ADDRESS TAKEOVER AND IPAT VIA IP ALIASING

Traditional IP address takeover (IPAT), in all HACMP Classic versions and in HACMP/ES prior to version 4.5, moves the IP address of an adapter on one node
