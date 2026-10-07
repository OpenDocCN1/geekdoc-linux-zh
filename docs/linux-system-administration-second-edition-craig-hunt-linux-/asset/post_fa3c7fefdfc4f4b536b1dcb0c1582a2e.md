
backup software. Your backup schedule, of course, is yours to set.

Backing up your data is not enough. You must have a good recovery plan in case of disaster. At a minimum, you should be able to boot an emergency recovery disk of some sort in order to restore data from a backup. This same or another recovery disk should allow you to edit your main system's files, in case you accidentally damage some critical file like /etc/fstab. There are also assorted tools available to help you recover data, even without a conventional system backup. All of these tools and techniques play an important role in safeguarding your system's data from accidental loss, or even from sabotage by a cracker.

Take a break and obtain your beverage of choice. When you return you'll learn about printers and the spooling subsystem.

## Part III: Communications and Networking

### Chapter List

- Chapter 10: Printers and the Spooling Subsystem
- Chapter 11: Serial Communications, Terminals, and Modems
- Chapter 12: TCP/IP Linux Networking
- Chapter 13: The X Window System
- Chapter 14: Setting Up Your Mail Server

### Featuring

- Understanding serial devices
- Configuring terminals and modems
- Configuring serial printers
- The printing process in Linux and the lpd print spooler
- Creating printers in Red Hat
- Kernel support for printing
- Remote printing
- Bash shell scripting
- Administrative scripting in other languages
- Understanding and configuring TCP/IP networking
- File sharing
- Internet servers and super servers
- Configuring the X Window System
- Building a user interface atop X
- Setting up a mail server
- Protecting against spam

246

# Chapter 10: Printers and the Spooling Subsystem

## Overview

Printers are critical tools for most businesses, and that makes the ability to set up and administer printing a very important system administration task. You will find that many of the emergency calls you receive are from users who cannot print a document they need for an upcoming meeting. Even when something small goes wrong with a printer, it seems like a crisis to anyone who needs that printer at that specific time. A successful system administrator must understand the printing process and be able to successfully troubleshoot basic printing problems.

Printing under Linux works somewhat differently than does printing under most non-Unix operating systems. If all works well, these differences are transparent to your users, but you must understand many of Linux's printing details and peculiarities in order to set up and troubleshoot a Linux printing queue. You must also understand how these queues interact with clients if the computer functions as a print server for other computers. This chapter outlines the types of printers commonly used today, the tools Linux provides for controlling printer operation, and basic installation and configuration.

## Printer Basics

Printers are classified both by the way they print and the way they connect to the computer. There are three main types of printers and four types of printer interfaces you may encounter. Familiarity with these printer basics makes you a more capable system administrator and helps your users to trust that you know what you're doing. A brief introduction to types of printers and the ways they interface with the computer will be helpful. If you already know these basics, you can skip ahead to "The Printing Process in Linux."

### Types of Printers

Printers differ radically in the way they create images on paper. Impact printers mechanically strike characters against inked ribbons to transfer an image to paper. These have limited and specialized uses in today's business world; more common are nonimpact printers, which transfer images by other means. Impact printers include line printers, daisy-wheel printers, and dot-matrix printers. Nonimpact printers include laser printers and ink-jet printers. Some of the earliest common printers for mainframe computers were line printers-big, fast, and noisy. Daisy-wheel printers were introduced in 1970, offering the same print quality as typewriters. Soon after, the dot-matrix printer effectively replaced the daisy-wheel. Laser printers hit the scene in 1975 but the cost was prohibitive, so most businesses continued to use dot-matrix printers. In 1976 when the first ink-jet came out, it too was cost-prohibitive. In 1988, Hewlett-Packard released the DeskJet ink-jet printer, which was priced at $1,000. Although many users kept their dot-matrix printers instead of paying for the better capability, this series of printers opened the door to widespread use of ink-jets by home users. Laser printers were still far too expensive and didn't do color like the ink-jets. In 1992, Hewlett-Packard introduced the LaserJet 4, which supported resolutions up to 600×600. Color laser printers were introduced in 1994. The market now is pretty much shared between ink-jet and laser printers. There are, however, a few printer types that are important in niche markets, such as dye sublimation and thermal wax transfer printers, which are popular in graphic arts departments.

### Dot-Matrix Printers

Dot-matrix impact printers have a number of pins (usually between 9 and 24) arranged in a vertical line. The printer shoots some of them into an inked printer ribbon, leaving a number of dots on the paper, which produces a fuzzy, low-quality representation of the intended letter. The fuzziness is due to the mechanical nature of the pins: they simply cannot be made small enough to hide the fact that the letters are made up of dots. To its advantage, however, this type of printer first introduced the possibility of printing graphics since it was not restricted to letters like the daisy-wheel printers that preceded dot-matrix models in the marketplace.

Today, dot-matrix printers are rare because they're slow, noisy, and produce lower-quality print than competing ink-jet and laser printers. Nonetheless, they cling to life in certain applications. The primary advantage of these printers is that, because they rely upon impact technology, they can print multipart forms. You'll therefore see dot-matrix printers in use in some retail establishments for printing receipts and invoices.

Linux support for dot-matrix printers is quite good. A handful of printer languages, led by Epson's ESC/P, have long dominated the dot-matrix market, and Linux's Ghostscript utility supports these common dot-matrix printer languages. Therefore, if you find yourself needing to support a dot-matrix printer, chances are you can get it working from Linux.

### Ink-Jet Printers

Whereas dot-matrix printers rely on impact through an inked ribbon to create images on the paper, ink-jet printers shoot small drops of ink through nozzles onto the page. Like the pins of a dot-matrix print head, ink-jet nozzles can be arranged to form characters or other images but create smaller dots that are less easily discerned as such. The printing mechanism moves horizontally as the paper is slowly drawn through the printer. Early models produced dots large enough that the print quality was on a par with that of dot-matrix printers, but the technology quickly improved to the point where the images rival laser printers in image quality.

Generally cheaper to buy than laser printers, ink-jet printers are more expensive to maintain. The system contains 1–6 ink cartridges, which have to be replaced or refilled when empty. (Each cartridge produces 1–6 colors; all modern ink-jets are color printers, although the earliest models printed only black.) These cartridges can be quite expensive and may print only a few pages before requiring replacement, leading to high per-page costs. Ink-jet printers work best with specially coated paper that prevents the ink from spreading as it dries. Care should be taken when removing a printed sheet from an ink-jet printer, since the ink will smear unless it is allowed sufficient time to dry. Regular printer paper may be used, but the image is often slightly blurred by the way the drops of ink soak into it.

**Note** You can buy ink refill kits for most popular ink-jet printer models. These kits can greatly reduce the cost of printing, but refilling can be a messy process and doesn't always work correctly. Printer manufacturers discourage this process, and they may refuse warranty service if they discover you've been refilling, although refill manufacturers claim any such action is illegal. To the best of our knowledge, this claim has never been tested in court.

### Laser Printers

Laser printers offer the best print quality. Introduced commercially by Hewlett-Packard in 1984, they have come to dominate the office market as their price has fallen compared to other printer types. A laser printer transfers a full-page image to paper electrostatically, much like a photocopier. But
