normally be the case. (The boot loader must not be installed in the master boot record of the whole disk or the disk will become unbootable.)

+   5. **Reboot and Alt key** — When Fedora installation is completed, reboot as instructed.
+      Hold the Alt key as the machine reboots. When you see the Boot Camp menu, select
+      Windows and the computer will boot to Fedora. Just use the default boot entry for Fedora
+      because trying to change GRUB boot labels will probably cause the computer to lock up.
+      (By the way, if you DVD gets stuck in the drive, hold down the mouse button when you
+      reboot and the DVD will eject.)

Remember that installing Fedora on an Intel-based Mac is still considered to be experimental.
The less you stray from the defaults (partitioning, boot loaders, and so on), the better chance of
getting a workable Fedora system running on your Mac.

If you run into problems, I recommend you refer to the Fedora Project's Fedora On MacIntel
page (http://fedoraproject.org/wiki/FedoraOnMacIntel). There are also resources
available from other Linux projects to get Linux to boot on Intel Mac architecture.

# ### Using the GRUB boot loader

A boot loader lets you choose when and how to boot the bootable operating systems installed
on your computer's hard disks. GRUB is the only boot loader offered for you to configure
during Fedora installation. (The LILO boot loader included with earlier versions of Fedora is
no longer included as of Fedora Core 5.) The following sections describe the GRUB boot
loader.

With multiple operating systems installed and several partitions set up, how does your
computer know which operating system to start? To select and manage which partition is
booted and how it is booted, you need a boot loader. The boot loader that is installed by
default with Fedora is called the GRAnd Unified Boot loader (GRUB).

GRUB is a GNU software package (http://www.gnu.org/software/grub) that
replaced LILO as the only boot loader available in Fedora. GRUB offers the following
features:

+   - Support for multiple executable formats.
+   - Support for multiboot operating systems (such as Fedora, FreeBSD, NetBSD, OpenBSD,
+     and other Linux systems).
+   - Support for non-multiboot operating systems (such as Windows 95, Windows 98,
+     Windows NT, Windows XP, Windows Vista and OS/2) via a chain-loading function.
+     Chain-loading is the act of loading another boot loader (presumably one that is specific
+     to the proprietary operating system) from GRUB to start the selected operating system.
+   - Support for multiple file system types.
+   - Support for automatic decompression of boot images.