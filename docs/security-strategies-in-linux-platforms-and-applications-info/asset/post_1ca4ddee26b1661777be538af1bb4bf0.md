
# Chapter 10 Topics

This chapter covers the following topics and concepts:

- Which options do you have with distribution-specific functional kernels
- What the stock Linux kernel is
- How to manage upgrades to the stock Linux kernel
- What to look for in a security or kernel update
- What development software is available for a custom kernel
- Which Linux kernel development tools are available
- How to build your own secure kernel
- How to increase security using kernels and the /proc/ filesystem
- What best practices are for kernel security risk mitigation

# Chapter 10 Goals

When you complete this chapter, you will be able to:

- Choose the best kernel suited to your systems
- Customize options within the Linux kernel
- Compile the source code for a kernel, with patches
- Configure how the kernel works in real-time

# Functional Kernels for Your Distribution

The developers behind some Linux distributions want to make things as easy as possible for their users. They provide installation programs to load and configure their distributions on a wide variety of hardware. They release software in packages, compiled in binary format. All the user has to do is load and install the package.

The kernels released by Linux vary at least architecture. Because the kernel includes interfaces between hardware and software, kernels vary with that most fundamental architectural hardware component, the CPU.

The developers behind some Linux distributions may also configure, customize, and release different binary kernels for different functional situations. For example, administrators may not install a graphical user interface (GUI) on many servers, developers may choose to deactivate features associated with high-end graphics cards for a server kernel.

# Kernels by Architecture

Linux kernels are available for a wide variety of architectures. Because the developers at the Linux Kernel Organization release only the source code for the kernel, it is left to the developers behind a distribution to customize, compile, and test a kernel for each architecture. Such testing takes time and effort. At last count, Debian Linux released production kernels for more than a dozen architectures, including the following:

- Standard 32-bit—The normal 32-bit PC architecture; may be labeled with an i386, i586, or i686 in the package name.
- Standard 64-bit—The normal 64-bit PC architecture: frequently labeled with an amd64 or x86_64 in the package name.
- Alpha—The CPU developed by the original Digital Equipment Corporation, now owned by HP.
- Advanced RISC Machine (ARM)—The CPU originally developed by the former Acorn Computers, Ltd., licensed by a number of companies.
- Itanium—A 64-bit CPU from Intel. Other Intel 64-bit CPUs are available.
- Motorola 68000 (m68k)—A 32-bit CPU developed by Motorola.
- PowerPC—A 32-bit CPU developed by Apple, IBM, and Motorola.
- s390—The IBM system 390 32-bit CPU.
- Sparc—A 64-bit CPU originally developed by Sun Microsystems.

In addition, Red Hat has its Enterprise Linux distributions for the IBM iSeries and pSeries CPUs. However, it does not support any of the other CPUs except for standard 32-bit and 64-bit systems, along with Intel Itanium systems on its older releases. Red Hat is not supporting the Itanium CPU on its newest releases.

One featured in mostly older Linux distributions is symmetrical multiprocessing (SMP), used for systems with multiple CPUs. On current Linux distributions, that feature has been incorporated into the main kernel. On the other hand, Ubuntu limits its officially supported releases to two different architectures: the 32- and 64-bit Intel-compatible CPU. The package names of such kernels may be a bit misleading, as they include i386 for the 32-bit kernel and amd64 or x86_64 for the 64-bit kernel. Such kernels work on systems with both Intel and Advanced Micro Devices (AMD) CPUs. focus enables Ubuntu to customize kernels for different purposes.

# Kernels for Different Functions

The developers behind most Linux distributions create kernels for different functions. Those who use Xen for virtual machines should be familiar with the specialized kernel for that purpose. Among the most popular Linux distributions, Ubuntu builds kernels for a wide range of functions. One list of Ubuntu kernels is shown in Figure 10-1. Some of the packages shown are meta packages; for example, the linux-image-generic package is automatically linked to the package built for the latest Linux kernel release.

