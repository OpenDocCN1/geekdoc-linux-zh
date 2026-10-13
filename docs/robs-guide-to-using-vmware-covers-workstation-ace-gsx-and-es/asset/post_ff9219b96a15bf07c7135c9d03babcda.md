
29. Power off the two nodes and add a Fixed Sized SCSI disk to both node one and node two. Do not forget to click Allocate disk space now. Make sure it is configured on SCSI bus 1 just as it is on your quorum disk. For example, if your quorum disk is SCSI 1:0, configure your new disk as SCSI 1:1.

After adding your disk, your configuration should look like the one in Figure 24.12.

![](img/25fe75b93b97a021effaba85db112a52_261_0.png)

Figure 24.12: Add a second SCSI disk to the Windows cluster for shared data.

Tip: If you forget to specify the disk for channel 1, you can always click the Advanced button (see Figure 24.12) to change the disk to SCSI 1:1.

30. First power on node one.

31. Open Disk Management in Computer Management and format the disk and assign a drive letter.

32. Next, we are going to create a new group in Cluster Administrator. Click Groups in the left panel and select New → Group.

33. Enter a name for the group (for example Shared Disk) and click Next to create the group. In the Preferred Owners window, select the nodes where the new Group will be available.

![](img/25fe75b93b97a021effaba85db112a52_262_0.png)

Figure 24.13: Assign nodes to the shared disk group.

34. Right-click the newly created group and select New → Resource.

![](img/25fe75b93b97a021effaba85db112a52_262_1.png)

Figure 24.14: Data Disk configuration.

Enter a name such as Data Disk for the resource, and select Physical disk as the Resource Type.

35. In the next window, select the cluster nodes for which the disk will be available.

36. In the next window, select the newly added disk and click Finish to create the resource.

37. At this point the resource will become available online and it is accessible from Windows Explorer.

38. Start node two and when it is online use Cluster Administrator to move the group to node two. The disk is now accessible via node two.

![](img/25fe75b93b97a021effaba85db112a52_263_0.png)

Figure 24.15: Test the cluster by moving the data disk to another node.

You have now configured your two node clusters in Windows Server 2003.

Have fun with your newly built cluster!

## Be careful to suspend the cluster nodes

The cluster nodes will continuously keep each other informed about their status. If a node is not available, it will be marked as off-line. If you suspend a cluster node, it will no longer be available to the other node(s) in the cluster.

You may think that suspending both cluster nodes at the same time is the solution. This can work, if you are fast enough, but if you bring the server back on-line from the suspend mode, resuming operation could take some time. This is especially the case if you resume two servers at the same time. There is a fair chance that they will not resume exactly at the same time (depending on your hardware), or that your host is so busy with this operation that the guests are slow, and the heartbeat between the cluster nodes gets lost.

The best thing to do is to either take all the servers in the cluster (or all but one) off-line, and then suspend all of them. Otherwise, just shutdown the operating system and power off the virtual machines.

## Part 5

### Introduction to VMware GSX Server

![](img/25fe75b93b97a021effaba85db112a52_266_0.png)

## 30 Introduction to VMware GSX Server

Now that you have made it to this chapter of the book, you should already know what VMware Workstation is. Also, you should be familiar with creating and running virtual machines and you should know how the virtualization technology can be used. But you may wonder why you would use a VMware server version instead of the Workstation software. In this chapter, I will explain in which scenarios it is better to use a server product instead of the Workstation version. Next, I will explain how to install VMware GSX Server on Windows and Linux. The next chapters in this part of the book contain information about management and configuration.

### 30.1 When to Use a VMware Server Version

Running multiple virtual machines on one hardware box is the basic functionality of any VMware product. You can use an existing machine in your organization, install VMware Workstation, and run several servers from your production environment, by using virtual machines. So, why bother using a server version?

There are several reasons, and some of them are technical, which I will discuss later. Let’s start with the manageability of your environment. With individual virtual machines in VMware Workstation, you can only manage them from the actual PC or server, where they are running. Powering on and off and changing the configuration requires access to the VMware application on the host computer. You may have to go to the machine physically. Or, you may be able to access the display with VNC. But you can still only do that with one administrator at a time. So as soon as more than one administrator needs to manage the virtual machines, you will need more advanced management capability.

Note: not only are there technical and usability issues with using VMware Workstation in this way. You also do not comply with the End User License Agreement for VMware Workstation that is very specific that the product is intended for one specific individual user only.

VMware GSX Server and ESX Server provide the management capability that you need for working with virtual machines from different locations. First of all, you can power your virtual machines on and off from a browser based management interface. The management interface also allows you to monitor the usage and performance of virtual machines. In addition, you can use the Remote Control utility to access the virtual machine at the hardware level. This allows you to work with the machine just as if it was a regular virtual machine running on your own PC, even when the operating system inside the VM has crashed. And last but not least, more than one administrator can work with a machine simultaneously. So, a server version takes away all of the manageability issues that you may encounter with VMware Workstation.

From a technical perspective, there are not that many VMware GSX server features compared to Workstation version 5. Workstation version 5 even has a few advantages over VMware GSX Server 3.2 in terms of memory management and performance improvements in suspend/resume and snapshot technology. At the time of writing this book, it is not clear when these new technologies may be implemented in VMware GSX Server. However, VMware traditionally introduces new functionality in Workstation first (where it can be exposed to the largest number of customers), and then rolls it out over time in to the other products.

The greatest technical advantages over using VMware Workstation can be found in VMware ESX Server. Chapter 1 contains an introduction to this product. The benefits include huge improvements in hard disk performance, memory management, and stability. For running multiple production servers, VMware ESX Server is certainly the platform of choice.

One final difference between purchasing a server version over VMware Workstation is that the server version always comes with a support contract. If you are seriously thinking about running virtual machines in a production environment, you must definitely consider buying a server version with support.

### 30.2 Choosing Between GSX Server and ESX Server

When you decide to virtualize the servers in your environment with a VMware server version, you need to decide whether you want to do that with VMware GSX Server or VMware ESX Server. Many consultants and resellers will always recommend the ESX Server and tell you that it is the only mature server virtualization product. However, it is my belief that there are still many usage scenarios where GSX Server is an excellent choice.

First, let's take a look at some of the differences between the two products. An extensive comparison can be found in chapter 1, the introduction to VMware ESX Server. The main advantages of VMware ESX Server over VMware GSX Server are:

- Immunity to host operating system stability risks
- Better hard disk performance
- Better memory management

When looking at the above advantages, it is clear that for an environment where availability and performance are important, VMware ESX Server is the platform to choose. No doubt that when you want to consolidate multiple servers on one hardware platform and you want to keep the performance you have on your physical hardware that you will have to choose the VMware ESX Server. Also, when you want to make use of the vMotion technology to increase the availability
