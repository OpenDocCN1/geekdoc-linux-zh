
- Upgrading from Windows 95, Windows 98, or Windows NT 4.0.
- Booting from the Windows 2000 CD-ROM.
- Booting from the Windows 2000 boot floppies.

The easiest way to begin the installation is to boot from the Windows 2000 CD-ROM. After Windows 2000 has started for the first time, you will need to configure the TCP/IP network setting.

## SYSTEM BOOT AND SHUTDOWN

## UNIX

- BSD Startup
- rc Scripts in BSD
- SysV Startup
- SysV Startup Script Structure
- Shutdown, Reboot, and Halt

## WINDOWS 2000

- Booting Windows 2000
- System vs. Boot Partition
- Advanced Boot Options
- boot.ini
- System Shutdown

For most people, the simple act of flipping on the power is the whole boot process. In this chapter, we will take you through the steps performed by the system while you are waiting for the login screen. We call this process "booting" (short for bootstrapping) the system.

The booting sequence involves both hardware and software components. Understanding this process is essential to a system administrator. There are very few things in this field more frustrating than a system that will not boot, often for no apparent reason, and usually in the presence of a user. Knowledge of these steps (from powering up the system to getting a login) is essential to properly diagnose and correct problems that occur when the system is most vulnerable.

## The Physical Boot Sequence

Booting a computer system is somewhat similar to waking up in the morning. Once the alarm goes off, a small, although not necessarily functional part of our subconsciousness acknowledges the signal and begins the process of loading the rest of our conscious faculties. At some point, we perform a physical inventory; we stretch and begin to move.

Likewise, when you power on traditional UNIX hardware, a physical component called firmware instructs the system to access a section of the disk drive known as the boot block. The boot block provides basic instructions for loading the operating system. One important piece of information is the location of the secondary boot file, called ufsboot in some systems. The secondary boot file handles the loading of the kernel into the system memory. The kernel is the core of the UNIX operating system. Once it is loaded, the system is a UNIX system and the process of waking up begins. Figure 3.1 shows the physical boot sequence for a traditional UNIX system.

The boot sequence of a PC is very similar. Instead of the firmware, we have the BIOS (Basic Input Output System; same thing as firmware, different name). The BIOS performs a basic system diagnostic, gathering information about the system architecture. The BIOS will provide information on the CPU, memory, and hardware. Then, based on how your system is configured, the BIOS will launch either a boot manager or the actual operating

![](img/415c89a1ede71e11e5040a0038b6916c_97_0.png)

![](img/415c89a1ede71e11e5040a0038b6916c_98_0.png)

Figure 3.2
Physical boot sequence—PC.

system for the system. In Figure 3.2, you can see the similarity between the UNIX and PC physical boot sequence.

Whereas the UNIX firmware and boot block are completely vendor-dependent, the PC world has standardized on a few BIOS configurations. Linux and other PC-based UNIX operating systems follow the PC boot sequence using the boot manager to load the kernel.

## Loading the Operating System

A computer without an operating system is like a human without a brain. The operating system provides the fundamental communications between the software and hardware components. The operating system is itself software, but it serves as the mediator between other applications and the physical layer. UNIX and NT use different approaches in this process of obtaining a higher level of consciousness.

Once the UNIX kernel is loaded, the ability to become conscious is there, but it is not entirely awake. A UNIX system can be brought up in two main operating modes, commonly called single-user and multi-user. Single-user mode is a state in which many but not all of the system functions are alive. This state is used primarily for administrative purposes, allowing a system administrator to perform corrective functions on disks or startup scripts.
