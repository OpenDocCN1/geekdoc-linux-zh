prevent the failure of one drive from bringing down the entire storage pool. As described previously, leaving some unpartitioned space on a new drive gives you the option of extending a storage pool without adding another drive. During installation, a storage pool named SYS is created for the SYS volume. The SYS volume is then used to hold OS files and programs. To separate OS files from the organization's data, a network administrator must create one or more additional storage pools.

![](bbox=[0.12, 0.15, 0.91, 0.46])

Figure 3-7 **Storage pools**

# Creating Storage Pools

In NetWare 6.5, you create storage pools and their associated partitions by using the File System Creation Operations window (see Figure 3-8), which is accessed from the Partition Disks options of Remote Manager.

![](bbox=[0.12, 0.57, 0.61, 0.77])

Figure 3-8 **Creating a storage pool in Remote Manager**

Notice that this window has two options: Create a New Pool and Create a New Pool and Volume. The Create a New Pool option displays the NSS Pool Create window (see Figure 3-9), where Remote Manager automatically creates a new partition of the size specified in the Pool Size text box and then assigns that partition space to a new storage pool with the physical pool name specified in the Pool Name text box. You should use the Create a New Pool option when you want to create a storage pool that holds multiple volumes.