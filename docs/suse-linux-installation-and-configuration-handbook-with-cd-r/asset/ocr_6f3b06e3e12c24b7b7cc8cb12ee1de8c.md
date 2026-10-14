Installing a new kernel can be done in one of two ways. You can either get a precompiled kernel that suits your needs, or if you can't find one you will have to configure and compile your own. The first choice requires much less time than the second one, because a precompiled kernel just needs to be installed and the system rebooted. If you chose to compile your own kernel, you will need to spend some time configuring and compiling it.

The answer to this question depends on the reason you are installing a new kernel. If you are looking to support a device or service that your current kernel does not, you can start by looking for a precompiled kernel that has that support. If you did not find a precompiled kernel that meets your needs, or if you want to upgrade to a newer kernel version, you will probably need to compile your own. Take your time making this decision; we will discuss both methods in this chapter. Let us start off by installing a precompiled kernel.

# Installing a Precompiled Kernel

The fastest method of installing a new kernel is by using a precompiled one. A precompiled kernel is a kernel that was configured, compiled, and packaged by SuSE for easy installation by the user. SuSE attempts to provide a precompiled kernel for most common hardware and service configurations. If you are looking for support for common hardware and services, chances are that you will find a precompiled kernel good enough for you. The more uncommon the configurations you want, the less your chances are.

There are two ways you can get a precompiled kernel from SuSE: the SuSE CDs and from their site on the Internet. SuSE CDs have different configurations of the same kernel. On the other hand, the Internet site will have just one configuration but for a newer kernel version than the one you are currently running. So if your aim is to just upgrade to a newer version of your kernel, it will probably want to get it from the Internet site. You can configure it yourself and recompile it to fine-tune it to your exact needs later.

# Installing from SuSE CDs

SuSE CDs have a wide variety of precompiled kernels that support a range of different devices and services. These kernels are easy to install. All you need to do is pick the one that fits your needs, install it, and reboot your machine. When your machine boots again, it will be booting the new kernel.

You use YaST to browse the list of precompiled kernels and install any of them. Follow these steps:

+   1. Run YaST and choose System Administration, Kernel and Boot Configuration, Select Boot Kernel.
+   2. YaST then displays a list of the available kernels that you can install right away (see Figure 8.1).