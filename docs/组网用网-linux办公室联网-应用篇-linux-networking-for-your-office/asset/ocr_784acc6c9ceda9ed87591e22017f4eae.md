This entry defines a single printer, which is known by two names—lp and hp4000—as defined on the first line of the entry. Entries are separated by colons, with a backslash (\ ) at the end of most lines. (The backslashes actually signal a continuation of a line—each /etc/printcap entry is technically a single line.) Options use an equal sign (=) or pound sign (#) to give values to parameters. Available options include the following:

+   - sd=—This is the spool directory—where lpr places files and where lpd looks for them.

+   - mx#—This is the maximum file size. A 0 here indicates no limit. In some environments, you might want to set a limit, to prevent abuse by individuals trying to print ludicrously large files. Be aware, though, that even some very large files can produce relatively few pages of output, particularly for raw printer queues. This is particularly true of color bitmapped graphics, which can easily exceed 1MB per page, even at modest resolutions.

+   - sf—This option, if present, suppresses the use of form feeds between print jobs. You might want to set it for a raw queue if you otherwise get a blank sheet between print jobs. If you set it when it’s not needed, though, you might find that the final page of some jobs doesn’t print.

+   - sh—This option, if present, suppresses the printing of job headers. To get a sheet separating different print jobs, remove this option from /etc/printcap.

+   - lp=—You set the name of the printer device with this option.

+   - if=—This option sets the input filter, which is what controls the way the queue handles input files. In particular, this filter tries to determine what type of file you’re printing, and processes it appropriately. On Red Hat systems, the default filter detects PostScript files (among other file types) and sends them through Ghostscript, when printing to a non-PostScript printer. If you omit this line or leave it blank, the queue becomes a raw queue, suitable for use with client drivers for the specific model of printer.

Most of these options correspond to options you set in printtool. Much of what printtool does is to translate the /etc/printcap entries into easier-to-understand questions, collect your answers to these questions, and translate back to an appropriate /etc/printcap format. In addition, there are several other possible options for /etc/printcap entries. You can type man printcap to learn more about them.

# Ghostscript Control: The postscript.cfg File

Additional printtool options wind up in the /var/spool/lpd/queuename/postscript.cfg file, which contains options that are passed to PostScript. This file sets a number of environment variables, which the filter uses when launching Ghostscript. Some of the most important of these variables are as follows: