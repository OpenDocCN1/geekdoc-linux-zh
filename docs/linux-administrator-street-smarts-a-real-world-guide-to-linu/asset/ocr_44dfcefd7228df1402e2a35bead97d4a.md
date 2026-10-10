some SATA disks, is to change from an ATA driver to an SATA driver or vice versa. Drivers for both disk classes are available for some SATA controllers, so you may be able to switch. If you try this, though, be aware that your disk identifiers will change. This means you'll need to edit entries in /etc/fstab, and you may need to adjust your boot loader configuration as well. If something goes wrong in your change, your system may be rendered unbootable, so be ready with an emergency recovery disk.

# Criteria for Completion

To complete this task, you should have correctly identified all your computer's hard disks. (Many computers have a single hard disk, although they may have removable disk devices.) You should also have checked your hard disks' performance with hdparm. If that performance is unacceptably low and if it's an ATA disk, you should try to improve it via hdparm and, if necessary, add an appropriate line to a startup script to make that change persistent when you reboot the computer.

# Task 2.6: Configure and Compile a Kernel

The Linux kernel is the heart of a Linux system. Indeed, in a technical sense, the word Linux applies only to the kernel; everything else--shells, disk utilities, compilers, and other programs--are programs that happen to run well on the Linux kernel. The kernel itself provides an interface between your hardware and the rest of these programs. It also provides important system services, such as process management. Ideally, if the kernel works well, you never notice it; but if it's misconfigured or buggy, the kernel can cause serious problems indeed.

Kernel configuration is an important system administration task because it enables you to add support for new hardware and to optimize the kernel for your hardware and your needs. A properly tuned kernel can help a system run at its most efficient.

![](bbox=[0.15, 0.68, 0.22, 0.74])

> Most distributions ship with kernels that include support, usually in the form of kernel modules, for a wide variety of hardware. Thus, you probably don't need to recompile your kernel just to add support for a new hardware device you've just bought. You might need to recompile the kernel to support particularly exotic hardware, though, and recompiling the kernel can slightly improve system performance.

# Scenario

You've heard that the latest Linux kernel provides faster and more reliable support for your Ethernet hardware than is available with the Linux kernel you're running. To take advantage of this improvement, you want to compile a new kernel.