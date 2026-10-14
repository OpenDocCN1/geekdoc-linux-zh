While a user can sometimes talk to a print device directly, print jobs under Linux generally run through a printer daemon. When a user sends a job to the printer daemon, the daemon spools it to a queue directory, where it waits its turn to go to the printer. Next, it passes through a print filter, and finally goes to the device itself. The filter turns the printer’s various bells and whistles (tray selection, duplex mode, and so on) on or off, and may also convert the job into a format the printer can understand—if your printer doesn’t have native PostScript support, the filter will probably include a rasterizer that interprets PostScript.

In practice, setting up a printer involves three main steps:

+   1. Installing the print filter software.
+   2. Making sure the computer can talk to the printer.
+   3. Putting it all together for the print daemon, lpd, in /etc/printcap.

Step 1 is the time-consuming part. (Sections 5.3 and 5.4 below deal with the two main kinds of filters.) At one time, Step 2 was problematic because many printers connected to the serial port, and the various port settings had to be just right (not to mention that for Step 3, you had to code all of the ioctl settings in one hexadecimal stream). Not only has this become more uniform, but serial printers are no longer common.

Before we can do much work with printers, we need to talk about the system that oversees print requests: the print daemon.

# 5.2 Print Daemons

Unfortunately, Unix has a messy set of three main print daemons, and we have to mention all of them.

# lpsched

Most System V-based machines include this. The less said about this system, the better (it has awkward queuing and obfuscated filters). However, it gets a mention because some programs try to print using its queuing programs.

# Berkeley lpd

BSD systems use this, and it’s standard on most Linux distributions. It’s an older program, but it works.

# LPRng

This new system resembles lpd, but has many enhancements and filters. Because they’re the ones found on most Linux distributions, we’ll cover only lpd and LPRng. Some distributions include a system called PLP, which you can think of as a predecessor to LPRng. Which one you choose depends mostly on the printers you have and the size of your installation.