NFS-mounted on the print server, and because this machine points within its own printcap file to the same print spool file, `lpd` waits for data to arrive in /share/printers/spool/jj. When your print job enters the spool, it either waits its turn in the queue, if other jobs are already printing and waiting, or gets sent to the printer directly, if nothing else is waiting.

However, `~/picture.jpg` is not a raw ASCII text file. It is an image file—a JPEG (Joint Photographic Experts Group format) file, to be precise. Fortunately, you had the foresight to realize that people were pretty likely to print more than just raw text to a color printer. With the APSfilter program installed—as discussed in “Setting Up Popular Print Filters,” in the Immediate Solutions section—your machine knows how to print a JPEG file. The image is converted and sent as a PostScript file to the printer.

# # Linux Printing Issues

With Linux, as with any other operating system, you need to consider the following items when setting up your printers and when printing:

+   * You cannot pass print jobs between Linux and another operating system without special tools. After your printers are set up and running, see Chapter 18 for information on how to share print jobs between Linux and other operating systems.

+   * Printing to a local printer and printing to a network printer are two entirely separate configuration issues. You need to configure network printers specially.

+   * Printing anything other than raw ASCII text files requires special filters to process the data and convert it into PostScript format. PostScript is a print-formatting language first developed by Adobe. It is more of a programming language than a markup language—more like C than HTML. If your printer is not PostScript-capable, you may be relegated to using only ASCII text documents.

+   * If you do not have print filters installed to do the conversion for you, there is a program called GhostScript that can handle this.

# # Introduction To GhostScript

When the Unix community needed a program that could handle PostScript format files, the GNU (Gnu’s Not Unix, at www.gnu.org) folks, along with Aladdin Enterprises (www.aladdin.com), stepped in and gave us GhostScript, which actually is a suite of tools.

The GhostScript program, gs, is a PostScript and PDF (Adobe’s Portable Document Format) interpreter. You can use this tool to view or print the contents of a