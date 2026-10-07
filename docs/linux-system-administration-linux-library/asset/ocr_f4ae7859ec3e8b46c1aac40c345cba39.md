USB interfaces, so there should be no trouble using these printers via more capable interfaces, at least from the printer's side of things. There are two situations in which you might be forced to use an RS-232 port:

+   - depletion on the computer Most x86 computers have one parallel port. If you're using it for one printer, you may need to use an RS-232 port for a second printer. You can buy add-on-parallel-port cards for such situations, unless you want to connect many printers to one computer or cannot add a card for some reason, you can usually work around a lack of parallel ports.

+   - Old serial-only printers A few printers don't include parallel, USB, or Ethernet ports. Fortunately, such printers are usually PostScript models, so they're not badly impacted by RS-232's speed problems as are non-PostScript models.

# In Sum

The RS-232 serial port is a low-speed but very flexible means of interfacing computing equipment. It can be used to link two computers together (directly or through a modem), to connect dumb terminals to a computer, or to interface a printer to a computer. Linux's support for these functions is quite good, but it relies on a large number of additional software packages, such as ppp for PPP links, getty for login access, and the printing system for printers. Understanding these tools is vital for using RS-232 serial ports under Linux.

USB is a recent port standard that surpasses the old RS-232 standard in many ways, including speed and flexibility. Many devices are available in USB interfaces, ranging from mice to scanners to disk drives. Linux's support for USB is still new, with the 2.4.x kernels it is good enough to allow you to use many of these devices. If you're using a Linux distribution that doesn't include either the 2.4.x kernel or a version of the 2.2.x kernel that's been patched with USB support, however, you'll need to upgrade the kernel to use USB devices.