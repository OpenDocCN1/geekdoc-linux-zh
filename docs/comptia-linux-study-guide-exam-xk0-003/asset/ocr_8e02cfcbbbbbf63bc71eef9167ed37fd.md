GRUB wasn't developed exclusively for Linux. It can be installed from, and used to boot, a wide variety of OSs. Its Web page is http://www.gnu.org/software/grub. Most Linux distributions use GRUB Legacy (version 0.97 or earlier). GRUB 2 is currently in development.

# ## Real World Scenario

# ### The 1024-Cylinder Limit

One bane of the PC world that reared its ugly head twice in the 1990s was the so-called 1024-cylinder limit. This limit is derived from the fact that the x86 BIOS uses a three-number scheme for addressing hard disk sectors. Each sector is identified by a cylinder number, a head number, and a sector number, known collectively as the sector's *CHS address*. The problem is that each of these values is limited in size. The cylinder number, in particular, is allotted only 10 bits and so cannot exceed 2$^{10}$, or 1,024, values. In conjunction with the limits for sectors and heads, this restricted addressable ATA hard disk size to 504MB in the early 1990s.

When disks larger than 504MB became common, BIOSs were adjusted with *CHS translation* schemes, which allowed them to juggle numbers between cylinders, heads, and sectors. This increased the limit to just under 8GB. A similar scheme abandeded CHS addressing for BIOS-to-disk communications but retained it for BIOS-to-software communications. This was known as *linear block addressing* (LBA) mode.

These limits never affected Linux once it had booted, because Linux could handle more than 10-bit cylinder values, and it could access disks directly using LBA mode. The Linux boot process was limited, however, because LILO (this was pre-GRUB) relied on CHS addressing via the BIOS to boot the kernel. Therefore, the Linux kernel has traditionally had to reside below the 1,024-cylinder mark.

Today, all new BIOSs include support for so-called *extended INT13* calls, which bypass the CHS addressing scheme. These BIOS support booting an OS from past the 1,024-cylinder mark on a hard disk, but only if the boot loader and OS support this feature. Recent versions of LILO and GRUB support extended INT13 calls, so new Linux distributions can be installed anywhere on a hard disk—if the BIOS supports this feature.

# Setting Global GRUB Options

The traditional location for the GRUB configuration file is /boot/grub/menu.lst. Fedora, Gentoo, and Red Hat, though, ship with a version of GRUB that uses /boot/grub/grub.conf as the configuration file. Whatever the name, the GRUB configuration file has the same basic form, as illustrated in Listing 1.1.