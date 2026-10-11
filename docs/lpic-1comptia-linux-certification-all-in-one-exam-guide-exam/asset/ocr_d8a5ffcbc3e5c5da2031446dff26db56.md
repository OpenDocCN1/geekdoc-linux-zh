![](bbox=[0.15, 0.08, 0.88, 0.34])

This system is very powerful. It’s what allows you to connect to the Internet and pull down web pages from a server somewhere else in the world. However, for it to work, your local system needs to know the IP address of the router to which it should forward packets if they are addressed to a system that doesn’t reside on the local network segment. You need to configure this parameter whenever you configure network settings on a Linux system. If you don’t, the system will be able to communicate only with systems on the same local network segment.

With this background in mind, let’s now discuss how to configure an Ethernet interface in a Linux system.

# ## Configuring Network Addressing Parameters

Probably the most common network interface you will work with in a Linux system is an Ethernet interface. Be aware that, under Linux, when we refer to a “network interface,” we are referring to

+   - The physical network interface card (NIC) hardware installed in the system
+   - The kernel modules (drivers) loaded to support the physical NIC
+   - The IP networking configuration parameters assigned to the interface

To install an Ethernet network interface in your system, you need to complete the following tasks:

+   - Installing the Ethernet board
+   - Configuring IP parameters
+   - Configuring routing parameters
+   - Configuring name resolver settings

Let’s begin by discussing how to install an Ethernet board in your system.