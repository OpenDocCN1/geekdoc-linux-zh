NT/2000, Windows 98 does not come with a boot loader such as NTLoader and therefore LILO or GRUB is necessary. Keep the following things in mind when setting up a dual-boot Windows 98 and Linux using LILO:

+   - Install Windows 98 on the first partition of your first hard disk before you install Red Hat Linux. Make sure that you have a second partition or a second disk to install Linux on.
+   - You have two choices of installing Linux: the Workstation class or the Custom class. If you install Linux using Workstation installation (see Chapter 1 for details), you have less that you need to do during Linux installation. If you do install by using a Custom installation, you must make sure that you install LILO on the MBR. The Workstation installation automatically installs LILO on MBR for you.
+   - After Linux is installed and LILO is installed on the MBR, you can boot either operating system from LILO when you next reboot.

# Booting Windows within Linux by Using VMware

The VMware products are amazing virtual machine solutions that allow you to boot another operating system while you are running one. For example, you can be on Linux and run VMware for Linux to run Windows NT/2000 on your Linux desktop. Similarly you can run VMware on Windows NT/2000 and load Linux on your Windows desktop.

VMware virtual machines are commercial products that you can freely evaluate from www.vmware.com. A license file is necessary to evaluate the product, so when you download the evaluation make sure you also fill out the evaluation form to get a temporary license file sent to you by e-mail.

When you use VMware, you’re practically setting up a machine within a machine. In other words, you are creating a virtual computer within a running computer. VMware requires that you click a button to switch on the power of the virtual computer, and then it even goes through the standard BIOS Power On Self Test (POST) process, hardware detection, and so on.