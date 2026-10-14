
# Printer Configuration

The printer configuration tool (printtool) maintains the /etc/printcap file, print spool directories, and print filters. The filters allow you to print many different types of files, including:

- plain text (ASCII) files
- PostScript files
- TeX .dvi files
- GIF, JPEG, TIFF, and other graphics formats
- RPMs

In other words, simply printing a GIF or RPM file using the lpr command will result in the printer doing "the right thing."

![](img/46f4935125ba89e12897afbe9d77a097_223_0.png)

Figure 8-28: Print Tool

In order to create a new print queue, choose Add. Then, select what type of printer is being added. There are four types of print queues which can be configured with printtool:

- Local print queues are for printers attached to a printer or serial port on your Red Hat Linux system.
- Remote print queues are attached to a different system which you can access over a TCP/IP network.
- SMB print queues are attached to a different system which uses LAN-Manager-type (SMB) networking.
- NCP print queues are attached to a different system which uses Novell's NetWare network technology.

![](img/46f4935125ba89e12897afbe9d77a097_224_0.png)

# Figure 8-29: Selecting a Printer Type

After choosing the printer type, a dialog box requests further information about the print queue (see Figure 8-30). All types of print queues require the following information:

- **Queue Name:** What the queue will be called. Multiple names can be specified with the | (pipe) character separating entries.
- **Spool Directory:** This is the directory on the local machine where files are stored before printing occurs. Be careful to not have more than one printer queue use a given spool directory.
- **File Limit:** Maximum size print job accepted, in kilobytes (1 kb = 1024 bytes). A size of 0 indicates no limit should be imposed.
- **Input Filter:** Filters convert printed files into a format the printer can handle. Press Select to choose the filter which best matches your printer (see Figure 8-31)

In addition to configuring print queues able to print graphical and PostScript output, you can configure a text-only printer, which will only print plain ASCII text. Most printer drivers are also able to print ASCII text without converting it to PostScript first; simply choose Fast text printing when you configure the filter. Please Note: This only works for non-PostScript printers.

- **Suppress Headers:** Check this if you don't want a header page printed at the beginning of each print job.

For local printers, the following information is also required:

Printer Device: Usually /dev/lp1; the name of the port which the printer is attached to. Serial printers are usually on /dev/ttyS? ports. Note that you will need to manually configure serial parameters.

![](img/46f4935125ba89e12897afbe9d77a097_225_0.png)

Figure 8-30: Adding a Local Printer

# Figure 8-31: Configuring a Print Filter

For remote printers, the dialog box contains additional fields; fill in the following information:

- Remote Host: Hostname of the remote machine hosting the printer.
- Remote Queue: Name of the queue to print to on the remote machine.

The remote machine must be configured to allow the local machine to print on the desired queue. Typically /etc/hosts.lpd controls this.

![](img/46f4935125ba89e12897afbe9d77a097_226_0.png)

![](img/46f4935125ba89e12897afbe9d77a097_227_0.png)

Figure 8-32: Adding a Remote Printer

![](img/46f4935125ba89e12897afbe9d77a097_227_1.png)

Figure 8-33: Adding an NCP Printer

# Figure 8-34: Adding an SMB Printer

For SMB and NCP printers, fill in the following information:

- **Hostname of Printer Server:** Name of the machine to which the printer you want to use is attached.
- **IP number of Server:** The IP address of the machine to which the printer you want to use is attached; this is optional and only relevant for SMB printers.
- **Printer Name:** Name of the printer on which you want to print.
- **User:** Name of user you must login as to access the printer (typically guest for Windows servers, or nobody for Samba servers).
- **Password:** Password (if required) to use the printer (typically blank). Someone should be able to tell you this if you do not already know it.
