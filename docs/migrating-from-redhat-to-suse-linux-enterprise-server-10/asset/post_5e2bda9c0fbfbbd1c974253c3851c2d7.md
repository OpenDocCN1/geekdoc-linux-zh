
You can scan your own system by entering the IP address 127.0.0.1. If an iSCSI target device is available on the tested system, a dialog similar to the following opens up:

![](img/63e88022bf135307e3eac051ad238b5b_426_0.png)

If there are several iSCSI target devices available, they will all get listed. The iqn (iSCSI Qualified Name) is used to identify the target.

After selecting the iSCSI target from the list you have to log in using the **Log In** button.

The following dialog appears:

![](img/63e88022bf135307e3eac051ad238b5b_427_0.png)

By default there is no authentication necessary. However, if you have, for example, configured your iSCSI target device with incoming authentication, then you have to select **Outgoing Authentication** in this dialog and enter the same username and password which you used for the iSCSI target configuration.

After selecting **Next**, the **Connected Targets** tab displays your configured iSCSI devices.

With the **Toggle Start-Up** button you can switch between **automatic** and **manual**, which defines how the device is activated.

Select **Finish** to write the settings to the system.

The client configuration is stored in the file /etc/iscsi.conf and within the directory /var/lib/open-iscsi/ in the database files discovery.db and node.db. The tool to use for manual configuration of these files is iscsiadm.

![](img/63e88022bf135307e3eac051ad238b5b_428_0.png)

The name of the iSCSI initiator is contained in the file **/etc/initiatorname.iscsi**.

```
da3:~$ cat /etc/initiatorname.iscsi

# DO NOT EDIT OR REMOVE THIS FILE!

# If you remove this file, the iSCSI daemon will not start.

# If you change the InitiatorName, existing access control lists

# may reject this initiator. The initiatorName must be unique

# for each iSCSI initiator. Do NOT duplicate iSCSI InitiatorNames.

InitiatorName=iqn.1996-04.de.suse:01.42:0cb385f5
```

A description of how iscsid, iscsiadm and the configuration files play together is contained in **/usr/share/doc/packages/open-iscsi/README**.

In the file **/var/log/messages** you should see entries similar to the following:

```
Oct 4 11:55:56 da3 kernel: scsi3 : iSCSI Initiator over TCP/IP, v1.0-595

Oct 4 11:55:56 da3 kernel: sess_param (173) 1 1 1 8192 8192 262144 65536 2 0 1 1 1 0 1 1

Oct 4 11:55:56 da3 kernel: Vendor: IET Model: VIRTUAL-DISK

Rev: 0

Oct 4 11:55:56 da3 kernel: Type: Direct-Access

ANSI SCSI revision: 04

Oct 4 11:55:56 da3 kernel: SCSI device sdb: 2097152 512-byte hdwr sectors (1074 MB)

Oct 4 11:55:56 da3 kernel: sdb: Write Protect is off

Oct 4 11:55:56 da3 kernel: sdb: Mode Sense: 77 00 00 08

Oct 4 11:55:56 da3 kernel: SCSI device sdb: drive cache: write through

Oct 4 11:55:56 da3 kernel: SCSI device sdb: 2097152 512-byte hdwr sectors (1074 MB)

Oct 4 11:55:56 da3 kernel: sdb: Write Protect is off

Oct 4 11:55:56 da3 kernel: sdb: Mode Sense: 77 00 00 08

Oct 4 11:55:56 da3 kernel: SCSI device sdb: drive cache: write through

Oct 4 11:55:56 da3 kernel: sdb: unknown partition table

Oct 4 11:55:56 da3 kernel: sd 3:0:0:0: Attached scsi disk sdb

Oct 4 11:55:56 da3 kernel: sd 3:0:0:0: Attached scsi generic sg2 type 0

Oct 4 11:55:56 da3 iscsid: version 1.0-064

Oct 4 11:55:56 da3 iscsid: iSCSI daemon with pid=6172 started!

Oct 4 11:55:56 da3 iscsid: iSCSI sync pid=6173 started

Oct 4 11:55:56 da3 iscsid: connection:0 is operational now
```

