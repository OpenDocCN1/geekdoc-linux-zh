
[content]

## Using Virtual Machines and Emulators

Virtualization is the logical separation of the request for the physical resources that actually provide that service, and is also one of today's hottest IT topics. The primary reasons for the popularity of virtualization today are the increasing speed and capabilities of today's off-shelf processors, falling hardware prices, and the ubiquity of networks that offer the capability to connect almost anything to anything else. These combine to provide higher-performance and higher-capability systems at a lower cost, providing plenty of CPU cycles and processor capabilities to handle any extra layer of abstraction that virtualization might introduce.

| IN THIS CHAPTER |
| :--- |
| Introducing virtualization |
| Using VirtualBox |
| Using KVM |
| Using QEMU |

The loudest virtualization-related buzz surrounds different approaches to two topics, namely, virtual storage and virtual machines:

- Virtual storage: Virtual storage, as the name suggests, prevents users and system administrators from knowing the physical devices upon which their data is stored because you access that through logical device, disk, or volume names. The physical hardware that supports these logical or virtual disks can be located on separate disk devices, storage devices, or even on physically distinct computer systems. Common virtual storage mechanisms such as logical volumes were introduced in Chapter 4, "Basic Linux System Concepts."
- Virtual machines: Virtual machines enable multiple complete operating systems to run simultaneously on the same physical computing hardware. Virtual machines must use the same instruction set as the system on which the virtual machines are running (which is typically referred to as the *host system*). In other words, you can only run x86-based operating systems on a machine with an x86-compatible processor. Virtual machines are often confused with *emulators*, which do approximately the same thing, but enable a single computer system to run operating systems and applications that require different processors and instruction sets by *emulating* those processors. Emulators are compiled for the instruction set of the machine on which they are running, but simulate an entire physical execution environment including the hardware subsystems. Emulators running on x86-based systems can therefore run operating systems and applications that are compiled for either x86-based systems or for systems that use other types of processors, such as ARM, MIPS, PowerPC, and SPARC processors.

This chapter provides an introduction to different types of virtual machine technologies and discusses the different types of virtual machines and emulators that are available for Ubuntu systems, usually as packages in the Ubuntu repositories.

## Note

As mentioned previously, *virtualization* is a hot buzzword. To get as much software as possible on the bandwagon, you'll often hear remote desktop connection technologies like VNC and RDP, discussed in Chapter 25, “Connecting to Other Systems,” referred to as *desktop virtualization* technologies because they provide the ability to display a graphical desktop system from one computer system on another computer system or smart display device. ■

## Overview of Virtualization and Emulation

As discussed in the introduction to this chapter, virtualization is a hot term in computing today. The next sections explore the reasons to consider virtualization (using it as *resume fodder* (which is not discussed)), and the different types of virtual machines that are in use today (and of which these are available as packages for Ubuntu systems), and make some recommendations on which virtual machine technology to adopt based on what you want to accomplish.

## Why Virtualize?

The most obvious reason for wanting to run a virtual machine is so that you can run multiple operating systems at the same time on a single physical computer system. For example, suppose that you want to run Linux but occasionally need to run Microsoft Word. You can configure your system to dual-boot so that you can run either Linux or Windows, but that isn't very useful if you depend on your Linux system to read mail, browse the Web, and so on. Because you can only run one operating system at a time, dual-booting can be time-consuming and irritating. You could also run some Windows programs using WINE on your Linux system — WINE is a Linux-based Windows API that supports Windows applications. However, you might encounter problems with WINE, and then what can you do?

Assuming that you have sufficient disk space, installing Windows as a virtual machine is probably your most convenient, robust, and long-term solution. Why waste hardware on Windows? Able to run Windows while running Linux will enable you to use the Linux applications you prefer while still being able to work on Microsoft Word documents that may have Windows-specific features (such as Extensive Virtual Basic macros, etc.).

Virtualization is more popular now than ever, for many reasons. Some of the most important reasons are the following:

- The power and performance of commodity x86 hardware continue to increase. Processors are faster than ever and more memory than ever, and the latest multi-core processors literally enable single systems to perform multiple tasks simultaneously. Most modern systems can easily run any primary operating system and at least one virtual machine without taking a significant performance hit.
- The integration of direct support for hardware-level virtualization in the latest generation of Intel and AMD processors, motherboards, and related firmware makes virtualization on commodity hardware both easier and more powerful than ever before.
- A wide variety of virtualization products for both desktop and server systems running on commodity x86 hardware are available for free and are easily installed on your Ubuntu systems.

In general, there are some common cases in which virtual machines are used:

- Dependency on a specific piece of software (described at the beginning of this section), where you need to use a software product that only runs (or runs best) on another operating system
- Running legacy software, where you depend on a software product that only runs on another operating system
- Software test and quality assurance environments, where you need to be able to test many operating systems
- Low-level development environments, where developers may want to work with different versions of operating system

Virtualization is not a new concept and has been in use for years. However, for the reasons discussed in this section, virtualization is both more available and easier to run than ever before.

The next section highlights different approaches to virtualization and details which of these are available for Ubuntu systems.

## Types of Virtual Machines

Virtual machines can work in many ways. The differences between these approaches can be subtle, but are always significant in terms of the capabilities they provide and the hardware requirements. The most common approaches today are the following:

- Guest OS: Virtual server runs as a separate operating system within a virtualization application that itself runs on the hardware. Parallels Workstation, VirtualBox, VMware Workstation, and VMware GSX are the most common examples of this approach. The Ubuntu repositories include packages for the open source version of VirtualBox and also include the packages for VMware which is free for individual use. A free version of VMware Server, VMware Player, and ESXi are all available for free download from the VMware site.
- System-level or operating system virtualization: Multiple, distinct environments are running on a single instance of operating kernel. System-level virtualization is based on the change root (chroot) concept that is available on all modern UNIX-like systems, and gives each virtual machine a portion of the parent system's filesystem as the root filesystem for the virtual machine, as well as its own set of processes that execute relative to that filesystem. Linux virtualization solutions such as FreeVPS, Linux Server, OpenVZ, and Virtuoso are all examples of system-level virtualization. The kernel and user-space administrative utilities are provided in the Ubuntu repositories.
- Parallel virtual machine: Some physical or virtual systems are organized into a single virtual machine using clustering software such as PVM. The resulting cluster is capable of performing complex CPU and data-intensive calculations in a cooperative fashion. The PVM packages are available from the Ubuntu repositories, but are not discussed in detail in this chapter because clustering is an advanced, specialized technology.
- Paravirtualization: Drivers in the virtual machines are modified so that they know they are running in a virtual machine environment and optimize device access for that. This can significantly reduce overhead and increase disk and network I/O. Paravirtualization is typically used in virtualization environments that also use a virtual machine monitor (known as a hypervisor), which runs on top of your machine's hardware, manages protected or privileged CPU operations that are requested by any virtual machine, and manages the hardware access requests that are made by any virtual machine. The most popular examples of hypervisor-based virtualization in use today are Citrix Xen, Microsoft's Hyper-V, and VMware's ESXi.

