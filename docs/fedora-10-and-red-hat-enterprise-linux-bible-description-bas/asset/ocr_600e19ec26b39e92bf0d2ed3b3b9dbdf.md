# Using Printing Commands

To remain backward compatible with older UNIX and Linux printing facilities, CUPS supports many of the old commands for working with printing. Most command-line printing with CUPS can be performed with the lpr command. Word processing applications for Linux, such as StarOffice, OpenOffice.org, and AbiWord, are set up to use this facility for printing.

With the Printer configuration window, you can define the filters needed for each printer so that the text can be formatted properly. Options to the lpr command can add filters to process the text other. Other commands for managing documents include lq toeq (for viewing the contents of print queues), lpm (for removing print jobs from queue), and lpc (for controlling printers).

> CROSS-REFERENCE: Chapter 6 provides examples of how to format and print documents in different formats, including troff and TeX.

# Using lpr to print

With the lpr command, you can print documents to both local and remote printers. Document files can be added to the end of the lpr command line or directed to the lpr command using a pipe (|). Here is an example of a simple lpr command:

```
$ lpr doc.ps
```

When you submit a document file with lpr, output is directed to the default printer. As an individual user, you can change the default printer by setting the value of the PRINTER variable. Typically, you would add the PRINTER variable to one of your startup files, such as $HOME/.bashrc. Here is a line to add to .bashrc to set your default printer to Lp3:

```
export PRINTER=lp3
```

For the NEW PRINTER value to take effect immediately, source the .bashrc file (type $HOME/.bashrc). To override the default printer, select a particular printer on the lpr command line. The following example shows the -P option to select a different printer:

```
$ lpr -P canyonps doc.ps
```

The lpr command has a variety of options that enable lpr to interpret and format several different types of documents. These include -# num, where num is replaced by the number of copies to print (from 1 to 100) and -1 (which causes a document to be sent in raw mode, presuming that the document has already been formatted).