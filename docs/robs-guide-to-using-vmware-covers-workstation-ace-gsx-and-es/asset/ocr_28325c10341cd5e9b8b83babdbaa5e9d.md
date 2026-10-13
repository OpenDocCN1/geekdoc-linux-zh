Tip: Also, check that you still have your **Private and Public network adapters** because if they have moved to another slot, they could be replaced by a new adapter called **Local Area Connection**. If needed, re-configure the adapter to be the Private or Public network adapter with the correct IP address. Repeat this step on node two in the next step.

5. Now power off the first node and power on the second node. The disk should now be available in node two. Go to **Disk Management** and assign the drive letter Q: to this disk. In Windows Explorer, you should now see the file that you have created from the first node. You can open this file and view the contents that you have added to the file from the first node. Also, check the network adapter configuration as described in the previous step.

If everything works, then power off node two again and power on node one.

6. On node one, start the Cluster Administrator (Go to Start → All Programs → **Administrative tools**).

7. Select **Create new cluster** from the dialog box.

![](bbox=[0.18, 0.67, 0.55, 0.79])

Figure 29.2: Create a new cluster.

8. The **New Server Cluster Wizard** has started. Click **Next** on the introduction screen.

9. In the Cluster Name and Domain Name selection screen, select your domain and enter a name for your cluster. This must be a unique and valid NETBIOS name.