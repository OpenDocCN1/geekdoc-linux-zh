Switching between bridged networking and host-only networking can be done on-line, when your virtual machines are up and running.

You can either select VM → Settings from the menu and then configure the networking option, or you can double click the network adapter icon on the right lower corner of your virtual machine. This will also bring up the networking control panel.

If you need advanced configuration options and tips on networking, go to section 11: “Networking configurations”

![](bbox=[0.48, 0.09, 0.92, 0.62])

Figure 2.4: The networking configuration can be modified when a machine is on-line.

Tip: I have met a lot of people who have problems with accessing virtual machines and the LAN when they start configuring their physical and virtual adapters. It is very important to make sure that all adapters (physical, including wireless, host-only VMnet1 and VMnet8) are in different IP subnets. A real PC with two network adapters on different Ethernet segments, but with the same IP subnet used on both LANs will not know where to send its packets.

Compare it to a junction with two signs pointing to Paris. You would also be confused as to what direction to choose (unless they both point to Rome, of course, since we know that all roads lead to Rome!).

A PC with a physical adapter and or more virtual adapters that have been configured for the same subnet will have the same problem and will prevent you from accessing hosts on either the physical or virtual networks.

# 2.8 Virtual Machine Hardware Specifications

A great advantage of virtual machines is that they always provide you with the same hardware. Independent of the hardware in the host system, the hardware inside the virtual machine stays the same. The only component that will be different is the processor, since the virtual machine will work with the underlying