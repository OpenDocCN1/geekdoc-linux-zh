+   3. Change to the dosutils directory (cd \dosutils).

+   4. Run the rawrite command as follows:

```
C:> rawrite
Enter disk image source file name: D:\images\bootdisk.img
Enter target diskette drive: a:
Please insert a formatted diskette into drive A: and press -Enter- :
```

+   5. Press Enter. The image is written to the disk. Remove the disk and mark it.

# Using GRUB or LILO boot loaders

A boot loader lets you choose when and how to boot the bootable operating systems installed on your computer's hard disks. GRUB is the only boot loader that comes with the Fedora Core distribution of Red Hat Linux. Earlier versions of Red Hat Linux and the current Red Hat Enterprise Linux also include the LILO boot loader. The following sections describe both GRUB and LILO boot loaders.

# Booting your computer with GRUB

With multiple operating systems installed and several partitions set up, how does your computer know which operating system to start? To select and manage which partition is booted and how it is booted, you need a boot loader. The boot loader that is installed by default with Red Hat Linux is called the GRand Unified Boot loader (GRUB).

GRUB is a GNU software package (www.gnu.org/software/grub) that replaced the LILO boot loader by default in Red Hat Linux 7.2. GRUB offers the following features:

+   - Support for multiple executable formats.

+   - Support for Multiboot operating systems (such as Red Hat Linux, FreeBSD, NetBSD, OpenBSD, and other Linux systems).

+   - Support for non-Multiboot operating systems (such as Windows 95, Windows 98, Windows NT, Windows ME, Windows XP, and OS/2) via a chain-loading function. Chain-loading is the act of loading another boot loader (presumably one that is specific to the proprietary operating system) from GRUB to start the selected operating system.

+   - Support for multiple file system types.

+   - Support for automatic decompression of boot images.

+   - Support for downloading boot images from a network.

For more information on how GRUB works, type man grub or info grub. The info command contains more details about GRUB.