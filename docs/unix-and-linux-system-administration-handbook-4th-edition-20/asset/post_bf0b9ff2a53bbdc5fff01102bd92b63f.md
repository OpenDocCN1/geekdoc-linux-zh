
# Recommended reading

The exact steps needed to make the linker use a specific version of a shared library vary from system to system. Under Linux, you can set the LD_LIBRARY_PATH environment variable or use the linker's -R option.

# Wrapper scripts

Unfortunately, library-level compatibility is only half the story. The fact that tools invoke one another directly is another opportunity for conflict. For example, suppose the utility foo makes frequent use of the utility name bar. If you update the default version of bar, you may find that foo suddenly stops working. In this case, you can conclude that foo depended on some behavior of bar that is no longer supported (or at least no longer the default).

If your software repository supports multiple versions (e.g., /tools/util/bar-1.0 and /tools/util/bar-2.0), you can fix this problem by making the original version of foo real and replacing it with a wrapper script:

```
#!/bin/sh
# make sure the program finds any files co-packaged with it
# first if it does not use an explicit path.
PATH=/tools/util/bar-1.0/bin:$PATH
export PATH
exec /util/foo-1.0/bin/foo.real "$@"
```

Now foo will be launched with a customized PATH environment variable, and will call the old version of bar in preference to the new one.

Wrappers are a powerful tool that can address not only package dependencies but also issues such as security, architecture-, or OS-dependence, and usage tracking. Sites wrap all shared binaries.

# 12.13 RECOMMENDED READING

- INTEL CORPORATION AND SYSTEMSOFT. Preboot Execution Environment (PXE) Specification, v2.1. 1999. pix.net/software/pxeboot/archive/pxespec.pdf

- PXELinux Questions. syslinux.zytor.com/wiki/index.php/PXELUX

- RODIN, JOSIP. Debian New Maintainers Guide. debian.org/doc/maint-guide. This document contains good information about .deb packages.

- SILVA, GUSTAV NORONHA. APT HOWTO. debian.org/doc/manuals/apt-howto

- HOHNEL, DIRK, AND FABIAN HERSCHEL. Automated installation of Linux Systems Using YaST. usgen.org/linux/659/full_packages/hohnedel/hohnedel_html

- STUCKELBERG, MARC VIELLUMIER, AND DAVID CLERC. Linux Remote-Boot mini-HOWTO: Configuring Remote-Boot Workstations with Linux, DOS, Windows 95/98 and Windows NT. 1999. tldp.org/HOWTO/Remote-Boot.html

- The Red Hat Enterprise System Administration Guide. redhat.com/docs

![](img/579efec8c67772f31ecf34844bbb71a2_461_0.png)

Chapter 12

Software Installation and Management

- WACHSMANN, ALF. How to Install Red Hat Linux via PXE and Kickstart. stanford.edu/~alfw/PXE-Kickstart/PXE-Kickstart.html

- BURGESS, MARK. Cfeengine: A Site Configuration Engine. USENIX Computing Systems, Vol 8, No 3. 1995. cfeengine.org

- HP Ignite-UX Administration Guide. docs.hp.com/en/5992-5309/5992-5309.pdf

- NIM from A to Z. www.redbooks.ibm.com/redbooks/pdfs/sg24296.pdf. This is a thorough Network Installation guide.

- Solaris Advanced Installation Guide. docs.sun.com/app/docs/doc/082-5740

# 12.14 Exercises

- E12.1 Outline the differences between Kickstart, JumpStart, and Ignite-UX. What are some of the advantages and disadvantages of each?

- E12.2 Install Subversion from subversion.tigris.org. Set up svversion and create a repository. How can you make the repository usable from anywhere on the local network but still maintain reasonable security?

- E12.3 Review the way that local software is organized at your site. Will the system scale? Is it easy to use? Discuss.

- E12.4 What are some of the most important features of a configuration management system? What are the security implications of distributed configuration files over the network?

- E12.5 Set up the network installer of your choice and install a new machine by using your server. Outline all the steps needed to perform this task. What were some of the stumbling blocks? What are some of the scalability issues you discovered with the installer you chose?

# 13 Drivers and the Kernel

The kernel hides the system's hardware underneath an abstract, high-level programming interface. It furnishes many of the facilities that users and user-level programs take for granted. For example, the kernel creates all the following concepts from lower-level hardware features:

- Processes (time-sharing, protected address spaces)
- Signals and semaphores
- Virtual memory (swapping, paging, mapping)
- The filesystem (files, directories, namespace)
- General input/output (specialty hardware, keyboard, mouse, USB)
- Interprocess communication (pipes and network connections)

The kernel incorporates device drivers that manage their interaction with specific pieces of hardware; the rest of the kernel is, to a large degree, device independent. The relationship between the kernel and its device drivers is similar to the relationship between user-level programs and the kernel. When a process asks the kernel (or more accurately, a driver) might translate this into device commands, the kernel would break this request into device instructions.

![](img/579efec8c67772f31ecf34844bbb71a2_463_0.png)

Chapter 13

# Drivers and the Kernel

The kernel is written mostly in C, with a sprinkling of assembly language to interface with hardware.

One of the advantages of Linux and other open source environments is that the availability of source code makes it relatively easy to mold your own. In the early days of Linux, having skills in this area was a necessity because it was difficult to administer systems without being able to tune the kernel.

Fortunately, sysadmins can be perfectly effective without soiling their hands with kernel code. In fact, such activities are better left to kernel developers. Administrators should focus on the overall needs of the user community. (This was not always true!)

# 13.1 KERNEL ADAPTATION

All the UNIX platforms covered in this book run monolithic kernels, in which the entire operating system runs in kernel space, a section of memory reserved for privileged system functions. In a monolithic kernel, services such as device drivers, interprocess communication, virtual memory, and scheduling run in the same address space. This approach contrasts with a microkernel architecture, in which many of these services run in user mode (i.e., as regular processes). The pros and cons of the two architectures have been hotly debated for years, but most kernel developers agree that both have merit.

Linux is a monolithic kernel at heart, but it allows user-space drivers for many devices. The Gelato, UIO, FUSE, and FUSD projects each provide interfaces to user space. Nevertheless, most drivers are still implemented in kernel mode, for performance reasons.

Modern kernels support on-demand loading of modules, which can incorporate device drivers and other kernel functions needed without rebuilding the kernel and rebooting. Drivers, filesystems, and new system calls are all commonly implemented as modules. The memory used by a module is allocated and freed as the code is loaded or removed.

A kernel can learn about the system's hardware in several ways. The most basic way is that you explicitly inform the kernel about the hardware it should expect to find (or pretend not to find, as the case may be). In addition, the kernel prospects for many devices on its own, at boot time or dynamically (once the system
