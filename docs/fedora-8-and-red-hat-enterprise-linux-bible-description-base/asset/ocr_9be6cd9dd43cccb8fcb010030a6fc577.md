![](bbox=[0.17, 0.1, 0.83, 0.52])

**Figure 5-6:** Virtual Machine Manager (virt-manager) lets you install and run guest operating systems.

# Running applications virtually with KVM and QEMU

As with Xen, Kernel-based Virtual Machine (KVM) virtualization requires a computer that has either an Intel VT or AMD-V processor. KVM, however, is implemented using a loadable kernel module (kvm.ko) that works with the standard kernel, instead of using a special Xen kernel. QEMU (www.qemu.org) is used to ultimately run the guest operating systems.

Within each virtual machine running under KVM is private, virtualized hardware that provides you with access to local hard disks, network interface cards, and other hardware resources. Some of the requirements for beginning with KVM virtualization are the same as they are for Xen:

+   * You need at least about 256MB of RAM for each guest.
+   * For hard disk space, you probably need between 2GB and 3GB at least for each guest system (judging from an average-size Fedora desktop install).
+   * You need to have the GRUB bootloader installed.