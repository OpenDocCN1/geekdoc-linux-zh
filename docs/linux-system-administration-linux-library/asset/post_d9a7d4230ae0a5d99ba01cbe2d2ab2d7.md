
USB interfaces, so there should be no trouble using these printers via more capable interfaces, at least from the printer's side of things. There are two situations in which you might be forced to use an RS-232 port:

- depletion on the computer Most x86 computers have one parallel port. If you're using it for one printer, you may need to use an RS-232 port for a second printer. You can buy add-on-parallel-port cards for such situations, unless you want to connect many printers to one computer or cannot add a card for some reason, you can usually work around a lack of parallel ports.

- Old serial-only printers A few printers don't include parallel, USB, or Ethernet ports. Fortunately, such printers are usually PostScript models, so they're not badly impacted by RS-232's speed problems as are non-PostScript models.

## In Sum

The RS-232 serial port is a low-speed but very flexible means of interfacing computing equipment. It can be used to link two computers together (directly or through a modem), to connect dumb terminals to a computer, or to interface a printer to a computer. Linux's support for these functions is quite good, but it relies on a large number of additional software packages, such as ppp for PPP links, getty for login access, and the printing system for printers. Understanding these tools is vital for using RS-232 serial ports under Linux.

USB is a recent port standard that surpasses the old RS-232 standard in many ways, including speed and flexibility. Many devices are available in USB interfaces, ranging from mice to scanners to disk drives. Linux's support for USB is still new, with the 2.4.x kernels it is good enough to allow you to use many of these devices. If you're using a Linux distribution that doesn't include either the 2.4.x kernel or a version of the 2.2.x kernel that's been patched with USB support, however, you'll need to upgrade the kernel to use USB devices.

## Printers and the Spooling Subsystem

Printers are critical tools for most businesses, and that makes the ability to set up and administer printing a very important system administration task. You will find that many of the emergency calls you receive are from users who cannot print a document they need for an upcoming meeting. Even when something small goes wrong with a printer, it seems like a crisis to anyone that printer at that specific time. A successful system administrator must understand the printing process and be able to successfully troubleshoot basic printing problems.

Printing under Linux works differently than printing under most non-Unix OSs. If all works well, these differences are transparent to your users, but you must understand many of Linux's printing details and peculiarities in order to set up and troubleshoot a Linux printing queue. You must also understand how these queues interact with clients if the computer functions as a print server for other computers. This chapter outlines the types of printers commonly used today, the tools Linux provides for controlling printer operation, and basic installation and configuration.

## Printer Basics

Printers are classified both by the way they print and the way they connect to the computer. There are three main types of printers and four types of printer interfaces you may encounter. Familiarity with these printer basics makes you a more capable system administrator and helps your users to trust that you know what you are doing. Brief introduction to types of printers and the ways they interface the computer will be helpful. If you already know the basics, you can skip ahead to “The Printing Process in Linux.”

## Chapter 13 Printers and the Spooling Subsystem

## Types of Printers

Printers differ radically in the way they create images on paper. Impact printers effectively strike characters against inked ribbons to transfer an image to paper. These have limited and specialized uses in today's business world; more common are inkjet printers by other means. Impact printers include line printers, daisy-wheel printers, and dot-matrix printers. Nonimpact printers include laser printers and ink-jet printers. Some of the earliest common printers for mainframe computers were line printers—big, fast, and noisy. Daisy-wheel printers were introduced in 1970, offering the same print quality as typewriters. Soon after, the dot-matrix printer hit the scene in 1975 but the cost was prohibitive, most businesses continued to use dot-matrix printers. In 1986, Hewlett-Packard released the DeskJet the first ink-jet printer came out, it was too cost-prohibitive. In 1988, priced at $1000. Many users kept their dot-matrix printers instead of paying for the better capability, series of printers opened the door to widespread use of ink-jets by home users. Laser printers were still too expensive and didn’t do color like the ink-jets. In 1992, Hewlett-Packard introduced the LaserJet 4, which supported resolutions up to 600 × 600. Color laser printers were introduced in 1994. The market is pretty much between ink-jet and laser printers. There are, however, a few printer types that are important in niche markets, such as sublimation and thermal wax printers, which are popular in graphics departments.

## Dot-matrix Printers

Dot-matrix impact printers have a number of pins (usually between 9 and 24) arranged in a vertical line. The printer shoots some of them into an inked ribbon, leaving a number of dots on the paper, which produces a fuzzy, low-quality representation of the intended letter. The fuzziness is due to the mechanical nature of the pins; they simply cannot be small enough to hide the fact that the letters are made of dots. To its advantage, however, this type of printer first introduced the possibility of printing graphics since it was not restricted to letters like the daisy-wheel printers that preceded dot-matrix models in the marketplace.

Today, dot-matrix printers are rare because they are slow, noisy, and produce lower-quality print than competing ink-jet and laser printers. Nonetheless, they cling to life in certain applications. The primary advantage of these printers is, that they rely upon impact technology, they can print multi-part forms. You'll therefore see dot-matrix printers in we use in some retail establishments for printer receipts and invoices.

Linux support for dot-matrix printers is quite good. A handful of printer languages, led by Epson's ESC/P, have long dominated the dot-matrix market, and Linux's Ghostscript supports these common dot-matrix printer languages. Therefore, if you find yourself needing to support a dot-matrix printer, chances you can get it from Linux.

## Ink-Jet Printers

Whereas dot-matrix printers rely on impact through an inked ribbon to create images on the page, ink-jet printers shoot small drops of ink through nozzles onto the page. Like the pins of a dot-matrix printer head, ink-jet nozzles can be arranged to form characters or other images but smaller dots that are easily discerned as such. The printing mechanism moves horizontally as the page is slowly drawn by the printer. Early models produce dots large enough that the print quality was on a par with that of dot-matrix printers, but the technology quickly improved to the point where the laser printers rival image quality.

Generally cheaper to buy than laser, ink-jet printers are more expensive to maintain. The system contains 1-6 ink cartridges, which have to be replaced or refilled when empty. (Each cartridge produces 1-3 colors; all modern ink-jets are color printers, although the earliest models printed only black.) These cartridges can be expensive and may print only a few pages before replacement, leading to high per-page costs. Ink-jet printers work best with specially coated paper that prevents the ink from spreading as it dries. Care should be taken when removing a printed sheet from an ink-jet printer, the ink will smear unless it allowed sufficient time to dry. Regular printer paper may be used, but the image is often blurred by the ways of ink soak into

> NOTE You can refill ink for popular ink-jet printer models. These kits can greatly reduce the cost of printing, but refilling can be a messy process and doesn't always work correctly. Printer manufacturers discourage this process, and they may refuse warranty service if they discover you've been refilling, although refillers claim any such action is illegal. To the best of our knowledge, this claim has never been tested in court.

## Laser Printers

Laser printers offer the best print quality. Introduced commercially by Hewlett-Packard in 1984, they have come to dominate the office market as their price has fallen compared to other printer types. A laser printer transfers a full-page to paper electrostatically, much like a photocopier. While a photocopier copies by copying the image from its source photographically, a laser printer begins with computer data, which the printer's is
