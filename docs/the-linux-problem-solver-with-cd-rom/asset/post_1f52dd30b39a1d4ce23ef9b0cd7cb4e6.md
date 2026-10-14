
## Printing Text

It’s a funny thing, but users tend to expect their text files to actually print on their printer. But unlike other kinds of operating systems that run programs on the text file before sending it to the printer, under Unix, if you send a text file straight to a PostScript printer, the printer may not have a clue as to what to do with it.

If every user knew how to print text with a program like enscript or a2ps, this wouldn’t be a problem. But (perhaps unfortunately) PostScript filters have always included autosensing software that checks the file to see if it’s PostScript, and if not, converts it to PostScript, then hands it down to the printer. So that’s what you’re dealing with when you install a printer in a larger workgroup environment.

Luckily, ifhp provides a short and quick solution. If your printer is HP-like and supports PCL, enabling PCL support causes the option default language-pcl to come into effect, and your text will come out. If you have a2ps installed on the system, it will be the default, and you won’t have to think about it as long as you have these lines in the systemwide ifhp.conf file:

```
text_converter=/usr/local/bin/a2ps -q -B -1 -M letter --borders=no -o-
text_converter_output=ps
```

The problem is, this won’t work if your printer doesn’t have native PostScript support and you’re not using ifhp (for example, if you’re using Ghostscript in your print filter as described in Section 5.4). The quick fix is to make sure you have version 4.2 (or later) of a2ps installed on your system in /usr/local/bin. Then, in your filter, send the print job through this before it reaches gs (or whatever you use to rasterize):

```
/usr/local/bin/a2ps -1 -q -B -o-
```

The details of the ifhp case lie in the text_converter= and file_output_match= settings in ifhp.conf; have a look at it if you want, but don’t worry too much over plain text printing—it’s just not worth it. If a user wants better-looking plain text output, tell them to read up on a2ps.

Relevant man pages: a2ps (1), enscript (1)

## AppleTalk Printers

Many Apple LaserWriters won’t let you talk directly on a port, or you may be on a Macintosh-dominated network that only lets you reach the printers via AppleTalk. No problem—take a look at Chapter 4 for how to install this package, put an appropriate entry in your /etc/printcap, carry out the two steps outlined below, and you should be ready to go.

## PROBLEM 56

Symptom: Someone printed a binary file and the printer is spewing garbage.

Problem: The print spooler doesn't reject binary files.

Fix: First get rid of the offending job. As root, stop the printer with lpc printername down. Remove the active job with lprm -Pprintername. The printer will probably continue to spew garbage pages; switch it offline, reset it, wait a little bit, and see if any print jobs remain in the buffer. Then start the printer again with lpc up printername.

After sending an optional nasty message to the user who caused the problem, install a binary filter (such as the one that comes with a2ps) to kick binary files out of the queue.

Here's the /etc/printcap entry:

```
lw|laserwriter|Apple LaserWriter\
:mx#0:sF:sh:\
:sd=/var/spool/lpd/lw:\
:lp=/var/spool/lpd/lw/null:\
:lf=/var/spool/lpd/lw/log:pw#80:\
:of=/usr/local/atalk/etc/filters/ofpap:\
:if=/usr/local/atalk/etc/filters/ifpap:
```

The filters here are ofpap, ifpap, and tfpap, which come with the Netatalk distribution (actually, they are all basically the same program, psf). These are no-frills filters—be careful not to use a filter with a rev at the end of the name because the filter will attempt to reverse the pages (this doesn't work particularly well because PostScript code is hard to parse without a full-blown interpreter). The ofmpap and ofwmpap variants of the filter turn on a couple of workarounds for certain printers that don't behave correctly. See the psf manual page for a description of those.

Your job doesn't end with the filters, though. Notice that the device is null, but for file-locking reasons it can't be a link to /dev/null. On Linux, the following creates the device:

```
# mknod spool_dir/null c 1 3
```

One last point—the program that eventually sends the file to the printer, pap, needs to know the printer name, which may be different from what you call it on your system. Create a file called .paprc containing the AppleTalk name of the printer.
