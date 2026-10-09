This section will not cover each option individually, as the kernel configuration menu provides context-sensitive help that you can refer to as you perform the configuration. Many of the options are self-explanatory—for example, which device drivers will be built—while others are less obvious. For instance, the kernel can include a variety of strong security options as part of the SELinux stack implemented by the U.S. National Security Agency (NSA). Many of these options will make less sense to you if you are not familiar with the design of SELinux. This isn’t a huge problem, however, since only a few embedded devices choose to make use of the extensive SELinux functionality in Linux.

One of the most important option menus is the one in which you choose the exact instance of the processor architecture that best fits your target. The name of this menu varies according to your architecture. Table 5-1 provides the system and processor selection option menu name, along with the correct kernel architecture name for several of the common architectures. When issuing *make* commands, you need to set the *ARCH* variable to the architecture name recognized by the kernel *Makefiles*.

**Table 5-1. System and processor selection option and kernel architecture name according to processor architecture**

| Processor architecture | System and processor selection option | Kernel architecture name |
|-----------------------|-------------------------------------|-------------------------|
| x86                   | Processor type and features        | i386                    |
| ARM                   | System Type                        | arm                     |
| PPC                   | Platform support                    | powerpc (or ppc for older targets) |
| MIPS                  | Machine selection/CPU selection     | mips                    |
| SH                    | System type                        | sh                      |
| M68k                  | Platform-dependent support or processor type and features | m68k or m68knommu |
| AVR32                 | System Type and features           | avr32                   |

When browsing through the kernel configuration options for your target, bear in mind that it is possible to enable support for hardware you do not have. Indeed, the configuration menus may allow you to enable many kernel features that have never been tested for your target. There are many millions of possible kernel configuration combinations, and it is not possible for the kernel developers to test every configuration choice you may make. Typically, selecting support for a device that is not present won’t prevent a system from booting, especially if it’s simply a PCI device driver that won’t be detected by the kernel anyway. But this isn’t always the case on embedded systems, and it is still all too possible to create a kernel that will not boot on a particular target. Therefore, you are advised to verify your selections against the published documentation for your chosen target before building your target kernel.