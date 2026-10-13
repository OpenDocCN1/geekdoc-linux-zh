# FIGURE 16.3

The xv command is an X11 client that loads, edits, captures, saves, or prints images and features sophisticated color controls.

![](bbox=[0.35, 0.17, 0.88, 0.45])

The xv command can import and export 18 different graphics file formats and also can print graphics. For more information about using xv, see its man page and read its definitive documentation. This file is 128 pages in PostScript format. See the next section to learn how to easily read this documentation.

# Using the gv Command to View PostScript Files

The gv command is a PostScript previewer used to examine or read PostScript graphics or documents before printing. You must run the X Window System to use this program. This command, found under the /usr/X11R6/bin directory, is a much-improved previewer by Johannes Plass and is based on the older ghostview program by Tim Theilison (installed under the /usr/X11R6/bin directory).

The gv command (shown in Figure 16.4) has more than 36 different command-line options and uses a number of X11 Toolkit options, such as geometry settings. You can start gv by itself or specify a file on the command line, along with its options:

```
# gv -geometry 640x480 myfile.ps
```

This command line starts the gv command in a 640×480 pixel window displaying the file myfile.ps.

> Use the gv command to read X11 client or program documentation in PostScript format. For example, to quickly browse and read the xv documentation, use gv like this:
> 
> # gv -geometry 640x480 /usr/doc/xv-3.18a/xv.docs.ps.gz
> 
> The gv client reads compressed PostScript documents!