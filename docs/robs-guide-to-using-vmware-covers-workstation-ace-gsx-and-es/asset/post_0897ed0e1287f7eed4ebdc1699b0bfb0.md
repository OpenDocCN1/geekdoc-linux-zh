
## 25 Shared Disk Cluster with VMware Workstation

This chapter covers the installation of two virtual machines with a shared SCSI disk. It is in preparation for the installation of Novell Clustering Services or Microsoft Cluster Services software. This part is generic for NetWare and Windows.

⚠️ Note: With VMware Workstation 4.5, clustering with a shared disk was not made an option. It was not documented in any way by VMware, because clustering is not supported in that product (it is only supported in GSX Server and ESX Server). That is also the reason that I moved to iSCSI for the first edition of my VMware guide. In this new edition, you can learn how to set up a cluster with VMware Workstation version 5.

### 25.1 Adding a Shared Disk to Virtual Machines

After installing two NetWare servers into a tree, and configuring them with the VMware tools, it is now time to add a shared disk that will be used for clustering.

💡 Tip: I prefer to use a separate disk as the Windows Quorum disk or for the NetWare Split Brain Detector partition, and a second shared disk for the data. With such a configuration, you have more flexibility to re-create the SBD partition, or to back up your VMware configuration.

First, power down both servers and close the VMware application. It is always a bad idea to manually edit the .VMX files while the application is running.

Open the .VMX files of both servers and add the following lines to the file:

```
disk.locking = "false"
diskLib.dataCacheMaxSize = "0"
diskLib.dataCacheMaxReadAheadSize = "0"
diskLib.dataCacheMinReadAheadSize = "0"
diskLib.dataCachePageSize = "4096"
diskLib.maxUnsyncedWrites = "0"
```

It does not matter where in the file you add these lines. Save the .VMX files and open the virtual machine software without powering the machines on.

On the first server, add a new virtual disk that will become the shared disk for clustering.

Follow these steps to perform this action:

- 1. Open the virtual machine settings and click **Add** to add a new device.
- 2. In the **Add Hardware Wizard** welcome screen, click Next.
- 3. Select **Hard Disk** as the type of device and click Next.

![](img/25fe75b93b97a021effaba85db112a52_228_0.png)

Figure 25.1: Add a new device to your virtual machine.

![](img/25fe75b93b97a021effaba85db112a52_228_1.png)

Figure 25.2: Select to add a hard disk.

- 4. In the Select a disk window select Create a new virtual disk and click Next.

![](img/25fe75b93b97a021effaba85db112a52_229_0.png)

Figure 25.3: Create a new virtual disk.

- 5. Change the default setting to SCSI and click Next (I always use SCSI for the shared disk so that it looks most like a real world clustering example and to make it easier distinguish between the server-IDE disks and the shared-SCSI-disk).

![](img/25fe75b93b97a021effaba85db112a52_229_1.png)

Figure 25.4: Select SCSI as the disk type.

- 6. In the Specify Disk Capacity window select the proper disk size.

In the image below, you can see that I have selected a half gigabyte disk size. That is adequate for a small shared disk that can hold some data. Remember that we also have to enable the option Allocate all disk space now, so that a 500 Mb file will be created on your hard disk. Selecting a 10 Gb disk could take up excessive space on your workstation.

Whether you need to split the disk file in two gigabyte files depends on your file system. FAT32 only supports files up to four gigabytes and traditional FAT supports two gigabyte files. For both of them, you need to split the files into two gigabyte chunks.

![](img/25fe75b93b97a021effaba85db112a52_230_0.png)

Figure 25.5: Create a fixed size disk.

- 7. You will be warned that creating a pre-allocated disk may take a long time. If you are prepared to create the disk that you have selected, select Yes.
- 8. You can create your server in one directory together with this shared disk; however, I prefer to keep the configuration on separate directories because it provides a better overview.

![](img/25fe75b93b97a021effaba85db112a52_231_0.png)

Figure 25.6: Give the disk a descriptive name.

- 9. Click Finish. The fixed sized disk will now be created.
- 10. Close the configuration Control Panel for this virtual machine.
- 11. Open the virtual machine configuration for your second server. Follow the same steps as the ones that you performed on your first server to start adding a new hard disk to your server (steps 1, 2, and 3).
- 12. In the Select a Disk window, select Use an existing virtual disk.

![](img/25fe75b93b97a021effaba85db112a52_231_1.png)

Figure 25.7: In the second machine select the disk you have just created.

- 13. Browse the shared disk file (this is not the file with the f001 suffix). Select the .vmdk file which you created in step 8.

![](img/25fe75b93b97a021effaba85db112a52_232_0.png)

Figure 25.8: Select the existing shared disk.

- 14. Click Finish and close the virtual machine setting’s Control Panel.

## Where to go from here

### For NetWare

When the servers are up and running you may need to activate the SCSI hard disk driver, depending on your version of NetWare. This is explained in detail in section 14.7 “Using SCSI drivers in older NetWare servers”. After that, install the cluster services as described in chapter 28 “Installing Novell Cluster Services”.

### For Windows

Leave the servers powered off and continue with the configuration of Microsoft Cluster Services as described in chapter 29: “Configuring Microsoft Cluster Services Software”.

## 26 Shared Disk Cluster with VMware GSX Server

This chapter covers the installation of two virtual machines with a shared SCSI disk, in order to prepare for the installation of Novell Clustering Services or Microsoft Cluster Services software. This part is generic for NetWare and Windows.

The technology for sharing disks in GSX Server is called SCSI Reservation. This is an SCSI technology, where the servers can send Reserve and Release commands to the disk to gain access to a shared disk.

By adding the scsi1.sharedBus = "virtual" command to the .vmx file, SCSI Reservation is activated in the GSX Server virtual machines. And the disk.locking = "false" command disables the file locking, so that a virtual machine can not lock the virtual disk file and prevent the other cluster servers from accessing the virtual disk file.

### 26.1 Adding a Shared Disk to the Virtual Machines

After installing two servers with Windows, Linux or NetWare, and configuring them with the VMware tools, it is now time to add a shared disk that will be used for clustering.

Make sure that you have taken all the necessary preparation steps described in chapter 23: "Preparing for a Windows Server 2003 Cluster" or chapter 24: "Preparing for a NetWare 6.5 Cluster".

> Tip: I prefer to use a separate disk as the Windows Quorum disk or for the NetWare Split Brain Detector partition, and a second shared disk for the data. With such a configuration you have more flexibility to re-create the SBD partition, or to back up your VMware configuration.

On the first server, add a new virtual disk that will become the shared disk for clustering. I have created this example from a VMware virtual machine console. You could add additional hardware from the Management Interface, but it is much more convenient from the remote console application.

Follow these steps to perform this action:

- 1. Open the virtual machine settings and click the **Add** button to add a new device.
- 2. In the **Add Hardware Wizard** welcome screen, click **Next**.
- 3. Select **Hard Disk** as the type of device and click **Next**.

![](img/25fe75b93b97a021effaba85db112a52_234_0.png)

Figure 26.1: Add a new device.

![](img/25fe75b93b97a021effaba85db112a52_234_1.png)

Figure 26.2: Select to add a hard disk.

- 4. In the Select a disk window, select Create a new virtual disk and click Next.

![](img/25fe75b93b97a021effaba85db112a52_235_0.png)

Figure 26.3: Create a new virtual disk.

- 5. Change the default setting to SCSI, and click Next. Whether the default is IDE or SCSI depends on the operating system that you have selected for the virtual machine.

![](img/25fe75b93b97a021effaba85db112a52_235_1.png)

Figure 26.4: Select SCSI as the disk type.