You can see that there is a new SCSI device available (/dev/sdb). You can create partitions using fdisk, create file systems on the partitions and mount them.

With the command lsscsi you can see all available SCSI devices.

In case you want to see whether any active iSCSI connection exists, have a look into the file /proc/net/iet/session on the server hosting the target using cat. You can see all iSCSI connections to a target on this host, as in the following example:

```
da3:~ # cat /proc/net/iet/session
tid:1
name:iqn.2006-10.com.digitalairlines:d3d43303-8b2c-43df-83ea-6721942677e2
sid:281474980708864 initiator:iqn.1996-04.de.ruse:01.427f8cb385f5
cid:0 ip:127.0.0.1 state:active hd:none dd:none
```

You can see that a connection from the IP address 127.0.0.1 is established to the Target with the id 1 (tid).

While it is possible to have more than one connection you should keep in mind that it is not recommended to mount an iSCSI target more than once without any precautions (like a cluster file system on top of the iSCSI target).

## Mount iSCSI Targets Automatically at Boot Time

On the server (iSCSI target) side you have to make sure that the iscsi target service will be started automatically after a reboot. Use the command chkconfig iscsitarget on (or inserv iscsitarget) to do this.

On the client (iSCSI initiator) side the open-iscsi daemon has to start automatically at boot time. This is achieved using the command chkconfig open-iscsi on.

If you checked the button When booting in the respective YaST dialog, it is not necessary to issue the above chkconfig commands.

Generally you enter all the devices which should be mounted automatically at boot time into the file /etc/fstab. One problem you face with iSCSI devices is that no network is available when the file /etc/fstab is read during the boot process. Another problem is that you do not know for sure which local SCSI device will be used for the iSCSI target.

There is a solution for both problems. To be sure that the iSCSI device will be mounted to the same directory every time you have to use the UUID (Unique Universal ID) from the partition. To establish the UUID of a device use the following command:

```
da3:~ # udevinfo -q symlink -n /dev/sdb1
disk/by-id/iscsi-149454000000000000000001000005d9a01000 200800-part1
disk/by-path/ip-127.0.0.1:3260-iscsi-ign.2006-10.com.digit alairlines:d3d4303-8b2c-43df-83ea-6721942677e2-part1
disk/by-uuid/8b4dcb80-372d-44ba-a35b-96b5619b8237
```

In this example, the last line contains the UUID of the device /dev/sdb1. Now you can create an entry like the following in /etc/fstab to mount this iSCSI device to the /iscsi directory:

```
/dev/disk/by-uuid/8b4dcb80-372d-44ba-a35b-96b5619b8237
/iscsi auto hotplug,defaults 0 0
```

With the mount option hotplug the first problem is also solved. This option signifies that the hotplug daemon, which is started after the network, will take care of this mount.

## Exercise 9-1

### Set up an iSCSI Target and an iSCSI initiator

In this exercise, you learn how to set up an iSCSI target and how to access that target using an iSCSI initiator.

You will find this exercise in the workbook.

(End of Exercise)

## Summary

| Objective | Summary |
| :--- | :--- |
| **1.** iSCSI Background | The Internet Small Computer Systems Interface implements the regular SCSI commands over IP. The server offering storage is called iSCSI target, the client using that storage is called iSCSI initiator. |
| **2.** iSCSI Configuration | iSCSI target and initiator can easily be configured using the respective YaST modules. The iSCSI Target configuration is stored in /etc/ietd.conf. The iSCSI initiator configuration is stored in /etc/iscsi.conf, /etc/initiatorname.iscsi, and in the files discovery.db and node.db in /var/lib/open-iscsi. |

# SECTION 10 Cluster File Systems

With a cluster file system it is possible to share a file system between systems. In the cluster jargon these systems are called nodes. Cluster file systems are also known as "shared disk file systems". The benefit of these file systems is that data is still available to the remaining nodes if one node fails. Cluster file systems are routinely used in high availability environments.

Different cluster file systems are available for Linux, the best known are:

- OCFS (Oracle Cluster File System)
- GPFS (General Parallel File System)
- GFS (Global File System)
- LUSTRE

## Objectives

- 1. Global File System (GFS)
- 2. Oracle Cluster File System 2 (OCFS2)
