
### Table 20.1 PCL Versions

| Version | Introduction | LaserJet Models | Features |
| :--- | :--- | :--- | :--- |
| 3 | 1984 | LaserJet, LaserJet Plus | Full-page formatting |
| 4 | 1985 | LaserJet Series II | Downloadable macros; additional fonts |
| 4e | 1989 | LaserJet IIP, IIP Plus | Compressed fonts and graphics |
| 5 | 1990 | LaserJet III series | Outline (scalable) fonts and vector graphics |
| 5e | 1992 | LaserJet 4 series and some 5 series | 600dpi printing; additional fonts |
| 5c | 1994 | Color LaserJet series | Color extensions |
| 6 | 1996 | LaserJet 5, 5ce, 6 series, 4000 series, 5000 series | Faster graphics; 1200dpi printing |
| XL | 1996 | LaserJet 6P, 6MP | Additional graphics commands; smaller file sizes |

HP uses PCL in both its laser printers and many (but not all) of its inkjet models. The inkjet printers usually implement a subset of the full PCL functionality.

PCL has become so successful that most laser printer manufacturers support it on their printers. This fact makes supporting laser printers fairly simple, because one set of drivers supports a wide variety of printers. (Some low-end models use strange proprietary protocols, however, as I describe shortly.)

When buying a PCL printer, pay attention to the PCL version the printer emulates. In particular, if you get a 600dpi printer, be sure the printer supports PCL 5e or later. PCL 5 and earlier printers support printing at up to only 300dpi. Some 600dpi printers support PCL 5 or earlier, but require special Windows drivers to work at 600dpi. You should generally avoid such printers.

