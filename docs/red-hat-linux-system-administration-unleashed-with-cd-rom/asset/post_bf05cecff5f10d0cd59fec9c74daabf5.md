
## Kernel Building

Now we come to the part that many new users of Linux consider black magic or high art—building the kernel from source. There are many reasons for building a customized kernel. As discussed at the beginning of this chapter, three of the most common are

- Removing unused or unwanted drivers and modules.
- Adding missing functionality.
- Upgrading to a later kernel release.

This section looks at the various configuration options, discusses the kernel makefile, looks at ways to manage having multiple configurations of the same kernel version, and takes a look at the support in the source tree for customized installation scripts. To finish out the chapter, we will look at the make process and the sequence of events for building your kernel.

## Configuring the Linux Kernel

Before beginning the configuration of your customized kernel, it is important to consider a few things. For example, do you have enough space in the filesystem where the kernel source lives to build the new kernel? Do you know how to modify the lilo.conf file to add your new kernel? Do you have a set of rescue disks handy if something goes wrong? These are important questions to consider before beginning to modify your operating system kernel. In these cases, always apply the Boy Scout motto, “Be Prepared.”

Once you have considered these issues, you are almost ready to actually run one of the four available configuration programs. Before you do this, however, you should check the Changes file in /usr/src/linux/Documentation to ensure that you have the required versions of the system utilities. Once you have done so, you can start configuring your kernel. The four methods to this include the old style configuration script, a text menu-based configuration program, a GUI program using tcl/tk, and a semiautomated update method that builds a configuration based on an old configuration file. These configuration methods are selected using make targets:

```
make config      To use the old configure script
make menuconfig  To use the menu-based program
make xconfig     To use the GUI kernel configurator
make oldconfig   To use the old configuration file method
```

You may ask yourself why you would need four different configuration methods and which one is best. Unfortunately, there is no answer to which one is best, but the reason for having four methods is to accommodate the needs of different users. Consider the fact that not all Linux systems have fancy color monitors and the capability to run a GUI. This eliminates the xconfig option. Some do not have addressable text consoles that allow the use of the curses library, thus eliminating the menuconfig option, and sometimes, you don’t have the time or desire to interactively configure your new kernel, thereby eliminating the make config option. Having these four targets makes it possible to deal with all of these cases.

All that being said, however, I find that the most useful and the easiest to understand configuration method is the GUI one. This method requires that you are running X Windows, that you have your DISPLAY environment variable set, and that you have permission to connect to the running X server. If you do not meet these requirements, my next recommendation is the menuconfig option, which requires ncurses,

## Getting Started

To begin configuring your kernel, you must first change directory to the top level of your kernel source tree. This default location for the kernel source code in Red Hat Linux systems is /usr/src/linux, which is a symbolic link to /usr/src/linux-M.N.P-XX, where M.N.P is the kernel version. For Red Hat 6.0, this would be linux-2.2.5. Once in this directory, you type one of the make commands shown in the preceding section to start the configurator.

When selecting either the GUI configurator or the menu-based configurator, there will be a brief period of activity while the config programs are built, followed by either the appearance of the GUI or the menu-based interface. The initial screens for these two methods are shown in Figure 35.2 and Figure 35.3.

FIGURE 35.2
The GUI kernel configurator.

![](img/4886c42c7629f445c7f7f3011ffbf3c3_1134_0.png)

FIGURE 35.3
The menu-based kernel configurator.

![](img/4886c42c7629f445c7f7f3011ffbf3c3_1135_0.png)

## Choosing Configuration Options

Now you can begin examining the various options that you can configure on your Linux kernel. We will not be examining all of the options, (there are currently over 400 of them), but will take a look at those that you are more likely to want to change. If you see an option not covered here, your first step should always be to read the help text for the option. It explains the options and gives you suggestions on if and when you would want to change it.

> Tip
> 
> In order to answer some of the questions about various kernel options, you will need to know about the various parts of your computer. You'll need to know the chipset used on the motherboard, whether your parallel port is a standard port or supports the newer extensions, the type of network card you have, and many more details about the inner workings of your PC. If you are converting your computer from a Windows system to a Linux system, you can get a lot of this type of information by printing out the hardware profile of your computer. You might also want to have your hardware manuals on hand to look things up.

## Code Maturity Level

The 2.2 series kernel distributed with Red Hat Linux 6.0 is part of what is considered the stable or production release kernel branch; however, there are some features that are deemed experimental. This experimental designation may mean that they represent a feature for which a standard is evolving. It may be a driver that is considered essential enough to include in the release, but is not tested enough to be considered rock solid.

## Caution

Experimental features are so designated because they are not heavily tested or are subject to change or removal. Using these features may make your system unstable. This instability may result in your system crashing. If you are building a system that requires high availability, you should carefully consider whether the experimental features should be included in your configuration.

All of the features in the kernel that are of this nature are clearly marked and you should use them only if they meet a need. Please be aware, however, that if your system becomes unstable, you should first remove any experimental options from your kernel before filing a bug report, especially if you think that the bug exists in a non-experimental feature or driver.

It is your decision as to whether you want to be presented with these experimental features. If you are not interested in taking risks, say no to this option. I usually say yes and may try one or two of the experimental options so that by real-world testing, they can move beyond the experimental stage.

## Processor Type and Features

One part of the kernel sources that you will most likely want to change is the selection of the processor type and features, due to the fact that the kernel distributed with some Linux distributions is compiled for the lowest common denominator, an Intel 386 with no math coprocessor.

By specifying the proper processor type, your kernel will be built with optimizations for that specific processor turned on, which is intended to increase performance. It is important to remember, however, that a kernel built for an advanced CPU may fail to run on an older machine, so if you build all of the kernels for your network on a single host, you should select the processor type with this in mind.

The following excerpt from the /usr/src/linux/Documentation/Configure.help file describes the proper setting of this option.

Here are the settings recommended for greatest speed:

- "*386*" for the AMD/Cyrix/Intel 386DX/DXL/SL/SLC/SX, Cyrix/TI 486DLC/DLC2 and UMC 486SX-S. Only "*386*" kernels will run on a 386 class machine.
- "*486*" for the AMD/Cyrix/IBM/Intel DX4 or 486DX/DX2/SL/SX/SX2, AMD/Cyrix 5x86, NexGen Nx586 and UMC US0 or US5.
- "*586*" for generic Pentium CPUs, possibly lacking the TSC
