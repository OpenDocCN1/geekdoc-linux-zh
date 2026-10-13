# 27 Shared Disk Cluster with VMware ESX Server

This chapter covers the installation of two virtual machines with a shared SCSI disk. It will help to prepare for the installation of Novell Clustering Services or Microsoft Cluster Services software. This part is generic for NetWare and Windows. At this point you should have created at least two virtual machines with an operating system (Windows, Linux or NetWare) and the VMware tools installed. Power both virtual machines off to start the clustering configuration.

⚠️ Note: The example in this chapter is based on the configuration with the Management Interface. All configuration steps can also be performed from VirtualCenter. If you have this software installed, it should not be too difficult to translate the configuration options for your virtual machines from the Management Interface to VirtualCenter.

+   1. In the Management Interface, click on the virtual machine name (hyperlink) to open the configuration window. Go to the Hardware tab or select Configure Hardware from the popup menu to go to that tab directly.
+   2. Click the link for Add device at the bottom of the hardware configuration tab. See Figure 27.1 for the location of this option.

![](bbox=[0.115, 0.71, 0.885, 0.895])

Figure 27.1: Add the shared virtual disk from the Management Interface.

3. Select Hard Disk as the device type to be added. This will start the virtual disk configuration wizard. In the wizard, select to create a blank virtual disk.