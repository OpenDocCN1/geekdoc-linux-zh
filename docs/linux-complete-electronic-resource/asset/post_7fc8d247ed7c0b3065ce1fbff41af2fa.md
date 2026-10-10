
## Non-PostScript

Failing the (larger) budget necessary to buy a PostScript printer, you can use any printer supported by Ghostscript, the free PostScript interpreter used in lieu of actual printer PostScript support. The Ghostscript Home Page (http://www.cs.wisc.edu/ghost/) has a list of supported printers and information on the status of new and experimental drivers. Note that this Page lists supported printers in the latest version of Ghostscript, while most Linux distributions can only ship a somewhat outdated version of Ghostscript because of the license. Fortunately, there is usually a prepackaged, up-to-date Ghostscript made available in each distribution’s contrib area. Please help improve the Ghostscript printer support page by reporting your successes and failures as it asks.

Adobe now have a new printer language called PrintGear. I think it’s a greatly simplified binary format language with some PostScript heritage but no PostScript compatibility. And I haven’t heard of Ghostscript supporting it. But some PrintGear printers seem to support another language like PCL, and these Printers will work with Linux (if and only if the PCL is implemented in the printer and not in a Windows driver).

## What Printers Work?

If you want to buy a printer, you can look in several places to see if it will work. The cooperatively maintained Printing HOWTO printer database (http://www.pica.net.com/~gtaylor/phl/printer_list.cgi) aims to be a comprehensive listing of the state of Linux printer support. A summary of it is below; be sure to check online for more details and information on what driver to use.

Ghostscript’s printer compatibility page (http://www.cs.wisc.edu/~ghost/printer.html) has a list of some working printers, as well as links to other pages. And Dejanews contains hundreds of “it works” and “it doesn’t work” testimonials. Try all three, and when you’re done, check that your printer is present and correct in the database (http://www.pica.net.com/~gtaylor/phl/printer_list.cgi) so that it will be listed properly in this document in the future.

## Printer Compatibility List

This section is a summary of the online version. The online version includes basic specifications, notes, links to driver information, user-maintained documentation, manufacturer Web pages, and so forth. The online version of this list is also interactive; people can and do add printers all the time, so be sure to check it as well. Finally, if your printer isn't listed, add it! Printers here are categorized into four types:

- **Perfectly** Perfect printers work perfectly—you can print to the full ability of the printer, including color, full resolution, etc. In a few cases, printers with undocumented resolution enhancement modes that don't work are listed as perfectly; generally the difference in print quality is small enough that it isn't worth worrying about.
- **Mostly** You can print fine, but there may be minor limitations of one sort or another in either printing or other features.
- **Partially** You can print but maybe not in color or only at a poor resolution. See the online listing's notes column for information on the limitation.
- **Paperweight** You can't print a darned thing; typically this will be due to lack of a driver and/or documentation on how to write one.

In all cases, since this information is provided by dozens of people, none of it is guaranteed to be correct. It should, however, be easy to corroborate from the driver Web pages and manufacturer Web sites.

And without further ado, here is the printer compatibility list:

### Brother

Perfectly: HL-10V, HL-660, HL-720, HL-760.
Mostly: HL-1050.

### Canon

Perfectly: BJ-10e, BJ-20, BJ-200, BJC-210, BJC-240, BJC-250, BJC-610, BJC-620, BJC-70, BJC-800, LBP-8II, LIPS-III.
Mostly: BJ-300, BJC-4000, BJC-4100, BJC-4200, BJC-4300, BJC-4400, BJC-7000, BJC-7004.
Partially: BJC-4550, MultiPASS C2500, MultiPASS C3500.
Paperweight: BJC-5000, LBP-460, LBP-660.

### Epson

Perfectly: ActionLaser 1100, LP 8000, LQ 850, Stylus Color, Stylus Color 400, Stylus Color 500, Stylus Color 600, Stylus Color 640, Stylus Color 850, Stylus Color II, Stylus Color IIs, Stylus Pro XL.
Mostly: Stylus Color 800, Stylus Photo 750.
Partially: Stylus Color 740.

### HP

Perfectly: 2000Cs e, 2500C, DesignJet 650C, DeskJet 1200C, DeskJet 1600C, DeskJet 1600Cm, DeskJet 400, DeskJet 420C, DeskJet 500, DeskJet 550C, DeskJet 600, DeskJet 660Cs e, DeskJet 690C, DeskJet 850C, DeskJet 855C, DeskJet 870, DeskJet 870Cx i, DeskJet 890, LaserJet 1100, LaserJet 2100, LaserJet 2100N, LaserJet 4000N, LaserJet 4L, LaserJet 5, LaserJet 5L, LaserJet 5MP, LaserJet 6L, LaserJet 6MP, LaserJet 8000, LaserJet 8100, LaserJet 5000, Mopier 320, PaintJet XL300.
Mostly: HP 660C.
Partially: DeskJet 1000C, DeskJet 670C, DeskJet 710, DeskJet 720C, DeskJet 722C, DeskJet 820C.
Paperweight: LaserJet 3100.

### IBM

Perfectly: Jetprinter 5852.

### Lexmark

Perfectly: Optra Color 1200, Optra Color 1275, Optra Color 40, Optra Color 45, Optra E, Optra E+, Optra 500, Optra S 1250.
Partially: 1020 Business, 3000, 5700, 7000.
Paperweight: 1000, 1020, 1100, 2030, 2050, 2070, 5000, 7200, Winwriter 100, Winwriter 150c, Winwriter 200.

### Minolta

Perfectly: PagePro 6, PagePro 8.

### NEC

Perfectly: P2X.
Partially: SuperScript 100C, SuperScript 1260, SuperScript 150C, SuperScript 650C, SuperScript 750C, SuperScript 860, SuperScript 870.
Paperweight: SuperScript 660i, SuperScript 660plus.

### Okidata

Perfectly: OL 410e, OL 610e/PS, OL 810e/PS, Okipage 6e, Okipage 6ex, Okipage 8c.
Mostly: Okipage 4w.
Paperweight: Okipage 8w, Okijet 2010.

### Olivetti

Perfectly: JP350S.

### Panasonic

Perfectly: KX-P1123, KX-P4440, KX-P5400, KX-P8420, KX-P8475.
Partially: KX-P6500.
Paperweight: KX-P6100, KX-P8410.

### QMS

Perfectly: 2425 Turbo EX.

### Ricoh

Perfectly: 4801, 6000.

### Xerox

Perfectly: DocuPrint C55, DocuPrint N17, DocuPrint N32.

## Which Spooling Software?

Until recently, the choice for Linux users was simple—everyone ran the same old lpd (Line Printer Daemon), lifted mostly verbatim out of BSD’s Net-2 code. The term lpd refers in different contexts to both the daemon and the whole collection of programs which run print spooling. Even today, most vendors ship this software. But this is beginning to change. SVR4-like systems, including Sun’s Solaris, come with a completely different print spooling package, centered around lpshcd. And there are signs that some Linux vendors will shift to providing LPRng, a far less ancient print spooling implementation that is freely available. LPRng is far easier to administer for large installations (read: more than one printer, any serial printers, or any peculiar non-lpd network printers) and has a less frighteningly haphazard database than does stock lpd. It can even honestly claim to be secure–there are no SUID binaries, and it supports authentication via PGP or Kerberos.

For the moment, even in light of the new options, lpd is probably fine for most Linux users. While it isn’t the snazziest system, it works fine once set up, and it is well understood and extensively documented in third-party Unix books.

If you’d like more information on LPRng, check out the LPRng Web page (http://www.astart.com/Lprng/LPRng.html). Future versions of this HOWTO will include information on using both LPRng and regular lpd.

## How It Works: Basic

In order to get printing working well, you need to understand how the lpd system works.

lpd refers in different contexts to both the daemon and the whole collection of programs which run print spooling. These are

- **lpd** The spooling daemon. One of these runs to control everything on a machine, AND one is run per printer while the printer is printing.
- **lpr** The user spooling command. It contacts lpd and injects a new print job into the spool.
- **lpq** Lists the jobs in a print queue.
- **lpc** The lpd system control command. With lpc you can stop, start, reorder, etc. the print queues.
- **lprm** This will remove a job from the print spool.
