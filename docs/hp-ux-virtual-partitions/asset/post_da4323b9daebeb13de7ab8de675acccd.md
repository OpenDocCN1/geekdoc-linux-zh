
# Figure 5-1 CPU Report in GlancePlus Showing Two Processors

![](img/eff8b9287a5f38c5adf538f24aacf29e_355_0.png)

The screen in Figure 5-1 confirms that we have two processors devoted to *cable1* (hostname *cvhdcn3*) by the (200% max) shown for *CPU Util* rather than the four (which would have read 400%) that are in the systems. You can also run *top* to confirm the two processors in *cable1*, as shown in Figure 5-2:

# Figure 5-2 top Screen Shot Showing Two Processors in cable1

![](img/eff8b9287a5f38c5adf538f24aacf29e_356_0.png)

top clearly shows two CPUs devoted to cable1 (CPU 0 and 1 in Figure 5-2.)

## Virtual Partitions and Memory

When assigning memory in Chapter 2, you use size. You can also specify base address and range as subset of size just as hopath is a subset of min and num for CPUs. We choose to use the size. Table 5-1 shows the options related to assigning and changing memory. The first activity we have to perform is to find the amount of memory on a system so that we can assign portions of it to vPars. There are a variety of ways to determine the amount of memory on your system. The following shows only the memory-related output of the dmesg command when booting standard HP-UX in non-vPars mode:

```
# dmesg

Memory Information:
  MBD / - cal page size = 4096 bytes, logical page size = 4096 bytes
  Physical: 4194304 Kbytes, lockable: 3180924 Kbytes, available: 3655192 Kbytes
```

This listing shows a *Physical* memory of 4GBytes. You could also run GlancePlus and select the *Memory* screen.

Memory can easily be specified for a vPar with *m::size*, where *size* is in MBytes. To specify 2 GBytes in a virtual partition, you would use the option *m::2048*.

After assigning memory to vPars you’ll want to confirm that indeed each vPar has in it the amount of memory you specified. You can verify this in a variety of ways. The first is by issuing **dmesg** when booting Virtual Partitions. The Virtual Partitions Monitor boots only the devices you have specified as part of a Virtual Partition. The following example shows only the memory-related output of **dmesg** for *cable1*:

```
# Memory Information:
cvhcon3:/ # page size = 4096 bytes, logical page size = 4096 bytes
  Physical: 2096128 Kbytes, lockable: 1576748 Kbytes, available: 1815620 Kbytes
```

Notice that this output shows 2 GBytes of RAM for *cable1*, as was specified when the *vPar cable1* was created. This is different from the example in Chapter 2, where *cable1* had one GByte of RAM. This is an indicator of how low-level vPars work, in that resources were assigned to *cable1* at the time of boot, ensuring that only the specified resources were assigned to the vPar.

We can also view memory-related information by running GlancePlus and selecting the *memory* screen. The following screen shot shows the total memory of the system when booting standard HP-UX and not Virtual Partitions as we have done in Figure 5-3:

# Figure 5-3 Phys Mem in GlancePlus Showing 4 GBytes for System (non-vPars)

![](img/eff8b9287a5f38c5adf538f24aacf29e_358_0.png)

Now let's view the memory for cable1 (hostname cvhdcn3) in GlancePlus. Figure 5-4 was obtained when the system loaded cable1 at boot time:

![](img/eff8b9287a5f38c5adf538f24aacf29e_359_0.png)

The Phys Mem in the bottom right-hand side of the screen is shown as 2 GBytes, as we had assigned for cable1. This confirms the 4 GBytes for the system and 2 GBytes for cable1 shown with dmesg.

Because you have multiple Virtual Partitions running, you have to have multiple HP-UX kernels running. The kernel for a specific Virtual Partition has to be located within the memory range devoted to that Virtual Partition. The location of the kernel in memory is specified in the /usr/con/cfg/map-file file in HP-UX 11i. Among the entries in this file is the location in memory at which the kernel will be located. This line begins with Text = LOAD. This file exists on every file system for which you have a Virtual Partition and contains the kernel location for the respective Virtual Partition as well as other dynamic information. This file exists on HP-UX 11i for non-Virtual Partition systems as well and contains other information used by 11i. Working with the HP-UX 11i kernel and Virtual Partitions is covered in Chapter 4.

## Virtual Partitions and LAN

