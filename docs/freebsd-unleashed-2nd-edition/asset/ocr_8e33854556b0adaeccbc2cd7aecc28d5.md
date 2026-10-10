you to print various types of files directly from the command line with `lpr` and avoid having to load them into a program or convert them by hand before you print them. You specify which filter to use on the command line with an option to `lpr`. (lpr is the command used to print files from the command line. We will cover it in detail later in the chapter.) Table 15.2 lists the conversion options that lpr understands.

# **TABLE 15.2 Conversion Options to lpr**

**Option Description**
`-d` The file is in DVI format (produced by the TeX typesetting system).
`-f` Intended as a filter for printing FORTRAN source files. This is basically obsolete unless you are still writing a lot of FORTRAN code.
`-c` The file contains plotting data produced by cplot. This program is not included with FreeBSD.
`-g` The file contains plotting data produced by the Unix plot routines. These routines are included with FreeBSD.
`-n` The file contains data from device-independent troff (ditroff). This is not supported by any software included with FreeBSD.
`-t` The file contains C/A/T phototypesetter commands for ancient versions of troff. This is probably obsolete for most people.
`-v` The file contains a raster image for various image-printing devices. Most people will not use this.

By default, none of these filters is installed. Also, the option letter and the filter it calls are not hard-coded into the system. Because of this, if you have no use for a cplot filter, for example, it is easy to have the -c option call some other filter that you might have use for. Like text filters, these filters can be shell scripts that call standard Unix programs or stand-alone executable programs that may be provided by manufacturers of third-party software.

The following is an example of a very simple conversion filter that converts data in the GNU groff typesetting system (which cannot be understood by the printer) into PostScript (which can be understood by the printer, either directly or by sending the data through GhostScript):

```
```
#!/bin/sh
exec grops
```
```

If you read the man page for `grops`, you will see that it is a program that converts groff to PostScript. In this case, the file will simply be sent through `grops` before being sent to the printer for printing.

The filter should be saved in the directory /usr/local/libexec. (You might decide to call this filter g2ps or something similar because it converts groff to PostScript.)