# Task 6.4: Configure Routing

Preceding tasks have referred to routing as something that other computers do—you configure your computer to know about a router on your local network, or you use `traceroute` to determine the path (through routers) a packet takes between your computer and another one. Linux, however, can be a router. To configure Linux as a router, you must install two network interfaces in the computer and issue a few commands. This task guides you through the process of configuring your system in this way.

# Scenario

A small business has a LAN that's linked to the Internet via a broadband connection using a dedicated broadband router. This business wants to support wireless connections for its employees' laptop computers, providing those computers with access to the LAN's local servers and to the Internet at large, as illustrated by Figure 6.2. To this end, the business has hired you to configure an old computer as a dedicated router between its Ethernet LAN and its wireless network. The computer is already set up with both Ethernet and wireless hardware, and Linux is installed on the system and can “talk” to machines using both the Ethernet and wireless hardware. Your task is to configure the computer as a router.

# **FIGURE 6.2** A router links two or more networks, which can have different types of network hardware.

![](bbox=[0.1, 0.53, 0.9, 0.92])