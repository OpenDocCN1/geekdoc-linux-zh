We will not cover LILO in detail, because it is already well documented, is no longer the de facto bootloader of choice, and is intended only for x86 PC-type systems with a PC BIOS.

# # GRUB

The GRand Unified Bootloader (GRUB) is the main bootloader for the GNU project, and it is also the most popular Linux bootloader on x86 systems these days. It is used by all the major "Enterprise Linux" distributions on the server and is fairly common on embedded x86 "PC" based boards, too. If you are developing an embedded Linux system that is based substantially upon standard PC hardware (and is perhaps, therefore, also already running a major distribution), GRUB is your friend, not U-Boot.

Erich Boley originally wrote GRUB in the course of finding an appropriate bootloader for what would later be known as GNU Mach. Erich's work was later picked up by Gordon Matzigkeit and Okuji Yoshinori, who continue to maintain and develop GRUB. The project's website is located at http://www.gnu.org/software/grub. There you will find the GRUB manual, which discusses the package's use extensively. Though GRUB's code can be retrieved using CVS, the latest stable releases are also tar-gzipped and made available for download through the project's website.

One aspect of GRUB's capabilities you may find helpful during development is its ability to boot over the network using TFTP and BOOTP or DHCP. You will also find that its ability to recognize several standard file systems (including tab completion of filename paths) simplifies testing without making persistent configuration changes.

You can find out more about GRUB by visiting the website and by experimenting with any x86 desktop or server Linux system.

# # loadlin

loadlin, maintained by Hans Lermen, is a Microsoft MS-DOS-compatible utility that can load Linux from an already running MSDOS, Windows 3.x, Windows 95, 98, or ME system (but not from NT, XP, Windows 2000, Windows 2003, VISTA, or others based upon the Microsoft NT kernel). We mention it for completeness, but strongly discourage using loadlin in any new designs, because it has not been updated in many years and is not compatible with newer Microsoft operating systems. However, you may find loadlin useful in very limited circumstances.

# # Coreboot (Formerly the LinuxBIOS)

Coreboot is a complete PC BIOS replacement, also available on PowerPC systems. Coreboot boots Linux from ROM, which requires that Linux then perform the initial system bringup, interrupt-routing assignments, device initialization, and so forth. When Linux takes over these roles, the software used is called LinuxBIOS.