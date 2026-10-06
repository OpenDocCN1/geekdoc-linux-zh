these messages reset the interface into the blocking state. The next state allows the bridge to enter addresses in the forwarding table (learning function); this state is called the learning state. In the forwarding state, which is reached after another expiry of the forward delay timer, data packets can be forwarded. Figure 12–10 shows the transitions of a network adapter.

# 12.3 Configuring a Bridge in Linux

# 12.3 CONFIGURING A BRIDGE IN LINUX

A bridge interconnects several local area networks on the data-link layer, simulating the behavior of one large network to the outside. To connect several local area networks in a Linux system, we need only install several network adapters. Linux also allows you to manage several bridges within one system, which can operate independently of another. Each bridge has a logical name. One network adapter can always belong to exactly one bridge. This allows the system administrator to build virtual local networks (VLANs), which previously expensive VLAN switches.

The following sections introduce options to configure and control Linux bridges.

# 12.3.1 Configuring the Kernel and the Network Adapter

To be able to use a Linux system as a bridge, the Linux kernel has to contain the bridge functionality. This is normally not the case, so we have to create a new kernel. When configuring the kernel, you should select the BRIDGEING option from the Networking Options. You can integrate it into the kernel either as a module or permanently.

Once you have booted your kernel (and loaded the module, if applicable), you can use the bridge functionality. Sometimes, you might incur problems trying to activate several network adapters. If this happens, you can specify the boot parameters linux ether=0,0,eth for each card when you start the system. If you use the LILO boot loader, you can also have the boot parameter passed automatically.

If the bridge functionality resides in the loaded kernel and all network adapters are activated, you can use the brctl tool to create and configure the desired bridge instances. brctl will be introduced in the next section.

# 12.3.2 Using the brctl Tool to Configure Linux Bridges

You can use the brctl (Bridge Control) tool to configure a bridge in Linux. This tool is part of the bridge-utils package and can be obtained from [Buy01].

This tool can be used by the administrator to pass commands to the bridge implementation in the kernel using brctl() commands. This section gives an overview of how you can use this program. [BoBu01] includes a detailed description of these commands and several examples.

The brctl lets you use the following commands to activate and deactivate a bridge. The commands are passed as parameters when brctl is called:

```
addbr bridge: This command creates a new instance of a bridge with the identifier bridge.
addif bridge device: This command adds the network adapter device to bridge. A network adapter can always belong to one bridge only.
```