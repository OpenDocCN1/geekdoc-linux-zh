![](bbox=[0.18, 0.13, 0.85, 0.52])

Figure 9-1. You can use *sysinstall* to tell FreeBSD to run *lpd* whenever it starts.

options, and eliminate extraneous ones. For instance, the *rm*, *rp*, and *if* options will all cause problems if they’re included but set to null values. You should also try printing as both *root* and an ordinary user; both should work equally well. If you’re printing to a remote printer, you may need to adjust that print server’s configuration to accept files from your client system. Consult the upcoming section, “Controlling Remote Printer Access” for information on how to do this.

# ## Using a Simple Filter

Much of the power of the BSD LPD system lies in the *if* option, which was omitted from Listing 9-1. The following section, “Setting Up Ghostscript,” describes the use of a powerful tool known as a *smart filter* in conjunction with Ghostscript to process a wide variety of file types. In many cases, a simpler filter may do the job. One common example is the need to turn a plain text file into a PostScript file for printing on PostScript printers that don’t know how to parse plain text. To do this, you first need a script to function as the filter program. Listing 9-2 shows an example. This script reads a file and looks for the string *%!*1*, with which all PostScript files begin. If that string is present, the script passes the file through to the printer unchanged. If the string isn’t present, the script uses the *nenscript* program to convert the file to PostScript. (This assumes that