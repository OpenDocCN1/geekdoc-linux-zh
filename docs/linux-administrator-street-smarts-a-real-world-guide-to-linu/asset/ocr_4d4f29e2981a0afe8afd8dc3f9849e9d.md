features, though, and some of them offer configuration options that you might want to adjust. To do so, you must access the appropriate BIOS utility screen. In the case of the BIOS depicted in Figure 2.1, you should select the Integrated Peripherals menu. The result is the screen shown in Figure 2.3, in which you can enable or disable the floppy disk (FDC Function), RS-232 serial ports, parallel ports, and more. (This area's options won't fit on one screen; they continue as you move the cursor down the list.)

# FIGURE 2.3 Modern BIOSs enable you to disable on-board devices if you so desire.

![](bbox=[0.2, 0.28, 0.72, 0.54])

Disabling on-board devices disconnects them electronically from the rest of the motherboard. The result is that Linux won't be able to use those devices. The advantage is that they also won't consume valuable interrupt request (IRQ) lines and other resources.

![](bbox=[0.14, 0.65, 0.2, 0.7])

> If you know you won't be using a hardware feature built into your motherboard, either because you don't need it at all or because you intend to use a better plug-in card for that function, disable the feature in the BIOS. This reduces the odds of your encountering IRQ conflicts or other problems related to an unused device consuming resources or otherwise interfering with the hardware you are using.

# Additional BIOS Options

Most BIOSs provide options I don't describe here. Power management, RAM and PCI bus timing options, CPU speed, and more can all be controlled from the BIOS. Most such options are of interest to those who want to tweak the best possible performance from their computers, sometimes at the cost of reliability. If in doubt, leave the options at their factory defaults. Some BIOSs, including the one depicted in Figure 2.1, provide an explicit option to reset the configuration to the factory default (Load BIOS Setup Defaults in Figure 2.1) or to a high-performance state (Load High Performance Defaults in Figure 2.1). Such options can be useful