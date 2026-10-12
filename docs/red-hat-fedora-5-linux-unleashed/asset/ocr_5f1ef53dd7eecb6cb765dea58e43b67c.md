# Console-Based Printer Configuration Quickstart

Local or remote print services can also be configured locally or on a server without the X Window System. To do so, you use Fedora's text-based `system-config-printer-tui` printer configuration utility. You have to run this command as root:

```
# system-config-printer-tui
```

The screen clears after you press Enter, and you will see the command's main dialog. (You see this screen in the section titled "Console-Based Print Commands," which can be found in Chapter 23, "File and Print.")

> **NOTE**
> If you launch `system-config-printer` as root when not using X at a console, the `system-config-printer-tui` interface is used.

You use the Tab key and spacebar to navigate the dialogs and expand lists of devices. You can create a new printer entry by highlighting the New button and pressing Enter. Use the Up or Down cursor keys to select and highlight an existing entry; then highlight the Edit button and press Enter to edit a previously defined printer.

You can then print documents from the command line using the `lpr` command, view any active jobs using the `lpq` command, and control the print queue by using the `lprm` command.

# Managing Printing Services

After defining a printer, you can use the command line to view and control your print jobs, or if root, all print jobs and printers on your system. Table 12.1 contains a partial list of CUPS and related printing commands and drivers included with Fedora.

| TABLE 12.1 Print-Related Commands and Drivers |
| Name | Description |
| a2ps | Formats text files for PostScript printing |
| accept | Controls CUPS print job destinations |
| cancel | Cancels a CUPS print job |
| disable | Controls CUPS printers |
| dvi[lj, lj4j, lj2p, lp4] | Converts TeX DVI files to specific PCL format |
| enable | Controls CUPS printers |
| enscript | Converts text files to PostScript |
| escputil | Epson Stylus inkjet printer utility |
| groffbp | groff driver for Canon LBP-4 and LBP-8 laser printers |
| gs | The Ghostscript interpreter |
| gsob[5,500, lp] | Ghostscript Bubblejet printer drivers |
| gsd[5,500, lj, lp] | Ghostscript Deskjet printer drivers |
| lpadmin | CUPS command-line based printer utility |