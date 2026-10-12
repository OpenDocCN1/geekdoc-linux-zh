# Chapter 27

# Adopting the Linux 2.6 Kernel

In This Chapter

+   * Getting to know the 2.6 kernel
+   * Improvements to desktop performance
+   * Improvements in laptop support
+   * Improvements to server performance
+   * Improvements in hardware support
+   * Using the 2.6 kernel beyond Fedora Core 3

When the Linux kernel is working well, it should be almost invisible to the people using Linux. External devices should be detected and configured automatically. Applications should be able to read and write data from storage devices, communications cards or any other types of supported hardware. By most accounts, the new 2.6 kernel included with Fedora Core 3 does those jobs well and provides a solid foundation for continued growth of Linux.

The focus of this chapter is on improvements in the 2.6 kernel that relate to how you might use it in Fedora Core 3. For that reason, I’ve broken down descriptions of the 2.6 kernel in much the same way I divided up the book: desktop, server, and administrative features (in this case, represented by a section on supported hardware drivers). After that, I describe features in the 2.6 kernel that relate to how it can be used outside of Fedora Core 3.

# Familiarizing Yourself with the Kernel

The Linux kernel is the software that allows application programs to communicate with the computer hardware and coexist with other running applications on the same system. To do that, the kernel must:

+   * **Know about the hardware drivers on the computer** — In Linux, the code that lets applications communicate with each piece of computer hardware can either be built into the kernel as drivers or added to the kernel after it is running, using what are called loadable modules.
+   * **Be able to manage applications** — By performing scheduling functions, the kernel can decide which running processes have access to the computer’s processor and for what