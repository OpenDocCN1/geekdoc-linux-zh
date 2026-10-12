**Input Filter** Filters convert printed files into a format the printer can handle. Press **Select** to choose the filter which best matches your printer.

![](bbox=[0.25, 0.2, 0.75, 0.4])

Figure 8.7: Adding a Local Printer

In addition to configuring print queue able to print graphical and PostScript output you can configure a *text-only* printer, which will only print plain ASCII text. Most printer drivers are also able to print ASCII text without converting to to PostScript first; simply make sure **Convert ASCII to PostScript** is not checked.

For *remote* printers, fill in the following information:

**Remote Host** Hostname of the remote machine hosting the printer.

**Remote Queue** Printer queue name of printer on remote machine.

The remote machine must be configured to allow the local machine to print on the desired queue. Typically /etc/hosts.lpd controls this.

For *SMB* printers, fill in the following information:

**Printer Server Name** Name of the machine to which the printer you want to use is attached.

**Printer Name** Name of the printer on which you want to print.

**Printer User** Name of user you must login as to access the printer.