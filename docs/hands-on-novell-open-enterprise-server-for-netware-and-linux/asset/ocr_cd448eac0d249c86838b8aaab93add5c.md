computer needs to be isolated from the LAN, yet you need Internet access for certain tasks, such as downloading patches. This option works only when your virtual PC is configured to get its IP address information automatically. If you have assigned your computer a manual IP address, you might need to temporarily change the IP address assignment to access the Internet.

+   *   *Host-only*—This option uses an internal network created by VMware that enables multiple virtual machines running on the local computer to communicate only with each other. With this option, the virtual network adapter doesn't communicate with the local computer's physical network adapter or with the local host computer. This option is ideal when you want to separate your virtual machines from the main network to prevent IP address conflicts or to test new network configuration settings.

You can change the setting of the virtual network card without having to power off your virtual machine by following these steps:

+   1.  In the VMware Console, right-click the tab of the virtual machine you want to change and click Settings.
+   2.  In the Hardware tab, double-click the Ethernet item to display the Network adapter dialog box shown in Figure C-13.

![](bbox=[0.12, 0.37, 0.43, 0.62])

+   3.  In the Network connection section, click to select the type you want to change to, and then click OK to save your setting.

# WORKING WITH VMWARE

After you have configured your virtual machine, you can begin using it much like you would any physical computer. VMware offers a number of features that can enhance your use of the system, described in the following sections.

# Starting and Stopping Virtual Machines

There are two basic ways to start a virtual machine. You can use the **Start** button on the VMware Console toolbar, or you can use **My Computer** to navigate to the folder containing the virtual computer files and then double-click the virtual machine configuration file (.vmx extension).