A few Linux programs, such as ApplePlexWare (http://www.applelex.com), can produce PCL output. Most Linux programs, however, produce PostScript. To use a PCL printer, therefore, you must use Ghostscript to convert most Linux programs' PostScript output into a form that the printer can understand. I describe this process shortly.

As with PostScript printers, most PCL printers come with RAM that's only marginally adequate. I recommend doubling or tripling the RAM in most PCL printers. The need for increased RAM is particularly acute if you print bitmapped graphics, because these graphics files typically don't compress as well as does text.

If you're in the market for a laser printer, my first recommendation is to buy a PostScript model. If PostScript printers are too rich for your blood, though, a PCL printer is my second—and final—choice. Some laser printers use other protocols, but they're generally very difficult to get working acceptably under Linux.

### ESC/P and ESC/P2

In the 1980s, dot-matrix printers were the most popular type of printer on small computers. Among dot-matrix printers, Epson dominated the market. Epson developed a simple printer language, known as ESC/P, for its dot-matrix printers. ESC/P commands could set fonts, adjust margins, or send an encoded bitmap graphic, among other things.

Like HP's PCL, Epson's ESC/P language was widely copied. If you need to use a dot-matrix printer with Linux, I strongly recommend you ensure that the printer understands ESC/P. Ghostscript can output to ESC/P, so you can produce good output from Linux on an ESC/P printer.

When Epson began producing inkjet printers, it refined ESC/P and called it ESC/P2. Epson's inkjet printers all use ESC/P2, although each printer speaks a slightly different dialect of the language. Fortunately, Ghostscript handles most ESC/P2 variants equally well.

Unlike ESC/P, ESC/P2 hasn't been widely copied. Most non-Epson inkjet printers use other languages—some high-end models use PostScript, some use PCL, and others use their own proprietary languages.

### Other Languages

A large number of proprietary printer languages exist, for example:

- Many early dot-matrix printers used their own languages. Some of these are supported by Ghostscript.
- Canon inkjet printers use a proprietary Canon language. Most of these printers are supported by Ghostscript.
- Most Lexmark inkjets use a proprietary Lexmark language, although a few use PostScript, and Lexmark laser printers use PCL or PostScript. Unfortunately, there is no Ghostscript driver for Lexmark's inkjet language.
- Some Hewlett-Packard inkjets use a proprietary system known as the *Printing Performance Architecture* (PPA). There’s limited support for some subvarieties of PPA.
- Other Hewlett-Packard inkjets and most Hewlett-Packard laser printers use PCL.
- Smaller inkjet printer manufacturers occasionally go their own way, but more often they emulate another manufacturer’s language—most often PCL.

If it’s not clear from a printer’s box or Web site what language it uses, you should assume it’s a proprietary language that’s not supported by Linux.

### Windows-Only Printers

In the mid-1990s, manufacturers began introducing low-cost laser printers that shipped with ridiculously small amounts of RAM and anemic processors. These printers relied upon special bidirectional Windows 3.1 (and later Windows 95 and 98) drivers to feed data to the printer at a precisely controlled rate. These printers work in Windows, but they’re ballast in all other OSs. Some of the more polite names applied to these printers include *WinPrinter*, *GDI Printer* (after Windows’ Graphics Device Interface subsystem), and *host-based printer*.

A few printers are host-based at 600dpi, but have enough RAM and CPU to support 300dpi printing in more conventional ways. These printers typically support PCL 5 or earlier, but require Windows to print at 600dpi.

Linux’s printing system isolates Ghostscript, which does the conversion from PostScript to a printer’s native language, from the low-level, parallel-port drivers. Therefore, writing reliable Linux drivers for host-based printers is an extremely difficult proposition.

The logic behind host-based printers, and the reason for pessimism concerning Linux drivers for these printers, doesn’t apply to inkjet printers. Most inkjet printers don’t have extensive RAM or processor support to begin with, and their timing needs aren’t as critical as are those for laser printers. The difference between a supported inkjet printer and an unsupported one is simply that nobody has written a Ghostscript driver for the unsupported printer. Likewise, a few laser printers aren’t technically host-based printers, but they use proprietary and undocumented protocols and therefore aren’t supported in Linux. None of this should be taken to mean that writing drivers for unsupported conventional printers is an easy task. As I’ve said, some of the protocols used are undocumented, and might in fact be quite complex. Writing such drivers is not a trivial undertaking.

By whatever name, you should avoid Windows-only printers. For information on support for specific printers, check the Printing HOWTO Support Database at [http://www.picanter.com/~gtaylor/pt/print1st.cgi](http://www.picanter.com/~gtaylor/pt/print1st.cgi). This is the single most valuable resource for anybody in the market for a Linux printer.

### Note

If you're using a Linux computer exclusively as a print server for Windows computers, you might be able to serve a printer that can't otherwise be used from Linux. You must load the printer's native drivers on the Windows client computers and export the printer as a “raw” queue—that is, without filtering the print jobs through Ghostscript. This procedure works for Windows-only printers that don't have any unusual timing requirements, but it doesn't work with most host-based printers.

### Using Printers in Linux

In most OSs, printer drivers serve as an interface between an application and a printer. Communication can go both ways in this arrangement. For instance, a printer driver can inform an application that the printer supports wide margins. This isn't the case in Linux. In Linux, applications produce PostScript output, usually without features that tailor the output for specific printers. If your printer supports wide margins, you must find some way to convince your application of this fact.

Because most printers sold for the x86 market are not PostScript printers, Linux includes a utility, Ghostscript, that converts between PostScript and an assortment of other printer languages. In effect, Ghostscript takes over many of the roles of a printer driver in other OSs, although Ghostscript doesn't communicate back to the application what a printer's capabilities are.

In addition to Ghostscript, Linux computers implement a printer queue system. This queue holds the output from an application until the printer becomes ready. The queue then feeds the job through Ghostscript or some other program, if necessary, and passes the result on to the printer.

### Understanding Linux Printer Queues

Most Linux installations use a printer queue system known as lpr, named after one of its component programs. To print using this system, a user or program calls lpr and passes to it the name of a file to print. Optionally, it also passes various parameters, such as the name of a printer, for instance,

```bash
lpr -Pepson example.ps
```

This command prints the file example.ps to the printer queue called epson. The lpr printing system includes a second program, known as lpd. This program is a daemon, which processes files in the queue according to rules outlined in the /etc/printcap configuration file, which I
