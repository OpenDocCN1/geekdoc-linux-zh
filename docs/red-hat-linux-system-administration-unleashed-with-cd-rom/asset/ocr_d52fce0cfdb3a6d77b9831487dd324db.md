# Kernel Building

Now we come to the part that many new users of Linux consider black magic or high art—building the kernel from source. There are many reasons for building a customized kernel. As discussed at the beginning of this chapter, three of the most common are

+   - Removing unused or unwanted drivers and modules.
+   - Adding missing functionality.
+   - Upgrading to a later kernel release.

This section looks at the various configuration options, discusses the kernel makefile, looks at ways to manage having multiple configurations of the same kernel version, and takes a look at the support in the source tree for customized installation scripts. To finish out the chapter, we will look at the make process and the sequence of events for building your kernel.

# Configuring the Linux Kernel

Before beginning the configuration of your customized kernel, it is important to consider a few things. For example, do you have enough space in the filesystem where the kernel source lives to build the new kernel? Do you know how to modify the lilo.conf file to add your new kernel? Do you have a set of rescue disks handy if something goes wrong? These are important questions to consider before beginning to modify your operating system kernel. In these cases, always apply the Boy Scout motto, “Be Prepared.”

Once you have considered these issues, you are almost ready to actually run one of the four available configuration programs. Before you do this, however, you should check the Changes file in /usr/src/linux/Documentation to ensure that you have the required versions of the system utilities. Once you have done so, you can start configuring your kernel. The four methods to this include the old style configuration script, a text menu-based configuration program, a GUI program using tcl/tk, and a semiautomated update method that builds a configuration based on an old configuration file. These configuration methods are selected using make targets:

```
make config      To use the old configure script
make menuconfig  To use the menu-based program
make xconfig     To use the GUI kernel configurator
make oldconfig   To use the old configuration file method
```