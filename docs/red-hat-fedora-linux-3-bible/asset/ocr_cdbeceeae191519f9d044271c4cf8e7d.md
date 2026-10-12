After that, you can print files as raw data to your printers without using the `-oraw` option to print commands. As an alternative, you can just select the Raw Print Queue driver when you first configure printing through the Printer configuration window.

# Using Printing Commands

To remain backward compatible with older UNIX and Linux printing facilities, CUPS supports many of the old commands for working with printing. Most command-line printing with CUPS can be performed with the `lpr` command. Word processing applications for Linux, such as StarOffice, OpenOffice, and AbiWord, are set up to use this facility for printing.

With the Printer configuration window, you can define the filters needed for each printer so that the text can be formatted properly. Options to the `lpr` command can add filters to properly process the text. Other commands for managing printed documents include `lpq` (for viewing the contents of print queues), `lprm` (for removing print jobs from the queue), and `lpc` (for controlling printers).

CROSS-REFERENCE: Chapter 6 provides examples of how to format and print documents in several different formats, including `troff` and `TeX`.

# Using lpr to print

With the `lpr` command, you can print documents to both local and remote printers. Document files can be either added to the end of the `lpr` command line or directed to the `lpr` command using a pipe (`|`). Here is an example of a simple `lpr` command:

```
$ lpr doc1.ps
```

When you just specify a document file with `lpr`, output is directed to the default printer. As an individual user, you can change the default printer by setting the value of the PRINTER variable. Typically, you would add the PRINTER variable to one of your startup files, such as `$HOME/.bashrc`. Here is a line to add to your _.bashrc file to set your default printer to lp3:

```
export PRINTER=lp3
```

To override the default printer, specify a particular printer on the `lpr` command line. The following example uses the `-P option to select a different printer:

```
$ lpr -P camyonps doc1.ps
```

The `lpr` command has a variety of options that enable `lpr` to interpret and format several different types of documents. These include `–# num`, where `num` is replaced by the number of copies to print (from 1 to 100) and `-1` (which causes a document to be sent in raw mode, presuming that the document has already been formatted).