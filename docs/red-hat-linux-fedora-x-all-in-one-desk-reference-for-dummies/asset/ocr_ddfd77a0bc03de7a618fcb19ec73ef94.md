# Rebuilding the Kernel

Building the kernel involves the following phases:

+   * Configuring the kernel
* Building the kernel
* Building and installing the modules
* Building a new file for the initial RAM disk
* Installing the kernel and setting up GRUB

I explain these phases in the next few sections, but first you need to know the difference between linking in a driver versus building a driver as a load-module.

# Creating a monolithic versus a modular kernel

You have two options for the device drivers needed to support various hard-devices in Linux:

+   * Link on support: You can link the drivers for all hardware on your system into the kernel. The size of the kernel grows as device-driver code incorporates the kernel. A kernel that links in all necessary code is a monolithic kernel because it's one big file.
* Use modules: You can create the drivers in the form of loadable kernel modules. A module is a block of code the kernel can load after it starts running. A typical use of modules is to add support for a device without having to rebuild the kernel for each new device. Modules don't have to be device drivers; they can also add new functionality to the kernel. A kernel that uses modules is a modular kernel.

You don't have to create a monolithic or fully modular kernel. In fact, linking some directly into the kernel but building frequently used device drivers in the form of modules is common practice. For a Fedora Core distribution, a mostly modular kernel makes sense, along with a large number of modules that can support many different types of hardware. The Fedora installer configures the system to load only modules needed to support the hardware installed in your user's.

When you create a custom kernel for your hardware configuration, you may want to link all required device drivers into the kernel. You can still keep the size of such a monolithic kernel under control because you link in device drivers only for the exact set of hardware installed on your system.

![](bbox=[0.13125, 0.77667, 0.20625, 0.8406699999999999])