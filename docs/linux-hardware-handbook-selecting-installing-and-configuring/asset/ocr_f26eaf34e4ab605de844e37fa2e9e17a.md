![](bbox=[0.26, 0.13, 0.68, 0.35])

# FIGURE 19.4

*SCSI generic support enables programs to access SCSI devices that don't fit into the categories of disks, CD-ROMs, or tape drives.*

# Note

> Most of these USB options aren't present in standard 2.2.x kernels. You must use a 2.3.x or later kernel or apply patches to the 2.2.x kernel in order to use theseoptions.
> 
> 2.2.x kernel patches are available from `http://www.linux-usb.org`, and the latest kernels can be found at `http://www.kernel.org` or most Linux archive FTP sites.

These kernel drivers aren't enough to get your scanner working, though; they're only enough to get programs talking to the scanner. As with printers, much of the real work of controlling the device rests with a separate program. In the case of scanners, this program is known as SANE.

# SANE Software

*Scanner Access Now Easy* (SANE) is a set of protocols and programs that enable you to access a scanner's features under Linux. In many respects, SANE is analogous to Ghostscript for printers. The goal of the SANE project is to provide a uniform interface to all scanner hardware. This goal is similar in concept to that of the TWAIN interface in the Windows world. SANE differs from TWAIN, however, in that SANE separates the low-level drivers from the user interface. TWAIN tightly integrates the two, so all programs that use a scanner use the same interface. This fact makes SANE at least potentially more cross-platform than TWAIN, and it allows for network scanning—using a scanner connected to one computer through software located on another computer.