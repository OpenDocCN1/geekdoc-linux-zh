
To prevent this from happening, you must use virtual disks that are pre-allocated. These disks were known as “plain disks” with VMware version 2. In VMware Workstation 4 and 5 and VMware GSX Server 3.x, you can create fixed sized disks by selecting the check box Allocate Disk Space Now, when you create a virtual disk. This creates a disk file that is the same size as the number of megabytes or gigabytes that you specified when you created the disk. Therefore, make sure that you have enough space available on your hard disk when you create large shared disks.

For clustering purposes, it is OK to use a small disk (500 Mb), as the Quorum disk (Windows) or as the disk for the Split Brain Detector partition (Open Enterprise Server). You can then add other plain disks to your cluster, in order to store the actual data for your clustered applications.

## 22.2 How to Share a Disk

Clustering software uses a shared disk that two or more physical cluster nodes can access for storing data. The disk can be accessed by the physical servers via a shared disk channel (typically SCSI or Fibre Channel).

With a virtual machine we do not have a real Fibre channel or SCSI channel available, but we can use a shared virtual disk. However, it is important to realize that using a shared disk is only supported in VMware GSX Server and VMware ESX Server. These products contain a configuration for a shared disk with SCSI reservation. For VMware Workstation, you can use a shared disk but that is not supported by VMware. However, it does work fine in the workstation version when you follow the guidelines in this chapter.

Using a shared disk within VMware is a great solution for working with clustering software. There can still be some scenarios where you may want to cluster a virtual machine with a physical machine. Or, you may want to use storage that is available on a physical server.

### iSCSI Considerations

As I described earlier, shared disks stopped working with VMware Workstation version 4.5. Disks became corrupted because of the caching that was performed by the virtual machines. In the first edition of my VMware guide I explained how to use iSCSI as a work around for this problem. By using this protocol which transports SCSI blocks via TCP/IP packets, it is possible to build a cluster with every possible combination of hardware and operating system. Your virtual machines only rely on networking to build a cluster; they no longer require exclusive SCSI or Fibre channel access to a shared disk. With VMware version 5 the shared disk works fine again and in both cases of GSX server and ESX server using a shared disk is supported.

However, there can still be a need to use iSCSI in your clustering scenarios. An example of this is when you want to build a cluster with virtual machines that are running on separate hardware boxes. Or, in case you want to build a cluster with virtual machines that use an iSCSI target outside the virtual environment. Another application could be if you want to build a cluster with nodes that are virtual machine and physical servers. All these types of combinations are possible by using iSCSI; the sky is the limit.

Because iSCSI has become a more commonly used technology, I have decided not to keep the detailed iSCSI manual for creating clusters inside this VMware guide.

Note: Be aware that when implementing iSCSI, your network adapter also becomes the adapter that is used to access your storage device. This could cause a bottleneck. Therefore, make sure that you investigate the network's load and storage traffic for your cluster nodes if you plan to configure them with iSCSI. You may want to add extra physical network adapters to assign separate adapters to the regular networking part and to the storage networking part.

## 22.3 Preparing for a VMware Cluster Installation

No matter what type of cluster you are going to build, there are a few preparatory steps that you will need to take before creating the actual cluster. You must create at least two virtual machines that will form the cluster and you must install an operating system inside the two machines.

The flow for creating your VMware cluster is as follows:

- 1. Create two or more virtual machines in VMware Workstation, GSX Server, or ESX Server as you normally would do. This is covered in the OS specific chapters that will follow.
- 2. Install the guest operating system on all the virtual machines that will take part in the cluster. Refer to one of these chapters for detailed instructions:
  - Chapter 23: Windows
  - Chapter 24: NetWare
- 3. Add a shared disk to your cluster nodes. This step is different for every VMware product. Refer to one of these chapters for detailed instructions:
  - Chapter 25: VMware Workstation
  - Chapter 26: VMware GSX Server
  - Chapter 27: VMware ESX Server
- 4. Install the clustering software and configure the cluster inside your virtual machines. Refer to one of these chapters for detailed instructions:
  - Chapter 28: NetWare
  - Chapter 29: Windows

## 23 Preparing for a Windows Server 2003 Cluster

This chapter describes how to prepare for a cluster with two Windows Server 2003 servers and the Microsoft Cluster Server Software. This chapter provides general information for a cluster in VMware Workstation, or VMware GSX Server and ESX Server.

This chapter describes the system requirements for your Windows Server 2003 cluster, and explains the required preparation steps prior to getting started.

The instructions in this chapter are a summary of the Guide to Creating and Configuring a Server Cluster under Windows Server 2003. This official Microsoft publication is available on the web at:

```
www.microsoft.com/technet/prodtechnol/windowsserver2003/technologies/clustering/default.mspx
```

### Before Getting Started

The required software is Windows Server 2003 Enterprise Edition or Datacenter Edition. Because Enterprise Edition is easily available as an evaluation copy, this chapter only covers the Windows Server version.

### 23.1 Creating the Virtual Machines for your Windows Cluster

You can create your virtual machines for the Windows Server 2003 cluster in the normal way. You need to configure two virtual machines for your VMware product and install the Windows Server 2003 operating system.

Tip: When you run VMware Workstation version 5 to create your cluster, you can use the new cloning feature to create a copy of your first machine so that you do not have to go through the entire installation twice.

### Network Adapters

You must be aware that when you create your machines for Windows clustering, you will need more than one network adapter. Every server needs two network adapters; one for the public network and one for the private network. If you create your servers with two network adapters in the beginning, it will be very hard to distinguish which adapter is which. Therefore, we start out with one adapter in each virtual machine, and we will add a second adapter further on in this chapter.

The easiest solution is to use your bridged network adapter as the public adapter for the cluster nodes, and the host only adapter for the private network between the cluster nodes. This will be explained later on in this chapter. However, you could also bridge a second network adapter, and use it so that the private and public networks are both bridged, or you can use a second host only network adapter so that the private and public adapters are both working host only. It is up to you to decide which option you prefer.

The first adapter that you assign to your virtual machines (at creation time) will become the public adapter in the setup that you create in this chapter. Therefore, assign your servers a fixed IP address (on the network adapter that is in another subnet to your private network) that you will use between your cluster nodes.

In this chapter I use the following setup:

Table 23.1: IP addressing for the Microsoft Cluster example.

|  | Node 1 | Node 2 | Cluster management |
|---|---|---|---|
| Public Network Adapter | 192.168.1.101 | 192.168.1.102 | 192.168.1.150 |
| Private Network Adapter | 10.0.0.101 | 10.0.0.102 |  |

### 23.2 Install Two Servers in a Single Domain

Cluster services require that all your cluster nodes are in the same Active Directory domain. DNS must be configured, and all the servers must be configured as member servers or domain controllers. If a server is configured as a member server, then it needs to have access to a domain controller in your network. Since we are going to create a two node cluster in this chapter, it is important to assign the role of domain controller to both servers, because we do not want to have a single point of failure.

### 23.3 Pre-Configuring the Servers

At this point you should have created your virtual machines and installed the two Windows Server 2003 servers in a single domain. Now we can start with the necessary preparations inside the server operating systems.

- 1. Rename the first network adapter.

You have installed the servers with one network adapter each. This first network adapter will be your public network adapter. So, we are going to rename that adapter accordingly in order to be able to identify it easier later on. Go to Control Panel → Network Connections and rename the adapter to Public Network Adapter.
