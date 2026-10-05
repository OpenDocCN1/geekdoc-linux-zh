Some drivers reside in a library or application. Many of these devices are external to the computer itself. Examples include the following:

+   - SANE, which handles scanners

+   - Ghostscript, which converts printed output into a form that particular printers can understand

+   - X, which manages the nonkernel element that communicates more or less directly with the device hardware.

X is unusual in that it's a nonkernel element. SANE and Ghostscript, by contrast, both communicate with external hardware devices via interfaces (such as a USB port) that are handled by the kernel. That is, you need at least two drivers to handle devices. To print to a USB printer, for instance, use the kernel's USB driver and a Ghostscript printer driver. Ideally, most users will be unaware of this complexity, but you may need to understand it if problems arise.

# Locating and Installing Drivers

Most drivers come with the Linux kernel itself, or with the library or application that installs the type of hardware. For instance, most X installations include a set of video drivers that you can use video cards. For this reason, it's seldom necessary to track down and install additional drivers for common hardware. There are exceptions—for instance:

New Hardware If your hardware is very new (meaning the model is new, not just that you purchased it), it might need drivers that haven't made their way into whatever distribution you're using.

Unusual Hardware If you're using very exotic hardware, as a specialized scientific data-acquisition board, you may need to track down drivers for it.

Proprietary Drivers Some manufacturers provide proprietary drivers for their hardware. For instance, the nvidia and fgrx drivers (referred to earlier, in 'Using Common Display Hardware') can improve the performance of video displays based on NVIDIA or ATI/AMD chipsets, respectively. Some hardware requires proprietary drivers. This is particularly common for some exotic hardware.

Bug Fixes Drivers like other software, can be buggy. If you run into such a problem, you might want to track down a more recent driver to obtain a bug fix.

One way to obtain a new kernel-based driver is to upgrade the kernel. Note kernel upgrade can provide bug fixes to both existing drivers and