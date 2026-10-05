
# SuSE System Administration
PART III

There is a popular misconception that kernel tuning is no place for the average user. In reality, this is both true and false. Like any other feature of Linux, the configuration possibilities are endless and deep, but you don't necessarily need to understand arcane PCI chipset mantras or the details of virtual memory to tailor a better Linux for your computer. Armed with nothing than your computer manuals, you should be able to zero in on features you need and leave the more kernel tuning for sometime down the road. If you do know all technical details, Linux will not stand in your way. But if all you know how to run a shell command, this section will show you how you can build a better Linux for your computer.

Linux is a UNIX-like system, and the core of a Linux system is the kernel, the innermost layer of the operating system that provides a uniform interface to the local hardware. When your computer starts, the boot loader hands control to the kernel. The kernel identifies your hardware, initiates the boot scripts, and launches your network and terminal daemons. After the boot, the kernel becomes the gateway to the local hardware, supplying applications with a standard interface to basic services such as task switching, signaling, device I/O, and memory management.

Although the default kernel installed by your SuSE stands a very good chance of running on your hardware, kernel cannot be all things to all people. At some point, you will want to harness the real power of Linux—the power of choice. In Linux, kernel tweaking can be as simple as adding a few command parameters to modify the kernel at boot time or picking and choosing from the ever-growing list of modules and kernel options. However, it can also involve complex tasks such as the precise tuning of memory and filesystem behavior, or the direct modification or creation of driver C code. The Linux kernel can be adapted for low-memory machines, optimized as a router or firewall, or extended to new hardware, alien filesystems, and a wide array of network protocols.

This chapter describes what makes the Linux kernel special, even among UNIX-like systems, and includes tips and tutorials on configuring your Linux iron. This chapter covers

- An overview of the Linux kernel architecture
- Obtaining and patching Linux kernel sources
- Compiling a kernel for multiple machines
- Configuring modules and the new kmod auto-loader
- How to configure the kernel for alien filesystems and arbitrary binary executables
- Optimizing Linux as a router versus a workstation
- Virtual memory
- Filesystem tuning
- RAID support and software RAID
- Adding network services as IP masquerading and port forwarding, IPv6, Packet Radio, ISDN, and firewalls
- Installing MS-DOS National Language Support (NLS)
- Supporting special devices as video/TV cards, joysticks, and infrared controls
- Configuring the Open Sound System driver and the new software-based MIDI Wave Table
- Kernel troubleshooting

After reading this chapter, you will be well equipped to create a custom kernel for your particular machine. The size of this chapter may be a little daunting, but this only illustrates the flexibility of the Linux kernel. You may only need to consult those few sections on installing your sound or special device. On the other hand, for those difficult problems of kernel optimization, advanced networking, or tailoring the kernel for embedded and other special situations, this chapter give you a full overview of what is possible.

![](img/cbac72550c7126a22162e94d91a0c360_690_0.png)

# Caution

The worst that can happen when reconfiguring your kernel is boot failure. It happens to the best of us, usually because of incompatible settings or forgetting to run LILO after changing a kernel. There are few things as frightening as the dread LILO-boot prompt.

Before rebooting a new kernel, you should take a few precautions to ensure a backup boot method. If your hardware has a floppy disk, keep your SuSE install/rescue disks handy. Also, production machines should always keep a boot-floppy with their current stable kernel. Your LILO configuration should also include at least one backup kernel image.

Although many people have a penchant for reinstalling from scratch, a habit unfortunately instilled by another popular operating system, in Linux this is a rarity. As the South African proverb goes, "if you hear hoofbeats in the street, it is probably not a zebra." With Linux, your darkest hour still probably does not require reinstalling the entire system. In seemingly hopeless situations, it is far more likely that your system can be safely rescued and repaired.

When the worst happens, use your rescue disks to boot your system, manually check and mount the hard drive, restore order, rerun LILO, and breathe easier. You can also find a number of rescue disks and tools in the Metalab archive at ftp://metalab.unc.edu/pub/Linux.

# Introduction to the Linux Kernel

Linux is one of the fastest-growing OS platforms, already rivaling the installed base of MacOS and giving NT something to worry about. There are millions of users and countless developers deploying Linux in Web servers, edge servers, routers, and embedded systems. Linux has been used on the space shuttle, for robotics, and in Hollywood. The reason for this success is not simply the low price tag. Linux has succeeded because it is based on a solid design that's friendly to open source development and portability. But succinctly, Linux succeeds because it works.

Linux is "UNIX-like." It's not a version of UNIX, but rather a new OS highly reminiscent of UNIX. This heritage has freed Linux from legacy code: Linux is designed to be compatible, but has been developed from scratch. This freedom allowed Linus Torvalds and the kernel authors to develop a core framework that is highly portable. In the years since the first MC68000 rewrite for the Amiga, Linux has been ported to platforms from the PalmPilot to the Alpha Processor, proving the portability of the core design.

Linux is an extremely large and complex piece of software. The kernel contains 1.7 million lines of source code, and by commercial standards, we could expect the development of Linux to take 5 to 10 years and require up to 500 programmers. The development process of open source has also been proven through the kernel project: Richard Gooch's Kernel FAQ (http://www.tux.org/linux/) observes that Linux is a little more than eight years old, placing it right on track compared to those commercial standards, while harnessing the talents of many as a thousand programmers spread around the world under the peer-review of thousands more.

## Microkernels Versus Monoliths

> "We should do smart things with stupid technology before we do stupid things with smart technology."—Bill Buxton, Alias Research

A successful operating system must weigh performance and portability. In the real world, the choices made in Linux are often a focus of debate. Linux is "monolithic," meaning it places many core services inside the kernel.

When Linux began working on the kernel in 1991, microkernels, small and simple, were the darling of academia and deemed to be the Holy Grail. In the '90s, the conventional wisdom on compilers believed that a simple set of interfaces could abstract the host. This approach may sound familiar to Java programmers; microkernel model also somewhat influenced the design of Microsoft's NT.

Linux was not convinced. Microkernels seemed too complex and prone to performance bottlenecks. For Linux, he chose to optimize the knowledge from microkernel research and apply it to a monolithic design. By designing for the lowest common denominator of many different architectures, he could keep Linux essentially portable.

Another pillar that guides Linux kernel development is the creation of good interfaces. A small number of simple interfaces allowed other developers to extend Linux with minimal damage to other parts of the project. Also, a process was set to limit adding any new interfaces: although any number of developers could freely build new drivers to plug the disk-driver interface, adding a new service such as video4linux (cameras and radio/TV cards) would carry the risk of including a bad interface, and an error could haunt the project later. Linux cites the example of 11-character filename imposed on NT by the DOS legacy; NT must not duplicate all files for longer.

Although Linux does carry some baggage being UNIX-compatible, its interface-based design is a major force behind its popularity. Rather than having a free-for-all or a design by committee, Torvalds can exercise control over the project by guarding the interfaces. Yet Linux can also accommodate a staggering and ever-increasing number of new devices. With the newer kernels and the notion of dynamically loaded modules, Linux has opened even more to the development of third-party modules from outside developers and vendors.
