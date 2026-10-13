# 23 Preparing for a Windows Server 2003 Cluster

This chapter describes how to prepare for a cluster with two Windows Server 2003 servers and the Microsoft Cluster Server Software. This chapter provides general information for a cluster in VMware Workstation, or VMware GSX Server and ESX Server.

This chapter describes the system requirements for your Windows Server 2003 cluster, and explains the required preparation steps prior to getting started.

The instructions in this chapter are a summary of the Guide to Creating and Configuring a Server Cluster under Windows Server 2003. This official Microsoft publication is available on the web at:

```
www.microsoft.com/technet/prodtechnol/windowsserver2003/technologies/clustering/default.mspx
```

# Before Getting Started

The required software is Windows Server 2003 Enterprise Edition or Datacenter Edition. Because Enterprise Edition is easily available as an evaluation copy, this chapter only covers the Windows Server version.

# 23.1 Creating the Virtual Machines for your Windows Cluster

You can create your virtual machines for the Windows Server 2003 cluster in the normal way. You need to configure two virtual machines for your VMware product and install the Windows Server 2003 operating system.

Tip: When you run VMware Workstation version 5 to create your cluster, you can use the new cloning feature to create a copy of your first machine so that you do not have to go through the entire installation twice.

# Network Adapters

You must be aware that when you create your machines for Windows clustering, you will need more than one network adapter. Every server needs two network adapters; one for the public network and one for the private network. If you create your servers with two network adapters in the beginning, it will be very hard to distinguish which adapter is which. Therefore, we start out with one adapter in each virtual machine, and we will add a second adapter further on in this chapter.

The easiest solution is to use your bridged network adapter as the public adapter for the cluster nodes, and the host only adapter for the private network between the cluster nodes. This will be explained later on in this chapter. However, you could