> NOTE While Ubuntu developers build a kernel that emulates the ARM architecture, that kernel is not officially supported by Canonical, Ubuntu's corporate sponsor.

- linux-generic Generic kernel image for version 2.62.30 on i686
- linux-image-2.62-39-386 Linux kernel image for version 2.62.30 on x86/64
- linux-image-2.62-39-generic-pae Linux kernel image for version 2.62.30 on x86
- linux-image-2.62-31-virtual Linux kernel image for version 2.62.30 on x86/64
- linux-image-2.62-304-ec2 Linux kernel image for version 2.62.30 on x86/64
- linux-image-386 Generic kernel image
- linux-image-generic Linux kernel image for ec2 machines
- linux-image-generic Generic kernel image
- linux-image-server Linux kernel image on Server Equipment.
- linux-image-virtual Linux kernel image for virtual machines
- linux-image-2.62-31-rt Linux kernel image for version 2.62.31 on Ingo Molnar's time preemption patch
- linux-image-rt RealTime (RT) Linux kernel image

FIGURE 10-1
Ubuntu kernel packages options.

The meta-packages shown in Figure 10-1 are described in Table 10-1. Figure 10-1 is based on selected output from the apt-cache search linux command. It does not include debug or development kernels. Kernels are not suitable for production, in part they have not been tested for security. It specifies the meta-package associated with the kernel, as the installation of a meta-package automatically installs the latest version of the kernel so described. Of course, if something other than the latest version of a kernel is best for a system, you should be able to choose that package by version number. A list of such kernel version packages would be.

TABLE 10-1 | Typical Ubuntu kernel packages.
| PACKAGE | DESCRIPTION |
| :--- | :--- |
| linux-image | Installs latest available kernel |
| linux-image-386 | Installs latest available kernel |
| linux-image-ec2 | Installs latest available kernel |
| linux-image-generic | Installs latest available kernel |
| linux-image-generic-pae | Installs latest available kernel |
| linux-image-server | Installs latest available kernel |
| linux-image-virtual | Installs latest available kernel |
| linux-image-rt | Installs latest available kernel |

# Kernel Risk Mitigation

In general, these meta-packages are customized for 64-bit systems. Some of these may not work for.

> NOTE be aware that the package names associated with the Linux kernel may change from time to time, and may vary by distribution. Ubuntu kernel packages used to have kernel in package name.

# The Stock Kernel

The stock kernel is the generic kernel released by the developers of Linux Organization at http://kernel.org/. The overall leader is Lin Torvalds, who developed the first kernel in 1991. Linux kernel version 0.01 was released that year. In 1992, Torvalds adopted the GNU Public License (GPL) for all Linux kernels. He is still acknowledged as the lead developer of Linux, coordinating the efforts of thousands of other developers.

The stock kernel is sometimes known as the "mainline" or "vanilla". Many kernel developers work on releases that may be stable or unstable. The current maintainer of the stable release tree is Greg Kroah-Hartman. Other key developers are responsible for different kernel subsystems.

# Kernel Numbering Systems

To understand the sequence of Linux kernels, you need to understand the Linux numbering system.

Production versions of most current Linux stock kernels include four numbers, such as 2.6.32.4, in majorversion.majorrevision.updateversion.patchnumber format. The following is a brief explanation of these kernel numbers:

- Majorversion—Specifies a version with drastic changes from a previous kernel.
- Majorrevision—Associated with major changes to the kernel. Through version 2.6, even-numbered major revisions were stable. Odd-numbered kernel versions such as 2.5 were unstable. If and when version 2.7 is released, it may also be an unstable release.
- Updateversion—Released for important updates and new features to the kernel.
- Patchnumber—Associated with bug fixes and security updates to the kernel.

Kernels with new update versions are released approximately every three months. As of early 2010, there are no near-term plans for the next major revision (presumably kernel version 2.7).
