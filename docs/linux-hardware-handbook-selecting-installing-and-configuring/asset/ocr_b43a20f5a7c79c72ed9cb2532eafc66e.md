# NOTE

You can often connect more than one device to a parallel or RS-232 serial port by using a *switch box*. This box enables you to safely and quickly direct the port's traffic to and from one of two or more devices by pushing a button or turning a dial. Some switches can work the other way: you can use them to connect one printer to two or more computers. Today, this latter task is generally handled by networking the computers and enabling printer-sharing protocols, but a switch box can still sometimes be a useful tool.

USB support is a very recent addition to the Linux kernel. Only in the 2.2.x kernel series was USB support officially added, and it’s still very primitive even late in the 2.2.x kernel series. The 2.3.x development kernels include much more extensive USB support, as described later in this chapter.

# Parallel Port Devices

Through the 2.0.x kernels, the assumption in Linux was that parallel ports were used to interface with printers. As such, there was but a single parallel port driver. With the increasing popularity of parallel-port devices such as Zip drives, scanners, and WebCams, it became desirable to break the parallel port driver into two parts: a low-level parallel port driver and a higher-level driver to handle the needs of specific devices. In the 2.2.x kernel, therefore, there are several parallel port kernel options, including

+   - **General setup, Parallel port support** This option is the core parallel port support. You must enable it (using either the *Y* or *M* option) to use any parallel port device. Enabling this feature is not sufficient to use a parallel port device, however. This option also has a couple of suboptions relating to the types of parallel-port hardware supported. For x86 systems, the *PC-style hardware* option is what you want to use.

+   - **Block devices, Parallel port IDE device support** Enable this option, and whatever suboptions are appropriate, to use most disk-like devices that connect to the parallel port. I describe the details in the chapters devoted to each of these devices.

+   - **SCSI support, SCSI low-level drivers, IOMEGA parallel port** There are actually two variants of this option for different varieties of Iomega Zip drive. You must also enable basic SCSI support to use these drives.

+   - **Character devices, Parallel printer support** This is the option you enable to use printers that connect to the parallel port.

+   - **Character devices, Video for Linux** Some drivers on this menu relate to parallel-interfaced WebCams.