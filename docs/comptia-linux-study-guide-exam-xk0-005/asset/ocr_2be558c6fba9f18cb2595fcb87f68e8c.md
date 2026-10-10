an outdated/incorrect driver (PPD) or a bad connection. Start by checking the kernel ring buffer with `dmesg` and taking a look at the printer error log files, such as `/var/log/cups/error_log`.

![](bbox=[0.17, 0.26, 0.27, 0.33])

**NOTE** Don’t buy a doostop. Make sure the printer your company is interested in purchasing is already supported by Linux. There are several websites that can help, such as www.openprinting.org/printers and tldp.org/ HOWTO/printing-HOWTO/printers.html. In addition, use your favorite search engine and enter `Linux compatible printers` to find more.

If the printer was recently installed, check its configuration. You can do this via a web browser, if available, on the system by entering **127.0.0.1:631** in the address bar. If your system does not have a GUI, you can look through the `/etc/cups/printers.conf` file to review the printer’s configuration.

Determine how the printer connects to the system. Is it a network printer? Does it attach via a USB cable? Is the printer directly connected into a parallel port? If it is a network-connected printer, first check that the network is operational. If the printer is attached with a USB cable, start by troubleshooting the USB connections (covered later in this chapter). If it uses a parallel port on your system, it may be a bad adapter. If possible, consider switching it to a different connection type, such as USB, or obtaining a new printer with a more modern configuration.

Check if the printer’s PostScript Printer Definition (PPD) file or driver needs updating. Go to the manufacturer or open source driver website to determine if an update is available. You can view all the currently available printer drivers on your system using the `lpinfo -m` command. Keep in mind the problem may involve a needed printer firmware update, so check for those as well.

![](bbox=[0.16, 0.76, 0.27, 0.83])

**NOTE** Some manufacturers provide their own Linux tools to assist in printer troubleshooting. For example, Hewlett Packard offers the `hp-info` and `hp-toolset` utilities to help in managing and problem-solving their printers’ issues.

**Video** Hardware issues with video show up in sluggish displays, audio lag, glitches on the screen, and so on. You may even see a black screen or receive no audio output. Some problems can even cause the system to crash or hang.

As with many other hardware problems, first check the kernel ring buffer (`dmesg`) and video log files. If your system is still using X11, check the journal file or the `/var/log/Xorg.0.0.log` file. If you are employing Wayland, check the journal file via the `journalctl` command.