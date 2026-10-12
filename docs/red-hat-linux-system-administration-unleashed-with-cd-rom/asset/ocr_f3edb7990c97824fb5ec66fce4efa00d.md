One of the required features of any modern operating system to allow it to be used as a server is support for Redundant Arrays of Inexpensive Disks, or RAID. Red Hat Linux is no exception to this and RAID is supported under Linux via both software and hardware.

This chapter begins with an overview of RAID concepts. It then describes Linux software RAID, including coverage of the RAID tools and a section on using RAID on your root filesystem. Finally, it presents information regarding Linux support for hardware RAID controllers, including the configuration options required to add support for them to your kernel.

# The History of Linux RAID Support

Support for software RAID was first incorporated into the Linux kernel in February, 1996 with the release of kernel version 1.3.69. This support was written by Marc Zyngier and at that time, the support was limited to linear mode md devices (commonly referred to as concatenated drives) and RAID level 0, or striping. Work to support additional levels of software RAID began shortly thereafter by Gadi Oxman, Ingo Molnar, Miguel de Icaza, and others, and in November, 1997, support for RAID levels 1, 4, and 5 were added to the 2.1.63 development kernel release. This support was finally backported to the 2.0.x stable release tree in July, 1998 when it was added to the 2.0.35 kernel release. Linux also supports hardware RAID in the form of support for RAID controllers and support for RAID devices that connect to a SCSI or IDE controller or even to the parallel port.

# RAID Overview

Before discussing the details of Linux software and hardware RAID, it is essential to understand what RAID is, and why you would want to use it. RAID was first described in a paper titled “Case for Redundant Arrays of Inexpensive Disks (RAID),” published by Patterson, Garth, and Katz of The University of California at Berkeley in 1987. Since its introduction, RAID has been implemented in both hardware and software, or a combination of the two. There were three major objectives for RAID as described in the 1987 RAID paper. These were reduced cost for data storage, increased performance, and increased reliability. Let’s examine each of these objectives and how they are achieved through RAID.

# Objectives of RAID

The first objective was reduced cost for large amounts of storage space. It is important to remember that at the time the 1987 RAID paper was written, large filesystems were usually implemented using single, large and expensive disks (SLEDs) that were proprietary to each hardware manufacturer. By comparison, you could purchase an equivalent amount of