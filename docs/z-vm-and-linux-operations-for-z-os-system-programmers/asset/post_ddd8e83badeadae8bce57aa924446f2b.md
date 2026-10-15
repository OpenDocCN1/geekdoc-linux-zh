
Because each virtual machine has its own equipment and each must have addressability, the same default device addresses and device types are assigned to each machine, as follows:

- Address 0009 is a 3215 console
- Address 000C is a 2540 reader
- Address 000D is a 2540 punch
- Address 000E is a 1403 printer

Along with the I/O devices, each machine must have central processors and memory to run programs and storage to save data. Processors (virtual CPUs), memory (virtual storage), and disks (minidisks) complete the components required for each virtual machine.

As we log on to a z/VM user ID (our unique machine identifier) and enter our password (our secure location), we are actually initiating the process of starting a computer system. We first make contact with the CP where we are given the required hardware to run our system. Next, as we bring up our system, such as CMS, Linux, z/OS, or another z/VM system, we do an initial program load (IPL) of a system that already resides on disk. We might spool input to our punch, reader, or spool output to our printer or console.

Over the years, IBM assumed this development effort. Work on VM continued as IBM announced newer processors such as system/360 and system/370, but was not seen as a system that customers would widely use. As the base system/370 operating system, MVS™ continued its development efforts. Because few processor prototypes were available, the realization was that VM provided a necessary processor simulation platform for the MVS developers. VM became a popular system among many customers who found the ease of programming and versatility of the system beneficial to their businesses.

By the 1980s, VM installations grew and more business processes and applications were being developed to run on VM. Customer popularity brought about enhanced programming products for VM such as REXX™ and Pipelines, which has since been ported to other operating systems. As new IBM processors and architectures were developed, VM kept pace with new functions to exploit the features.

With the advent of other technologies and systems, z/VM was becoming less of a front-end direct-user interface and more of an IBM virtualization technology platform. Now, with the popularity of Linux and the recognition of z/VM virtualization capabilities, it has again demonstrated its place in the System z operating system portfolio.

As with early computers, z/VM has evolved from its early roots and now provides many more functions and services, although the underlying principles of the virtual machine has not significantly changed.

Figure 2-2 shows a timeline of how z/VM has evolved to today's version.

![](img/b0a4b9056f819dccd4781a5105c92d45_31_0.png)

Figure 2-2 History of z/VM

## 2.2.2 About z/VM

z/VM provides each user with an individual working environment known as a virtual machine. The virtual machine simulates the existence of a dedicated real machine, including processor functions, memory, networking, and input/output (I/O) resources. Operating systems and application programs can run in virtual machines on the second level as guest. For example, you can run multiple Linux and z/OS images on the same z/VM system each on their own virtual machine.

As a result, development, testing, and production environments can run side by side sharing the same resources.

A virtual machine can use its own real hardware resources (for example, a tape drive); however, for the most part it shares from a pool of virtual hardware managed by z/VM. The virtual address of these devices might or might not be the same as the real address of the actual device. Therefore, a virtual machine only knows virtual hardware that exists or does not exist in the real world.

## 2.2.3 First-level versus second-level guest system

A first-level z/VM means that it is the base operating system that is installed directly on top of the real hardware. A second-level system is a user brought up in z/VM where an OS can be executed upon the first-level z/VM.

In other words, a first-level z/VM operating system sits directly on the hardware, but the guests of this first-level z/VM system are virtualized; see Figure 2-3 on page 18. By virtualizing the hardware from the first-level, we are able to create and use as many guests as needed with a small amount of actual real hardware.

Operating systems running in these virtual machines are often called guests. Other phrases you might encounter include:

- Running first level, which means running directly on the hardware (this is what a base z/VM does).
- Running second level, running under z/VM, or running on (top of) z/VM, which mean running as a guest on the second-level.
