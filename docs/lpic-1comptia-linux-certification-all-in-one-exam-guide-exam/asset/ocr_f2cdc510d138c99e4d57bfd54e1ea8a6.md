If your printer isn't PostScript compatible, you use CUPS filters to convert print jobs from PostScript into the appropriate format using the PDL of the printer to which they are being sent. These filters are located in `/usr/lib/cups/filter`.

The next components you need to know about are the CUPS backends. Backends are responsible for providing the interface between the scheduler and the actual printer hardware. The CUPS backends are located in `/usr/lib/cups/backends`. CUPS provides backends for a variety of different printer interfaces, including parallel, serial, USB, and so on. Each time cupsd starts, it queries each backend installed on the system. The backends respond to the daemon, reporting whether or not a printer is connected. If a printer is connected, they report information about the printer, such as the make and model.

The next CUPS components you need to be familiar with are the PPD (PostScript Printer Description) files. PPDs are used by cupsd to determine the capabilities of your printer. These PPD files are stored in `/etc/cups/ppd`.

The last CUPS component you need to be familiar with is the web-based administration utility. The CUPS scheduler provides the web-based administrative interface. The CUPS administration utility can be used to set up printers and manage print jobs. To access the CUPS web-based administration utility, just open a web browser and navigate to `http://your_server_address:631`. When you do, the screen in Figure 16-1 is displayed.

When a print job is submitted to a CUPS server, the process depicted in Figure 16-2 occurs.

![](bbox=[0.08, 0.46, 0.79, 0.91])