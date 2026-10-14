
You can configure printing services using the system-config-printer-gui graphical interface. Most of the detailed information in this chapter refers to the use of the GUI. The overview sections that follow, however, give you a solid foundation in both configuration approaches. You learn the details of these processes in later sections of the chapter.

## GUI-Based Printer Configuration Quickstart

Configuring a printer for Ubuntu is easy but you must use root permission to do it. Make sure that the cupsd daemon is installed and running. If you elect to use printing support when you install Ubuntu, the daemon and related software will be installed. If you're not sure whether cupsd is running, you can quickly drop to a terminal and use the /etc/init.d/cupsys command with the status keyword like so:

```
$ sudo /etc/init.d/cupsys status
```

You will see either

```
Status of Common Unix Printing System: cupsd is not running.
```

or, if cupsd is running, an acknowledgement such as

```
Status of Common Unix Printing System: cupsd is running.
```

If cupsd is installed but not running, start the daemon like so:

```
$ sudo /etc/rc.d/init.d/cups start
```

To access the GUI select System, Administration, Printing.

You then simply follow the prompts to define your printer and add local or remote printing services. You should print a test page before saving your changes. Use the printer configuration client or the File menu's Print menu item from a GNOME or KDE client.

> NOTE
> The system-config-printer utility is a replacement for gnome-cups-manager, which was previously the default printer configuration tool for Ubuntu. This new utility was actually originally developed for Fedora and has been adopted by Ubuntu.

## Managing Printing Services

After defining a printer, you can use the command line to view and control your print jobs, or if root, all print jobs and printers on your system. Table 8.1 contains a partial list of CUPS and related printing commands and drivers included with Ubuntu.

### TABLE 8.1 Print-Related Commands and Drivers

| Name | Description |
|------|-------------|
| a2ps | Formats text files for PostScript printing |
| accept | Controls CUPS print job destinations |
| cancel | Cancels a CUPS print job |
| disable | Controls CUPS printers |
| dvi[lj, ij4l, lj2p, ij4] | Converts TeX DVI files to specific PCL format |
| enable | Controls CUPS printers |
| enscript | Converts text files to PostScript |
| escputil | Epson Stylus inkjet printer utility |
| groplb | groff driver for Canon LBP-4 and LBP-8 laser printers |
| gs | The Ghostscript interpreter |
| gsbj[dj500, lp] | Ghostscript BubbleJet printer drivers |
| gsdj[dj500, ij, lp] | Ghostscript DeskJet printer drivers |
| lpadmin | CUPS command-line-based printer utility |
| lp | Starts a CUPS print job |
| lpc | A Berkeley-subset CUPS printer control client |
| lpf | General printer filter |
| lprm | A Berkeley-compatible CUPS job queue utility |
| lpstat | Displays CUPS print jobs and printer status |
| mpage | PostScript text formatting utility |
| pbm[2ppa, page, to10x, toepson, toppa, toptx] | Portable bitmap conversion utilities |
| pr | Text formatting command |
| psmandup | Duplex printing utility for nonduplex printers |
| reject | Controls CUPS print job destinations |
| setup | Launches printer configuration tool |
| smbclient | SMB print spooler |
| smbprint | SMB print shell script |
| smbspool | SMB printer spooler |
| thinkjettopbm | Portable bitmap to ThinkJet printer conversion utility |

Most Linux systems use PostScript as the default document format for printing. Ubuntu uses the gs command along with CUPS to manage local and remote print jobs and the type of data transferred during a print job. The gs command is used to translate the document stream into a format accepted by the destination printer (which most likely uses HPCL).

You can use the Ghostscript interpreter gs to display its built-in printer devices by using the gs interpreter with its --help command-line option like this:

```
# gs --help
```
