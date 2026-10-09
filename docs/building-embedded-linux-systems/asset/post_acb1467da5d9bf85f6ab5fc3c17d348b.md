
# Tracking development with git

Day-to-day development of the Linux kernel is supported through extensive use of Linus Torvald’s git SCM tool. *git*, the “stupid content tracker,” was written by Torvalds in response to a sudden need to replace a proprietary version control system that had previously been in use for some time. It works by tracking changesets—related groups of changes to the kernel—rather than changes (patches) to individual source files. In this way, it is possible to see modifications in terms of their collective impact upon the kernel, rather than by wading through many patches. A variety of third-party tools, such as *gitk*, can be used to provide a visual representation of the changing state of a *git* repository. You can obtain a copy of your Linux distribution, or at *http://www.kernel.org*.

You can download a private copy of the kernel *git* repository using the *clone* command:

```
git clone git://git.kernel.org/pub/scm/linux/git/torvalds/linux-2.6.git linux_26
```

This clones, or copies, the upstream Linux kernel repository (which Linus Torvalds maintains on the kernel.org site) and creates a local directory, in this case called *linux_26*, that reflects the current state of the art. The upstream kernel repository is frequently changing due to the many thousands of changesets that can make it into the kernel from one release to the next. If you’re serious about tracking the Linux kernel, you will want to get into a daily habit of updating your local copy of Linus’s repository. You can do this using the following command, from within the local repository:

```
git pull
```

Many more commands exist, along with a number of documents describing the kernel development process and how it involves *git*. You can find out more about *git* or download a copy (if your Linux distribution does not include it, or you are running another operating system for which *git* has been ported) at *http://git.or.cz*.

# Third-party kernel trees and patches

Rather than using the kernel available from the kernel.org website, you may also choose to use a third-party-supplied 2.6 kernel. This will typically be the case whenever you elect to use a specific embedded Linux distribution. Although these kernels are based on the upstream 2.6 Linux kernel, they are typically patched with a variety of additional features, bug fixes, and other modifications deemed useful by the vendor. Therefore, you should not place too much stock in the version of the kernel they claim to provide—you might think you have a 2.6.20 kernel, but in fact it may differ widely from the 2.6.20 kernel available from the kernel.org website. In any case, you should contact your vendor for support in the first instance; the kernel community, in general, does not support vendor kernels.

You may also want to try some of the various patches made available by some developers. Extra kernel functionality is often available as an independent patch before it is integrated into the mainstream kernel. Robert Love’s kernel preemption patch, for instance, was maintained as a separate patch before Linus integrated it into the 2.5 development series. We will discuss a few kernel patches in Chapter 11. Have a look at *Running Linux* if you are not familiar with patches.

# Configuring the Kernel

Configuration is the initial step in the build of a kernel for your target. There are many ways to configure the Linux kernel, and there are many options from which to choose. Regardless of the configuration method you use or the actual configuration options you choose, the kernel will generate a .config file at the end of the configuration and will generate a number of symbolic links and file headers that will be used by the rest of the build process.

We will limit our discussion to issues specifically affecting embedded systems. For general advice on kernel configuration and compilation, consult one of the previously mentioned texts on Linux kernel development or the documentation supplied inside the Linux kernel source tree itself; see the Documentation subdirectory.

*Linux Kernel in a Nutshell* (published by O'Reilly and also available online at http://www.kroah.com/ikln) provides a brief but thorough guide to configuring and building a kernel, along with explanations of some of the most popular configuration options. (It is not specifically addressed to embedded systems developers, though.)

## Configuration Options

It is during configuration that you will be able to select the options you want to see included in the kernel. Depending on your target, the option menus available will change, as will their content. Some options, however, will be available no matter which embedded architecture you choose. The following is a list of the main menu options available to all embedded Linux architectures:

- Code maturity level options
- General setup
- Loadable module support
- Block layer
- Networking
- Device drivers
- Filesystems
- Kernel hacking
- Security options
- Cryptographic options
- Library routines

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
