Apsfilter works well with all Linux printing applications. Two added benefits are that it prints two formatted pages in Landscape mode on a single page when you print text documents, saving you paper, and “automagically” recognizes the following documents and graphic formats: `fig`, `bmp`, `pbm`, `pnm`, `ppm`, `PDF`, `tiff`, `jpeg`, `gif`, Sun rasterfile, PostScript, `dvi`, `raw` ASCII, and `gzip` and `bzip2` compressed files.

You’ll find the Apsfilter available through its home page at http://people.FreeBSD.org/~andreas/apsfilter/index.html.

# magicfilter

Another printer filter similar to Apsfilter is H. Peter Anvin’s magicfilter (also maintained by David Frey for the Debian Linux distribution), which detects and converts documents for printing through a combination of a compiled C filter and a printer configuration file. You’ll find a copy at http://www.debian.org/Packages/unstable/text/magicfilter.html.

# LPRMagic

Michele Andreoli’s LPRMagic is another printer filter you can set up under Red Hat Linux. All configuration for the filtering is contained in a `/etc/lprmagic.conf` file. Some of the features of LPRMagic include file type recognition (even .wav and MIDI!), delayed printing, and Samba and LPing support. Installation is via a set of shell scripts (executed as root). You can download a copy from http://metalab.unc.edu/pub/Linux/system/printing/.

# HPTools

Have a Hewlett-Packard printer? If so, you might want to try Michael Janson’s HPTools to manage your printer’s settings. The main tool is the `hpset` command, which sports more than 13 command-line options you can use to control your printer. For example, to save money on print cartridges by using less ink, you can use `hpset` to tell your printer to print in the economy mode with this code:

```
```
# hpset -c econ | lpr
```
```

The `hpset` command also has an interactive mode, so you can test your printer, set different default fonts, or perform other software control of your printer, such as bi- or uni-directional printing.

You can find HPTools through its home page at http://www.uni-karlsruhe.de/~uips/ hptools.html.

![](bbox=[0.93, 0.56, 0.99, 0.86])