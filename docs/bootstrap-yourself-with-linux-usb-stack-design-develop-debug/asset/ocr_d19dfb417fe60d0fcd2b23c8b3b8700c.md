This section detailed various key menu options of the Linux USB subsystem of both host and device. Besides the menu options through interfaces such as command line and menuconfig, explore the Kconfig and the makefile so you know the files that make up the module and can explore the correct files.

# SUMMARY

When you're working on large code bases, configuration management is the key knowledge to develop over and above knowledge of source code. The same applies to the Linux kernel so that you can effectively use the kernel's various modules. For example, if your platform supports only USB device mode, it makes sense to remove the USB host subsystem drivers. This enables you to effectively use platform resources such as memory and avoid conflicts on shared resources. The Linux USB subsystem provides comprehensive menu options so you can select required modules and skip others. You need to update the menu option when you write your own driver and integrate it with the kernel.

# MORE READING

To better understand the kernel configuration and to modify a configuration file, read the Kconfig documentation from Documentation/kbuild/config-language.txt. You can also read about how to build the module Documentation/kbuild/modules.txt and the makefile Documentation/kbuild/makefile.txt.