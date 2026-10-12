# ### 10.1.1 IPL phase

Initial Program Loader (IPL) is a mainframe term for the loading of the operating system into the computer's main memory. IPL is to mainframe as boot is for other architectures. See Figure 10-2.

![](bbox=[0.26, 0.2, 0.72, 0.67])

The IPL phase consists of reading the boot loader code from the operator-specified device into memory and starting boot loader (zIPL).

DASD, SCSI disk, tape, and VM reader can be used as IPL devices.

# ### 10.1.2 Boot loader phase

The main boot loader function is to load other software for the operating system to start. It is found at the start of the IPL device. The boot loader used for IBM S/390 and zSeries machines is called zIPL. Boot loader code is made by the