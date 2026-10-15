competitors' products. Sometimes a board manufacturer even removes the markings identifying a chipset and replaces them with its own.

Linux includes support for almost all the NICs on the market today, so it's difficult to pick a poor board, at least from the point of view of Linux driver support. Among PCI boards, particularly popular and well-supported products include Intel's EtherExpress line, 3COM's EtherLink XL (using the 3c905b chipset), and a variety of products using the Tulip (21x4x) chipset from DEC (now from Intel) or clones of this chipset from PNIC, Macronix, and others. Most of the inexpensive 10/100 Mbps NICs in stores today are based on Tulip clones.

# Note

> The Linux kernel included with Red Hat 6.0 includes a driver for the Tulip chipset, but this driver doesn't work with all the Tulip clones. Therefore, you might need to recompile your kernel with updated Tulip drivers if you buy such a board. These drivers are available from http://cesdis.gsfc.nasa.gov/linux/drivers/tulip-devel.html.

# Additional Hardware Tips and Recommendations

Although components such as the CPU, hard disk, and NIC are obvious concerns in building a computer, they're not the only components. Others, although perhaps not as critical, deserve mention and are described in the following sections.

# Video Cards

It's possible to operate a Linux server without its own monitor, although you need one to install Linux, and the motherboard will probably require that a video card be installed in order to run. If you want to run a Linux system in such a "headless server" configuration, you can buy the video card that's cheapest. Even an antiquated industry standard architecture (ISA) video card will work in such a situation.

If you want to use your Linux system with its own monitor and X, however, you need to get a video card that's supported by Linux—or, more precisely, by XFree86. Because the video card market changes so rapidly, it's difficult to make specific recommendations in a book. In general, though, availability of XFree86 drivers lags a generation or two behind actual video hardware, so if you buy the latest and greatest video board, you might find that it's useless under Linux, except in text mode. Boards by Matrox and ATI generally have good Linux support, as do products with S3 chipsets. You can find more information on current XFree86 driver support at the XFree86 Web site, http://www.xfree86.org. In addition, SuSE