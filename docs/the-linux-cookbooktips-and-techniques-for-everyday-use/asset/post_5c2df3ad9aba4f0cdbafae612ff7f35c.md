
## 26. Printing

```
@sf(Debian): `magicfilter`
```

The usual way to print on a Linux system is to send a print job to the printer with lpr, as described below in Sending a Print Job to the Printer.

But you don't always send a file straight to the printer---sometimes you may want to add special things to it before you print it, such as headers or graphic trim. For example, you might want to split a text file into pages and add a header to the top of each page containing the file name and page number; all of this is described in Formatting Text.

Sometimes you may need to convert or otherwise prepare a file so that it can be printed on your particular printer, since not all print hardware can print the same kinds of file formats. Recipes in this chapter show how to do this, such as how to convert PostScript files so that they will print properly on a non-PostScript printer (see section Preparing Files for Printing).

This chapter also shows how to format PostScript files for printing. To convert plain text to PostScript and enhance it for printing, by adding fonts, graphic headers, and the like, see Converting Plain Text for Output.

And this chapter isn't in the files section, because you can print things that aren't in a file---for example, you can pipe the output of another tool or series of tools to lpr, and it will spool that command output to the printer. This usage is actually very common.

NOTE: When a printer is properly configured on Linux, it is a pleasure to use, but a misconfigured printer can lead to all kinds of trouble---including the dreaded "staircase effect," where a text file prints with each subsequent line of output offset to the right by the length of the previous line.

If print services haven't been configured yet on your system, I strongly recommend that the `magicfilter` package be installed; it includes filters for the automatic detection of file types---when you print a file, it automatically converts it to the proper format for your printer.

Comprehensive details on the setup of printer resources can be found in both the Printing HOWTO and the Printing Usage HOWTO (see section Reading System Documentation and Help Files).

- 26.1 Making and Managing Print Jobs Sending a job to the printer.
- 26.2 More Recipes for Printing Print services in some applications.
- 26.3 Preparing Files for Printing Converting files for your printer.

## 26.1 Making and Managing Print Jobs

The traditional way to print on Linux-based systems is to send a print job for the file or data you want to print to the spool queue for the printer in question. The spool queue contains all of the print jobs sent to it by all users; these jobs are released in turn to the printer device as it becomes available. In this way, Linux can handle multiple print jobs going to the same printer at once.

The following recipes show how to make and manage print jobs. In practice, you will probably send print jobs all the time—since this is the way most printing is done in Linux—and use the tools for listing or cancelling print jobs rarely. But sometimes things do go wrong, and it helps to know what to do when that happens.

- 26.1.1 Sending a Print Job to the Printer
- Sending a print job.
- 26.1.2 Printing Multiple Copies of a Job
- Printing more than one copy.
- 26.1.3 Listing Your Print Jobs
- Listing your print jobs.
- 26.1.4 Cancelling a Print Job
- Cancelling a print job.

### 26.1.1 Sending a Print Job to the Printer

Use lpr to send a print job to the printer—give the name of the file to print as an argument. (You can also pipe the output of a command to lpr.)

lpr writes a copy of the specified file or text to the spool queue of the specified printer, to be sent to the printer when the printer becomes available.

- To print the file `invoice`, type:

```
$ lpr invoice RET
```

- To type a message with banner and send it to the printer, type:

```
$ banner "Bon voyage!" | lpr RET
```

- To print a verbose, recursive listing of the `/usr/doc/HOWTO` directory, type:

```
$ ls -lR /usr/doc/HOWTO | lpr RET
```
