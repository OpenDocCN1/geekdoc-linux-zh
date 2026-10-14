# Objective 2—Configure Printers and Queues

YaST provides printer installation and configuration functionality. To configure a printer, you need to know the following:

+   - When to Configure a Printer
+   - Required Printing Software
+   - Add a Printer
+   - Manage Print Queues with the GNOME Printers Dialog

# When to Configure a Printer

You can configure your printer at the following times:

+   - *During installation*—If you are at the Hardware Configuration dialog during installation and your automatic detection is not correct, select the Printers link or use the Change drop-down list. Note that during installation, only locally connected printers are detected automatically and listed under Printers.
+   - *After installation*—You can change your printer configuration settings from the YaST Control Center by selecting **Hardware > Printer**. You can also, as root, start the YaST Printer Configuration module directly from a terminal window with the `yast2 printer` command.

# Required Printing Software

Table 12-1 shows the packages needed to set up a print server.

| Package | Content |
|---|---|
| cups | Provides the cupsd printer daemon. |
| cups-client | Provides the command-line printing tools. |
| cups-libs | Should always be installed, because a number of programs (such as Samba) are linked against the CUPS libraries. |
| cups-drivers cups-drivers-stp | Provides the PPD files for print queues. |
| cups-SUSE-ppds-dat | Provides a pregenerated `/etc/cups/ppds.dat` file. |

**Table 12-1**

These files are installed automatically if YaST is used for printer configuration. YaST also creates the symbolic links in runlevel directories to ensure that the CUPS daemon is started automatically when booting.

Other packages required by the printing system, such as ghostscript-library, are automatically selected during a standard installation.