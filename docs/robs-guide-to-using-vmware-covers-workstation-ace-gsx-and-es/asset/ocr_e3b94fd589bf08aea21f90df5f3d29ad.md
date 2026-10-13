# On a Linux host

To modify the networking configuration for your VMware environment on a Linux host, you must run the vmware-config.pl script. This script will run through the same wizard-like questions that you have seen during your initial VMware Workstation configuration. The script allows you to configure bridged networking, host-only networking, and NAT.

# Setting up a virtual machine with two host-only adapters

If you are going to create the setup where the guest operating system (virtual machine 3 in Figure 11.13) takes care of the routing, you must set up that machine with two virtual host-only network adapters.

> Tip: In your guest operating system, rename the network adapter (Windows) or identify the adapter by its configuration to be able to distinguish between this already existing adapter and the new adapter that you will be adding here.

Open the configuration of your virtual machine VM → Settings. Click Add to add a new Ethernet Adapter to your virtual machine.

![](bbox=[0.08, 0.58, 0.95, 0.85])

Figure 11.16: Adding a second network adapter to a virtual machine.