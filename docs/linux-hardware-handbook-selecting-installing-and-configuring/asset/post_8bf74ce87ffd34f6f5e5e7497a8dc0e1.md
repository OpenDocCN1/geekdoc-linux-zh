
## Web-Based Sources for Driver Information

Specific chapters of this book include information on popular clearinghouses for drivers for specific devices. There are a few general-purpose Web sites, as well as sites that are particularly important for specific types of devices. These include the following:

- **The Linux kernel site**
  http://www.kernel.org is the official site of the Linux kernel. You won't find non-kernel drivers on this site, but you will find the latest kernels, including development kernels. In Linux kernel development, kernels with even second numbers (such as 2.0.3 and 2.2.14) are considered stable. Kernels with odd second numbers (such as 2.1.7 and 2.3.48) are development kernels. Development kernels are at least potentially unstable, but they usually contain more drivers than stable kernels. You therefore might want to check a development kernel for new or updated drivers.

- **The Linux Hardware Components site**
  Check http://www.linux.org/hardware/components.html for a list of companies that make Linux drivers available, and a list of projects related to Linux hardware development. Some, but not all, of these links lead to new and experimental drivers that aren't present in the kernel.

- **The ALSA Project site**
  The Advanced Linux Sound Architecture (ALSA) project is dedicated to producing an alternative set of sound drivers for Linux. This project's Web site is located at http://www.alsa-project.org. The ALSA drivers are officially beta-test and therefore experimental, but in practice they're quite stable, on the whole.

- **The OSS site**
  4Front Technologies (http://www.4front-tech.com) offers a set of shareware sound card drivers for Linux. Most of these Open Sound System (OSS) drivers aren't really experimental, but they are alternatives to the usual Linux drivers.

- **The Linux USB site**
  http://www.linux-usb.org is the official home of USB development for Linux. In the 2.2.x kernels, USB support is minimal. The 2.3.x kernels include more in the way of USB support, and this site documents these developments. You can also obtain a port of the 2.3.x USB drivers to a 2.2.x kernel from this site. After 2.3.x stabilizes into 2.4.x (which is expected by the end of 2000), USB development will no doubt continue in the 2.5.x kernel series. Chances are the Linux USB site will then make 2.5.x USB drivers available for 2.4.x kernels.

- **The LinModems site**
  http://www.linmodems.org is the best site for information on, and drivers for, software modems.

- **SuSE X servers**
  SuSE develops XFree86 drivers, and usually offers these drivers from its Web site, at http://www.suse.de/en/support/xsuse/, before they're available from XFree86. As a general rule, the drivers SuSE makes available are quite stable.

- **SANE drivers**
  Linux scanner support comes from the Scanner Access Now Easy (SANE) project, which is hosted at `http://www.mostang.com/sane/`. Check here for pointers to experimental SANE drivers. The Linux USB site, mentioned earlier, also has links to SANE drivers for USB scanners.

- **Ghostscript drivers**
  Most Linux distributions ship with GNU Ghostscript, which is typically a few months behind the latest version of Aladdin Ghostscript. You can update from `http://www.cs.wisc.edu/~ghost`. You can also find information on this site about unofficial Ghostscript drivers. Another extremely useful site is `http://www.picipant.com/~gtsaylor/pht/printer_list.cgi`, a site that contains a data-base of printers, including pointers to unusual Ghostscript drivers.

With any luck, one of the preceding links will take you to the information you need. If not, check the chapter on the relevant device. I’ve included many URLs for driver development projects throughout this book.

> **CAUTION**
>
> Experimental drivers can be extremely dangerous. A bug in a driver can crash your computer, corrupt data on your hard disk, or otherwise cause serious problems. Many of the drivers you'll find at the preceding sites are quite stable, but some aren't. Exercise caution when you use any experimental driver.

### Checking with the Manufacturer

An increasing number of manufacturers support Linux, either directly by sponsoring driver development or indirectly by distributing Linux drivers written by others. Sometimes the manufacturer merely makes available drivers that already come with the Linux kernel, but other times the drivers are patched or are more recent versions than those that come with the kernel. If you're having trouble with a standard driver, it's worth trying the driver provided by the manufacturer. At the very least, it's worth checking to see if it's the same driver that comes with the kernel. If not, that might indicate a patch by the manufacturer to improve compatibility or performance.

You should check with both the board manufacturer and the chipset manufacturer; one might provide drivers, but the other might not. Appendix B, “Hardware Manufacturers,” provides contact information for many hardware manufacturers. The Web site `http://www.linux.org/hardware/components.html` also provides links to many hardware manufacturers that provide Linux drivers for their products.

![](img/860d0c38bd76c9ded976e9d1e179ef25_641_0.png)

## Using Experimental Drivers

Experimental and commercial drivers come in several basic forms:

- **Independent source code**
  Some drivers, such as the ALSA drivers, come as source code trees, independent of the main Linux kernel source code. To use these drivers, you extract their packages and compile the drivers as if they were a non-driver software package. When you type `make install`, however, the drivers install themselves in your kernel modules directory, `/lib/modules/a.b.c`, where `a.b.c` is your kernel version. You can then load the drivers as if they were normal kernel modules. This approach doesn't normally allow you to include the driver in the kernel file itself; however, you *must* use the driver as a module.

- **Kernel source tree patch**
  Some drivers come as a set of patches to the normal kernel tree. To use these drivers, you change to the Linux kernel directory and then issue a command such as `patch -p0 < patch-filename`. You then reconfigure and recompile your kernel. Depending upon the driver, you might be able to use it as a module, as part of the kernel proper, or both. Some simple driver replacements only require you to replace one or two files in the kernel source tree, rather than use a patch file.

- **Binary-only distribution**
  Some drivers, such as the shareware OSS drivers and Lucent's software modem driver, come only as binary code. These drivers normally come with an installation script and are used only as modules. They're more likely than source code drivers to break when you upgrade to a new kernel version.

- **Non-kernel drivers**
  Some devices don't use kernel drivers. For instance, XFree86 for video displays, Ghostscript for printers, and SANE for scanners all require drivers in the form of non-kernel programs. These drivers might need to be compiled directly into the relevant program, or they might work independently. Check the relevant documentation for details.

It's critically important that you read and follow the directions included with experimental or other non-standard drivers. The usual way to distribute Linux drivers is through the kernel, so separately distributed drivers are all non-standard by definition. As such, there is no standard way to apply patches. Each project is different.

## Contributing to Driver Development

Linux is a community effort. When Linus Torvalds made the earliest versions of the Linux kernel available, other programmers looked upon the software as a living thing which could grow only through their participation. Without the contributions of these many other programmers, Linux today would not be very useful. Linus Torvalds, by himself, almost certainly could not have written the drivers for the dozens of SCSI cards, Ethernet cards, sound cards, and so on
