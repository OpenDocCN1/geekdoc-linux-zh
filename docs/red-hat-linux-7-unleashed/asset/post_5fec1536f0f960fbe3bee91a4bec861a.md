
In fact, you can have multiple entries for each printer, which is helpful if you want to print different size papers, print color or black-and-white documents by switching cartridges, or change printer trays.

Old versions of Red Hat Linux used the 4.3BSD line-printer spooling system. This system has a number of features and associated programs to support background printing, multiple local and networked printers, and control of the printers and queued documents.

The main files used in the older printer spooling system were as follows:

- /etc/printcap
- /usr/sbin/lpd
- /usr/sbin/lpc
- /usr/bin/lpr
- /usr/bin/lprm
- /usr/bin/lpq
- /dev/printer

These files provided the basic features needed to initiate and control print jobs from the command line. See Table 19.3 for a selected list of additional Linux commands you may find helpful when printing.

Red Hat Linux now uses Patrick Powell's LPRng print spooler software, which is descended from the 4.3BSD release but rewritten from the ground up. LPRng offers a host of benefits and features over the previous printer spooling software, such as being distributed under the GNU GPL, backward compatibility, security, diagnostics, and multiple printers on a single queue. In addition to the previously listed commands, LPRng also uses

- /etc/lpd.conf
- /usr/sbin/checkpc
- /etc/lpd.perms
- /usr/bin/lpstat

These additional files are used for site-specific settings, to check or fix LPRng's installation, to set permissions for users, and to report on a printer's status.

When you first boot Linux, the shell script, lpd (under /etc/rc/init.d/) starts lpd, the printer daemon. This program, a printer server, runs in the background and waits for print requests. When a request is detected on the print queue, the server connects to the designated printer and passes the document stream through the proper printer filter.

Print requests are started with the `lpr` command. For example, the following command line will print your document to a file in the `/var/spool/lpd/lp` directory using the printer named `lp`:

```bash
# lpr -Plp myfile.txt
```

Other print spooling commands can help track your request. If you're printing a large document or a number of smaller files, you can see a list of print jobs running by using the `lpq` command. For example, to print a number of files at once to the default printer, use this:

```bash
# lpr *
```

**Note**

The LPRng system will only allow printing of 52 files at once. If you want to print more multiple files, you'll need to split up the print job.

Follow that command with this:

```bash
# lpq
```

This outputs the following:

```text
Printer: lp@thinkpad
Queue: 1 printable job
Server: pid 3631 active
Unspooler: pid 3632 active
Status: processing `ff6E30@thinkpad.home.org`, size 1309, format `f', IF filter `filter' at 17:40:52.610
        Owner/ID            Class Job Files             Size Time
 active  root@thinkpad+630  A      630 adsl,amd,anacron,apm 14542 17:40:51
```

This shows quite a bit of information, but the important item to note is the job number (630 in this example). If you want to stop the preceding print job, use the `lprm` command, followed by the job number, as in the following:

```text
# lprm 630
Printer lp@thinkpad:
        checking perms `root@thinkpad+630'
        dequeued `root@thinkpad+630'
```

This shows that `lprm` has removed the spool files and stopped the job. To disable or enable a printer and its spooling queue, rearrange the order of any printing jobs, or find out the status of printers, you can use `lpc` from the command line or interactively, but you must be logged in as root or as a superuser (through the `su` command).

LPRng's `lpc` command is very comprehensive and offers much more control over system and network printing than the legacy `lpc` command. This command may be used to activate or abort the print server, disable or enable print queueing, hold or release print jobs, and even move print jobs to a different printer! Start `lpc` on the command line like this:

```bash
# lpc
```

To view the built-in help on command keywords and syntax, type `help` or press `?` like this:

```text
lpc> help
```

After you press Enter, you'll see several pages of help text for `lpc`'s 30 different commands. A more abbreviated command is LPRng's `lpstat`. Use the command like this:

```text
# lpstat
Printer: lp@thinkpad
Queue: no printable jobs in queue
Status: subserver pid 3632 exit status `ABORT' at 17:43:05.111
```

If you have print jobs waiting, you'll see a list of jobs, along with information similar to that returned by `lpstat`.

LPRng is documented through its commands' man pages and documentation under the `/usr/share/doc/LPRng-3.6.22` directory. You'll find the latest version and documentation (including an excellent HOWTO document) at `http://www.astart.com/lprng/LPRng.html`.

