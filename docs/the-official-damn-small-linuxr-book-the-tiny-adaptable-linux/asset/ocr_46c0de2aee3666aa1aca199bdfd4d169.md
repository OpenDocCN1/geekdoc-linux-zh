# NOTE

Although we have not formally tested dual booting Windows Vista and DSL, there are some Windows Vista “features” that make dual booting with Linux difficult.

One issue is that Windows Vista erases the master boot record (which in our case is Grub or Lilo) when Windows Vista is installed. So you should install Windows Vista before installing Linux to not lose the Grub boot loader. The second issue is that Windows Vista uses a different version of NTFS that cannot be resized using tools in Linux or older Windows resizing tools. If you can overcome those issues, dual-booting with DSL and Windows Vista should be possible.

The Poorman’s installation is now complete. However, if your hard disk has some configuration other than those just described (either all DSL or DSL plus a single Windows system on the first partition), you probably need to edit your Grub configuration file by hand.

“How do I edit the boot options in a Frugal Grub installation?” is one of the most frequently asked questions after installation.

All Frugal type installations emulate running from a CD-ROM; to the running system, this means that the system is mounted at /cdrom. Therefore, as superuser root, you may edit Grub’s configuration file /cdrom/boot/grub/menu.lst. However, if you have booted your system with the toram boot option, you do not find this file until you mount the partition first. For example, let’s say you install to hda2 and boot with toram; as superuser, mount /mnt/hda2, if necessary, and then edit /mnt/hda2/boot/grub/menu.lst.

# Frugal Lilo CompactFlash Install

Why does this option refer to CompactFlash? I chose to name this option with CompactFlash for two reasons:

+   - For most users, the Lilo boot loader is more difficult to edit.
+   - Usually, the use of CompactFlash means one is building an appliance and therefore does not want easy access or even a boot menu option to appear.

Frugal Lilo also differs from Frugal Grub in that it does not install into the master boot record (MBR). It installs the boot loader into the target partition. You need to mark the partition as the active partition.