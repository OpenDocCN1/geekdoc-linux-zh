Although people who use CentOS casually rarely see a need for lots of *partitions*, those who maintain and have to recover large systems are thankful when the system they need to fix has several partitions. Multiple partitions can localize deliberate damage (such as denial-of-service attacks), problems from errant users, and accidental file system corruption.

# ## Using the GRUB Boot Loader

A boot loader lets you choose when and how to boot the bootable operating systems installed on your computer's hard disks. GRUB is the only boot loader offered for you to configure during CentOS installation. The following sections describe the GRUB boot loader.

With multiple operating systems installed and several partitions set up, how does your computer know which operating system to start? To select and manage which partition is booted and how it is booted, you need a boot loader. The boot loader that is installed by default with CentOS is called the *Grand Unified Boot loader* (GRUB).

GRUB is a GNU software package (**www.gnu.org/software/grub**) that replaced LILO as the only boot loader available in CentOS. GRUB offers the following features:

+   
+   - Support for multiple executable formats
+   - Support for multitboot operating systems (such as CentOS, Red Hat Enterprise Linux, Fedora, FreeBSD, NetBSD, OpenBSD, and other UNIX-like systems)
+   - Support for non-multitboot operating systems (such as Windows 95, Windows 98, Windows NT, Windows ME, Windows XP, Windows Vista, and OS/2) via a chain-loading function. *Chain-loading* is the act of loading another boot loader (presumably one that is specific to the proprietary operating system) from GRUB to start the selected operating system.
+   - Support for multiple file system types
+   - Support for automatic decompression of boot images
+   - Support for downloading boot images from a network
+   

For more on how GRUB works, type **man grub** or **info grub**. The *info* command contains more details about GRUB. Or, see the GRUB wiki: **http://grub.enbug.org**.

When you install CentOS, information needed to boot your computer (with one or more operating systems) is automatically set up and ready to go. Simply restart your computer. When you see the boot message, press the `[Enter]` key (quickly, before it times out) and the GRUB boot screen appears (it says GRUB at the top and lists bootable partitions below it). Then you can do one of the following:

+   
+   - **Default** — If you do nothing, the default operating system will boot automatically after a few seconds.
+   - **Select an Operating System** — Use the up and down arrow keys to select any of the operating systems shown on the screen. Then press `[Enter]` to boot that operating system.
+