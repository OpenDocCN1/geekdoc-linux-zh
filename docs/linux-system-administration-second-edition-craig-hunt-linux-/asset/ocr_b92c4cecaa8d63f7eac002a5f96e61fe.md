Action: Compiled & installed Samba 2.2.3a. Located in /usr/local/samba.

# # Kernel Compilation

The Linux kernel is a particularly critical and complex component on any Linux system. It therefore deserves special consideration in any discussion of software installation and maintenance. Although you can install a precompiled updated kernel much as you can other precompiled packages, doing your own kernel compilation offers certain advantages, as described shortly.

The kernel compilation and installation process has its own quirks, so this section covers the process in detail, starting at setting the compilation options and proceeding through rebooting the computer to use the new kernel.

# ## Why Compile Your Kernel?

With any luck, your computer booted and ran immediately after you installed Linux on it. This fact means that the Linux kernel provided with the distribution works. Why, then, should you go to the bother of compiling a new kernel? The most important advantages to custom kernel compilation are:

+   Architecture optimization The kernel includes optimization options for each of several classes of CPU—80386, 80486, and so on. Most distributions ship with kernels that are optimized for 80386 CPUs. By compiling a kernel for your particular CPU model, you can squeeze a little extra speed out of your system.

+   Removing unnecessary drivers The default kernel includes drivers for a wide variety of hardware components. In most cases, these drivers do no harm because they're compiled as *modules* (separate driver files), which aren't loaded unless necessary. A few are compiled into the kernel proper, however. These consume memory unnecessarily, thus degrading system performance slightly.

+   Adding drivers You may need to add a new or experimental driver to your system. This may be necessary if you're using an unusually new component, or if there's a bug fix that's not yet been integrated into the main kernel tree. Such changes often require you to *patch* the kernel—to replace one or more kernel source code files. For details on how to do this, check with the site that provides the new driver.

+   Changing options You may want to change options related to drivers, in order to optimize performance or improve reliability. As you examine the kernel configuration procedure, you'll see many examples of such options.

+   Upgrading the kernel You may want to run the latest version of the kernel. Sometimes you can obtain an upgrade in precompiled form, but occasionally you'll have to compile a kernel from source code.

Of course, kernel compilation isn't without its drawbacks. It takes time to configure and compile a kernel. It's also possible that the kernel you compile won't work. Be sure to leave yourself a way to boot using the old kernel, or you'll have a hard time booting your system after a failed upgrade. (This chapter describes how to boot the computer into either the old or the new kernel.)

194