The LAN cards on your system are also easy to identify with **ioscan**. To see only the listing of LAN cards on a system, we would issue the following command:

```
# ioscan -f | grep lan
lan   0  0/0/0/0        btl an5   CLAIMED   INTERFACE   PCI Ethernet (10110019)
      ~ 1                btl an5   CLAIMED   INTERFACE   PCI A5230A/B5559BA
                                  PCI 10/100Base-TX Addon
lan   3  0/5/0/4/0      btl an   CLAIMED   INTERFACE   PCI 10/100Base-TX 4 port
lan   4  0/5/0/5/0      btl an   CLAIMED   INTERFACE   HP A5506B
                                  PCI 10/100Base-TX 4 port
lan   5  0/5/0/6/0      btl an   CLAIMED   INTERFACE   HP A5506B
                                  PCI 10/100Base-TX 4 port
lan   6  0/5/0/7/0      btl an   CLAIMED   INTERFACE   HP A5506B
                                  PCI 10/100Base-TX 4 port
lan   2  1/2/0/0        btl an5   CLAIMED   INTERFACE   PCI A5230A/B5559BA
                                  PCI 10/100Base-TX Addon
#
```

This system has seven LAN interfaces. It has the built-in LAN interface, two add-on LAN cards, and a four-port card. Although this system was not used in our earlier example, I wanted to show a listing of a system with a variety of LAN interfaces present.

Going back to our earlier example, our system has three LAN interfaces as shown in the following **ioscan** listing:

```
cvhdcn3:/ # ioscan -f | grep lan
lan   0  0/0/0/0        btl an   CLAIMED   INTERFACE   HP PCI 10/100Base-TX Core
lan   1  0/10/0/0       btl an   CLAIMED   INTERFACE   HP AS230A/B5509BA PCI 10/100Base-TX Addon
lan   2  0/12/0/0       btl an   CLAIMED   INTERFACE   HP AS230A/B5509BA PCI 10/100Base-TX Addon
cvhdcn3:/> #
```

The LAN card at 0/0 has been assigned to *cable1*, and the card at 0/10 has been assigned to *cable2*, as shown in the following **vparstatus -v** listing:

```
# vparstatus -v

[Virtual Partition Details]
Name:     cable1
State:    Up
Attributes: Dynamic,Manual
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_360_0.png)

```
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/3
Bound by User [Path]:
Bound by Monitor [Path]: 33
Unbound [Path]:

[IO Details]
0.0 <-- cable1 LAN on 0/0 but not shown
0.0.1.1.2.0 BOOT

[Memory Details]
Specified [Base /Range]:
      (bytes) (MB)
Total Memory (MB): 1024

[Virtual Partition Details]
Name:     cable2
State:    Up
Attributes: Dynamic,Manual
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/3
Bound by User [Path]:
Bound by Monitor [Path]: 37
Unbound [Path]:

[IO Details]
0.8,0.0,0.8,0.5,0.0.0, BOOT
0.10 <-- cable2 LAN

[Memory Details]
Specified [Base /Range]:
      (bytes) (MB)
Total Memory (MB): 1024
# 
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_361_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_361_1.png)

The LAN interface on the Core I/O card at *0/0/0/0* is not called out explicitly in the **vparstatus** output. The console at *0/0/4/0* is also an implied component of this vPar. Both of these components are part of the Core I/O card that we specified as part of *cable1* with the *-a* *0/0/0/0* argument to the **vpareccreate** command.

The unassigned LAN interface can be added to *cable1* or *cable2* with the **vparmodify** command. At the time of this writing, however, I/O components can't be added dynamically, and the vPar would have to be *down* in order to add LAN or any other I/O component. You can, however, use Online Replacement and Addition (OLAR) of components in vPars. If you had, for instance, assigned an I/O path to a vPar and then you physically add a component to that I/O slot then it is part of the vPar.

## Virtual Partitions and the Console

You can set up a dedicated physical console for each virtual partition. This would mean allocating a serial port for each of your virtual partitions. Alternatively, your virtual partitions can use virtual consoles. The Virtual CoNsole driver, vcn, handles I/O related to the virtual consoles. As shown in Figure 5-5, vcn communicates with the Virtual Partitions Monitor. The Virtual Partitions Monitor buffers I/O related to virtual consoles until it can be handled by the Virtual Console Slave (vcs). All vPars use Virtual Consoles and the physical console is assigned to one of the vPars as part of the I/O specification.
