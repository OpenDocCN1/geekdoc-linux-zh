5. Creating a protected environment: If a guest OS running on a VM becomes damaged in a way that is difficult to repair, such as may occur when testing, the VM can be discarded without harm to the host system, and a clean copy used next time.

Primary contemporary virtualization techniques:

Full virtualization: In full virtualization, the VM simulates enough hardware to allow a complete "guest" OS, one designed for the same processor instruction set architecture (ISA) to be run in isolation.

Examples for UNIX systems running on X86 ISAs include VirtualBox, Parallels Workstation, Oracle VM, Virtual Server, Hyper-V, VMware Workstation, and VMware.

Hardware-assisted virtualization: In hardware-assisted virtualization, the hardware provides architectural support that facilitates building a VMM and allows guest OSs to be run in isolation. In 2005 and 2006, Intel and AMD provided additional hardware to support virtualization. Sun Microsystems added similar features in their UltraSPARC processors in 2005. Examples of virtualization platforms adapted to such hardware include KVM, VMware Workstation, VMware Fusion, Hyper-V, Xen, Oracle VM server for SPARC, and VirtualBox.

Partial virtualization: In partial virtualization, including address space virtualization, the VM simulates multiple instances of much of an underlying hardware environment, particularly address spaces.

Paravirtualization: In paravirtualization, the VM does not necessarily simulate hardware, but instead (or in addition) offers a special application programmer's interface (API) that can only be used by modifying the "guest" OS. For this to be possible, the "guest" OS's source code must be available.

OS-level virtualization: In OS-level virtualization, a physical server is virtualized at the OS level, enabling multiple isolated and secure virtualized servers to run on a single physical server. The "guest" OS environments share the same running instance of the OS as the host system. Thus, the same OS kernel is also used to implement the "guest" environments, and applications running in a given "guest" environment view it as a stand-alone system. Examples in UNIX are FreeBSD jails, iocage in PC-BSD, and other examples include Solaris zones. In LINUX, examples include LXC, and its derivative management system Docker.

In this chapter, we illustrate both full virtualization and OS-level virtualization. We use three popular and important facilities for creating a virtual environment within which a UNIX OS can work. What differentiates these three facilities is that, for the first two, all virtual environments are running under the same kernel (OS-level virtualization). In the third one, any number of different kernels can be running simultaneously on one machine (full virtualization).

Practically speaking, an important application of these implementations, as already stated, is to provide a measure of system security, in addition to what is described in