## Table 19.3 Selected Printing Commands

| Command | Description |
| :--- | :--- |
| `cancel` | LPRng utility to cancel print service |
| `checkpc` | Verifies and fixes LPRng print system files |
| `lpc` | Controls program for local and remote printers |
| `lpd` | LPRng print server daemon |
| `lpf` | General printer filter |
| `lpr` | Sends print jobs to printer queue |
| `lprm` | Controls print queue |
| `lpstat` | Displays specified print service status |
| `mpage` | Prints multiple pages of text per sheet |
| `nprint` | NetWare print client |
| `pbm2ppa` | Converts bitmap to HP PPA format |
| `pbm2tolox` | Converts bitmap to Gemini printer graphic |
| `pbm2eopson` | Converts bitmap to Epson printer graphic |
| `pbm2oppa` | Converts bitmap to HP PPA format |
| `pbm2ptx` | Converts bitmap to Printtronix printer graphic |
| `pnm2ppa` | Converts any map to HP PPA format |
| `pqlist` | Lists NetWare print queue |
| `lprm` | Removes jobs from NetWare print queue |
| `pqstat` | Lists jobs in NetWare print queue |
| `pr` | Formats text files for printing |
| `printmail` | Formats mail messages for printing |
| `pserver` | NetWare print server |
| `sliceprint` | Formats documents with long lines |
| `smbclient` | Essential command used by smbprint for printing |
| `smbprint` | Shell script for printing to shared printers |
| `testprns` | Printer name check utility for Samba |
| `tunlp` | Parallel-port hardware utility |

## Other Helpful Printer Programs and Filters

Printer filters work by defining and inserting printer definitions into your /etc/printcap file. Embedded in each printer description is a pointer (pathname) to a script or program containing the filter to be run before output to the printer. This section introduces several ancillary printer filter systems you can try with Red Hat Linux.

### Apsfilter

Even if you're spoiled by the printtool program, you will at times need to use other programs or scripts to help set up or manage printing. If you can't or don't want to run X, but want to easily install printing services for HP or PostScript printers, one great solution is the printing filter package called Apsfilter, by Andreas Klemm and Thomas Bueschgens. Installing Apsfilter is a snap, and it's even easier to use.

Apsfilter works well with all Linux printing applications. Two added benefits are that it prints two formatted pages in Landscape mode on a single page when you print text documents, saving you paper, and “automagically” recognizes the following documents and graphic formats: `fig`, `bmp`, `pbm`, `pnm`, `ppm`, `PDF`, `tiff`, `jpeg`, `gif`, Sun rasterfile, PostScript, `dvi`, `raw` ASCII, and `gzip` and `bzip2` compressed files.

You’ll find the Apsfilter available through its home page at http://people.FreeBSD.org/~andreas/apsfilter/index.html.

### Magicfilter

Another printer filter similar to Apsfilter is H. Peter Anvin’s magicfilter (also maintained by David Frey for the Debian Linux distribution), which detects and converts documents for printing through a combination of a compiled C filter and a printer configuration file. You’ll find a copy at http://www.debian.org/Packages/unstable/text/magicfilter.html.

### LPRMagic

Michele Andreoli’s LPRMagic is another printer filter you can set up under Red Hat Linux. All configuration for the filtering is contained in a `/etc/lprmagic.conf` file. Some of the features of LPRMagic include file type recognition (even .wav and MIDI!), delayed printing, and Samba and LPRng support. Installation is via a set of shell scripts (executed as root). You can download a copy from http://metalab.unc.edu/pub/Linux/system/printing/.

### HPTools

Have a Hewlett-Packard printer? If so, you might want to try Michael Janson’s HPTools to manage your printer’s settings. The main tool is the `hpset` command, which sports more than 13 command-line options you can use to control your printer. For example, to save money on print cartridges by using less ink, you can use `hpset` to tell your printer to print in the economy mode with this code:

```bash
# hpset -c econ | lpr
```

The `hpset` command also has an interactive mode, so you can test your printer, set different default fonts, or perform other software control of your printer, such as bi- or uni-directional printing.

You can find HPTools through its home page at http://www.uni-karlsruhe.de/~uips/hptools.html.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_678_0.png)
