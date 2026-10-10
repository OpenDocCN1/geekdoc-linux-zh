Dtc refers to the Device Tree Compiler, which we will get to shortly. Nonetheless, the *u-boot* executable is there, and you can run it from a command shell. The device tree compiler is part of the Linux kernel source tree and again, there does not seem to be a corresponding package in the CentOS repos. A simple hack to solve this one is to copy `linux/scripts/dtc/dtc` to somewhere in your path such as `/usr/local/bin`.

# *Device Trees*

One of the biggest problems with porting an operating system such as Linux to a new platform is describing the hardware. That is because the hardware description is scattered over perhaps several dozen or so device drivers, the kernel, and the boot loader, just to name a few. The ultimate result is that these various pieces of software become unique to each platform, the number of configuration options grows, and every board requires a unique kernel image.

There have been a number of approaches to addressing this problem. The notion of a “board support package” or BSP attempts to gather all of the hardware-dependent code in a few files in one place. It could be argued that the entire `arch/` subtree of the Linux kernel source tree is a **gigantic board support package**.

Take a look at the `arch/arm/` subtree of the kernel. In there you will find a large number of directories of the form `mach-*` and `plat-*`, presumably short for “machine” and “platform,” respectively. Most of the files in these directories provide configuration information for a specific implementation of the ARM architecture. And of course, each implementation describes its configuration differently.

Would not it be nice to have a single language that could be used to unambiguously describe the hardware of a computer system? That is the premise, and promise, of device trees.

The peripheral devices in a system can be characterized along a number of dimensions. There are, for example, character vs block devices. There are memory mapped devices, and those that connect through an external bus such as I2C or USB. Then there are *platform* devices and *discoverable* devices.

Discoverable devices are those that live on external busses, such as PCI and USB, that can tell the system what they are and how they are configured. That is, they can be “discovered” by the kernel. Having identified a device, it is a fairly simple matter to load the corresponding driver, which then interrogates the device to determine its precise configuration.

Platform devices, on the other hand, lack any mechanism to identify themselves. System on Chip (SoC) implementations, such as the Sitara, are rife with these platform devices—