
# 888 Part V ◆ SUSE Linux in the Enterprise

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_732_0.png)

For more information on using fdisk to create partitions, see Chapter 3.

When your storage has been configured, you should tell SUSE that it needs to load the Qlogic driver at boot time so that you can mount the filesystems using fstab. To do this, edit the file /etc/sysconfig/kernel and add the Qlogic driver to the MODULES_LOADED_ON_BOOT list. Every module listed in MODULES_LOADED_ON_BOOT will be automatically loaded when the system boots. Each module is the module without the .ko extension as found in /lib/modules.

```
MODULES_LOADED_ON_BOOT= *cdrom ide-cd ide-scsi qla2300
```

# Disaster Recovery

In recent years, disaster recovery (DR) has become a very important part of an organization. This is not only for the enterprise, but also for any company. DR can mean anything from storing backups your network at a server, off-site location to replicating data in real time to a DR site.

DR is not just about saving data in the event of a disaster but also a methodology on how to bring your business back up when the worst happens. Most organizations realize that the quicker they can get back a DR site, the less they will lose. To do this, real-time data replication has become very popular.

Most SAN controllers block-level replication over fiber to another location. This is a very costly DR solution. However, it is a solution that is very resilient and fast. The main problem is that you need to have a very fast connection to your DR site, which could involve linking dark fiber directly to the site, using a high-capacity link, and employing iSCSI or an IP to Fiber translator, which is again very costly.

Luckily, DRBD has a replication service called DRBD that mirrors a disk device over TCP/IP to another server. Philip Reiner wrote DRBD while writing his thesis and has very elegant ways to transfer data across the network.

DRBD works on the block level of a device which has no understanding of files, directories, or filesystems. It transfers any changes to the device, whether they are metadata or file changes. DRBD works by storing a bitmap of the disk and transferring dirty data across the network based on changes to the bitmap to another device on the machine.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_732_1.png)

DRBD provides a shared storage system and is seen by Linux as a disk device in the same way that a SAN is seen. This also produces the problem you you have with sharing a disk between two machines with a standard Linux filesystem. In this mind, you should never mount your DRBD device on both machines at the same time because you will probably corrupt your data at some point.

# Setting Up a DRBD Pair

Before configuring DRBD, make sure it is installed using YaST. By default, the DRBD system is not installed. For more information on installing packages, refer to Chapter 1.

To configure the partners, you need to create a single DRBD configuration that is used on both machines, /etc/drbd.conf. A DRBD configuration file needs to contain a resource definition that describes the DRBD devices. This definition will contain the host names of the partners, IP addresses, and the devices you want to keep synchronized.

DRBD works on the block level, so you need to specify the partition, not the mount point, of the filesystem.

> Note: When defining your hosts, one must be the primary, and another the secondary node (synchronizing from one to the other). With in mind, the secondary node's device you are synchronizing to be the same or bigger than the primary's node.

If you have multiple devices that you want to synchronize, you can specify multiple resource definitions in the same file. For example, if you want to synchronize /dev/sdb2 to 192.168.0.5 and synchronize /dev/sdb3 to 192.168.0.6, you can specify two resource definitions.

When you define a host in the DRBD definition section, you need to specify the name returned by the `hostname` command. This parameter is paramount to the operation of DRBD, and if it is incorrect, it will fail.

In this listing, we show a sample configuration for a DRBD resource.

```
resource my-resource {
    disk /dev/sdb1;
    on primary {
        address 192.168.0.5:7788;
        policy primary;
    }
    on secondary {
        address 192.168.0.6:7788;
        policy secondary;
    }
}
```
