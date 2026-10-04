# Attacking and Defending Windows 2000 • Chapter 5

the necessary interfaces for operating system functions such as network services and security. The Environment Subsystems include services that interface with application program interfaces (APIs) providing interoperability with applications written for other operating systems, such as POSIX, Win32, and OS/2. Generally, applications running in user mode that fail or crash will affect only the operation of that individual application, rather than affecting the operation of the Windows 2000 operating system.

# Figure 5.1 Windows 2000 Kernel Architecture

![](bbox=[0.142, 0.276, 0.858, 0.623])

Kernel mode allows software to access important system information and hardware directly. This mode consists of some specific architectural areas, which are divided into these four large areas:

+   - Executive
- Microkernel
- Device drivers
- Hardware Abstraction Layer (HAL)

The executive area is composed of system components that have a responsibility to provide services to other executive components and to the environment

www.synergy.com