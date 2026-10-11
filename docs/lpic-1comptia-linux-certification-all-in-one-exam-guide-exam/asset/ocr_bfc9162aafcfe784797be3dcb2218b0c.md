troubleshooting issues can be traced back to incorrect master/slave settings with IDE drives and termination/ID settings with SCSI drives. I also pointed out how to manipulate the hardware ID assigned to storage devices to configure the boot device. I also discussed how optical and flash memory storage devices work.

I then reviewed removable hardware interfaces that are used to connect external devices to a PC. We first looked at USB. I noted that USB uses hubs to create a cascaded star topology that can connect up to 127 external devices. I then reviewed how IEEE 1394 accomplishes a similar task using a daisy-chained bus topology. I finished by reviewing the PCMCIA standard that is used to create credit card-sized expansion boards for notebook PC systems.

We then looked at managing system resources. I reviewed the role and function of interrupts, I/O addresses, and DMA channels. I also reviewed how the PnP system works, emphasizing that PCI expansion cards use PnP and can be configured to share interrupt channels.

We then turned our attention to managing integrated devices. I pointed out that you can enable or disable integrated devices using the CMOS Setup program in your system's BIOS. I pointed out that the keystroke used to access the Setup program as well as the exact menu option used to enable or disable integrated devices varies by manufacturer.

We then looked at managing systems that don't have any external peripherals installed, including keyboards or video displays. These types of systems can be managed using either VNC or SSH, with SSH being the more secure option of the two.

Next, you learned how to manage and configure drivers to enable the hardware in your Linux system. I related that drivers are small programs that are loaded into RAM that enable the CPU to communicate with a particular hardware component. For basic components, this software is provided by the BIOS. For other components, the driver is stored on the hard disk and must be loaded into RAM by the operating system kernel. On Linux, drivers can be loaded in two ways. First, they can be loaded as kernel modules after the operating system has started. Second, they can be compiled directly into the kernel itself. I related that, as a general rule of thumb, only drivers needed to boot the system should be compiled directly into the kernel. Drivers for other hardware should be loaded as kernel modules. This will keep your kernel lean and trim.

I then reviewed some of the tools you can use to view information about the hardware in your Linux system. Within the /proc directory, you can view hardware information in the following files and directories:

+   - cpuinfo
+   - devices
+   - dma
+   - interrupt
+   - iomem
+   - modules
+   - version
+   - /scsi/