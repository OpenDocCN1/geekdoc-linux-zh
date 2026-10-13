
## Command Management

Command management deals with the tools that you need to administer Linux. With the latest distributions, you can choose between CLI and GUI administration tools. Linux GUI administration tools are often less than complete. Some Linux GUI commands may override settings that you've edited into your configuration files. Also, most Linux GUI commands do not report the details of success and failure, which can be critical when you're troubleshooting a problem.

For these reasons, many experienced Linux users prefer the CLI.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_67_0.png)

> When you study Linux commands, focus on command-line interface (CLI) tools.

Linux GUI tools are based on add-ons to standard command-line utilities. So when you use a GUI tool, like Red Hat's LinuxConf, you're actually using a GUI control for different command-line utilities. Not all of LinuxConf's controls work. There are, however, a number of shortcuts built into the CLI. Linux administrators who learn these shortcuts often do their work more quickly than administrators who try to use a GUI tool.

The apparent superiority of CLI tools may not last forever, but CLI superiority is a key assumption of the Sair Linux/GNU exams.

## Hardware Compatibility

Hardware compatibility is sometimes a problem for the Linux administrator. When first released, newer hardware may not always include a Linux driver.

A special problem is the "winmodem," which is a telephone modem that substitutes Microsoft Windows driver libraries for some hardware controllers.

To deal with these issues, you need to know the kinds of hardware to avoid, alternate locations for Linux drivers, and the way Linux communicates with different types of hardware.

### Hardware Compatibility Lists

Before installing Linux on a computer, you should check two different lists. You can find the main Linux hardware compatibility list (HCL), the "Hardware-HOWTO," on the Linux Documentation Project Web site at www.linuxdoc.org. Many Linux distributors keep their own HCLs on their Web sites. These lists are more up-to-date. If you see your hardware on your distribution's HCL, you'll probably find the appropriate Linux driver packaged with the distribution.

If you don't see your hardware on the HCL, there is no need to panic. There is a way to configure just about any device that isn't in the "Linux Incompatible Hardware" section of the "Hardware-HOWTO." Many manufacturers provide Linux drivers on disk or through their Web sites. These sites may also list Linux compatible products that your hardware can emulate. For example, many network cards can emulate a NE2000 adapter, and thus can work with its Linux driver.

### Modems

One of the banes of the Linux administrator is the winmodem. A winmodem substitutes Microsoft Windows software drivers and libraries for the hardware that controls a regular modem. Because the source code for Microsoft Windows is currently unavailable, it is difficult to create Linux drivers for a winmodem.

Some Linux gurus believe that it would be wrong to try to create drivers for winmodems. Devices like winmodems, which use your computer's Central Processing Unit (CPU), affect the performance of the entire system.

Although some Linux developers have developed techniques for working with some winmodems, the prevailing attitude in the Linux community is to avoid winmodems because of the interaction with the CPU.

### Video Adapters

Another common hardware problem is the video adapter, sometimes known as the graphics card. Although you may not require graphics if you do your work at the command line, most users demand a high level of performance from video hardware.

When possible, the XFree86 project creates Linux drivers for video adapters. But this work takes time, and not all video adapter manufacturers release the design information required for a Linux driver. Although you can set up standard VGA settings on almost any card, standard 16-color VGA graphics are not enough for anyone who uses a graphical application. So before you install Linux, check the XFree86 Web site for the latest list of supported video adapters.

### Printers

The other major hardware uncertainty is printers. As shown in the "Hardware-HOWTO" on the Linux Documentation Project site, some ink- and bubble-jet printers don't have Linux drivers. However, if you have a new PostScript or generic text printer, you may be able to set it up with generic Linux drivers.

### Driver Development

There are several sources of new drivers. Many manufacturers release Linux drivers when they release a new product. Some Linux companies and nonprofit groups develop drivers under the GPL or related licenses. Many developers create their own drivers that they post on various Internet (Web and FTP) sites.

At the time of this writing, a major hole in the Linux hardware driver library includes peripherals that connect through a Universal Serial Bus (USB). This issue should be addressed, at least for keyboards, mice, and sound cards, by the release of the Linux kernel version 2.4 around the beginning of the year 2001. For the latest information, refer to the Linux USB Web site at www.linux-usb.org.

## Hardware Management

Most users don't have hardware problems when they install Linux on their computers. In general, users with the latest Linux distributions but not the "latest and greatest" hardware usually have the least amount of trouble. Choosing hardware at least a few months old generally ensures that all of the components are effectively listed on the Linux HCL, or at least have Linux drivers.

As an administrator, you're more likely to run into hardware problems. For the Sair Linux/GNU exam, you need to know about several different categories of conflicts.

Just about every part of your computer needs processing power and memory. Each component uses a specific port to ask for processing power from your CPU. While it waits for this processing power, each component stores its request and data in a dedicated address in your random access memory (RAM). If two parts of your computer try to use the same port or the same area in memory, you generally get a hardware conflict.

Ports are conceptually similar to television channels; two different pieces of hardware generally can't use the same channel.

Conceptually, the solution is fairly simple: Change the port or designate a different area in memory. But to understand how these ports and areas work, you need to know a bit about the architecture inside your personal computer.

The backbones of computer architecture are known as buses. A bus is a communication highway inside your computer. Different buses regulate communication for ISA adapters, PCI cards, and RAM. If you're using Linux with kernel 2.2 or later, the ports used on each bus may depend on the settings in a Plug-and-Play BIOS.

### ISA Bus

When you install an ISA adapter, there is potential for conflict on four different kinds of ports:

- **IRQ**—Computer components use IRQ ports to ask the CPU for processing time. Computers generally have 16 IRQ ports. Basic computer components, like keyboards, hard drives, modems, BIOS clocks, and so forth, already occupy most IRQ ports.
- **Input/output (I/O)**—I/O addresses are dedicated locations in RAM that work like a cache. For example, information that comes through a network card waits in a specific range of I/O addresses for processing.
- **Direct Memory Address (DMA)**—A DMA bypasses your CPU. For example, some sound cards have a specific DMA because they can independently process an audio file directly from a hard drive. DMA conflicts are relatively rare.
- **Shared memory address**—Adapters that can't use a DMA use a shared memory address. Adapters can use a DMA or a shared memory address but not both.

The Linux command to reconfigure Plug-and-Play ISA adapters is isapnp. For more information, refer to its man page.

### PCI Bus

When choosing a PCI adapter, consider the following three issues. First, there are fewer Linux drivers available for PCI adapters. Second, older PCI cards may not work in newer computers. Third, many PCI cards also rely on IRQ ports to communicate with the CPU, so they may conflict with your ISA cards.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_70_0.png)

> If one PCI card is more important than the others, you can improve its performance by installing it in the slot furthest from your ISA cards. Closer slots get lower priority when they compete for CPU time. PCI SCSI adapters often need higher priority slots.

### BIOS

The BIOS (Basic Input/Output System) on your motherboard is the first program that runs when you turn on your computer. It includes a routine in its read-only memory (ROM) that checks your buses for new and existing hardware.
