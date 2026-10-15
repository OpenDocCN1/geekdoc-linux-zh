# Managing Printing Services

After defining a printer, you can use the command line to view and control your print jobs, or if root, all print jobs and printers on your system.

Table 12.1 contains a partial list of CUPS and related printing commands and drivers included with Ubuntu.

# TABLE 12.1 Print-Related Commands and Drivers

| Name | Description |
|------|-------------|
| a2ps | Formats text files for PostScript printing |
| accept | Controls CUPS print job destinations |
| cancel | Cancels a CUPS print job |
| dvi[l], lja1, lj2p, lj4 | Converts TeX DVI files to specific PCL format |
| encscript | Converts text files to PostScript |
| escputil | Epson Stylus inkjet printer utility |
| gro1bp | groff driver for Canon LBP-4 and LBP-8 laser printers |
| gs | The Ghostscript interpreter |
| gsbj[dj500, lp] | Ghostscript BubbleJet printer drivers |
| gsdj[dj500, lj, lp] | Ghostscript DeskJet printer drivers |
| lpadmin | CUPS command-line-based printer utility |
| lp | Starts a CUPS print job |
| lpc | A Berkeley-subset CUPS printer control client |
| lpf | General printer filter |
| lprm | A Berkeley-compatible CUPS job queue utility |
| lpstat | Displays CUPS print jobs and printer status |
| mpage | PostScript text formatting utility |
| pbm[2ppa, page, to10x, toep son, topp a, toptx] | Portable bitmap conversion utilities |
| pr | Text formatting command |
| psmandup | Duplex printing utility for non duplex printers |
| reject | Controls CUPS print job destinations |
| setup | Launches printer configuration tool |
| smbclient | SMB print spooler |
| smbprint | SMB print shell script |
| smbspool | SMB printer spooler |
| thinkjettopbm | Portable bitmap to ThinkJet printer conversion utility |

Most Linux systems use PostScript as the default document format for printing. Ubuntu uses the gs command along with CUPS to manage local and remote print jobs and the type of data transferred during a print job. The gs command is used to translate the document stream into a format accepted by the destination printer (which most likely uses HPCL).