
was attached) and executed a special program called a *PostScript interpreter*, which read the incoming PostScript program and *rendered* the results into the printer's internal memory, thus forming the pattern of bits (dots) that would be transferred to the paper. The generic name for this process of rendering something into a large bit pattern (called a *bitmap*) is raster image processor (RIP).

As the years went by, both computers and networks became much faster. This allowed the RIP to move from the printer to the host computer, which, in turn, permitted high-quality printers to be much less expensive.

Many printers today still accept character-based streams, but many low-cost printers do not. They rely on the host computer's RIP to provide a stream of bits to print as dots. There are still some PostScript printers, too.

## Printing with Linux

Modern Linux systems employ two software suites to perform and manage printing. The first, the Common Unix Printing System (CUPS), provides print drivers and print-job management, and the second, Ghostscript, a PostScript interpreter, acts as a RIP.

CUPS manages printers by creating and maintaining *print queues*. As we discussed in the earlier history lesson, Unix printing was originally designed to manage a centralized printer shared by multiple users. Since printers are slow by nature, compared to the computers that are feeding them, printing systems need a way to schedule multiple print jobs and keep things organized. CUPS also has the ability to recognize different types of data (within reason) and can convert files to a printable form.

## Preparing Files for Printing

As command line users, we are mostly interested in printing text, though it is certainly possible to print other data formats as well.

## pr—Convert Text Files for Printing

We looked at pr a little in the previous chapter. Now we will examine some of its many options used in conjunction with printing. In our history of printing, we saw how character-based printers use monospaced fonts, resulting in fixed numbers of characters per line and lines per page. pr is used to adjust text to fit on a specific page size, with optional page headers and margins. Table 22-1 summarizes its most commonly used options.

Table 22-1: Common pr Options

| Option | Description |
|---|---|
| +first[:last] | Output a range of pages starting with first and, optionally, ending with last. |
| -columns | Organize the content of the page into the number of columns specified by columns. |
| -a | By default, multicolumn output is listed vertically. By adding the -a (across) option, content is listed horizontally. |
| -d | Double-space output. |
| -D format | Format the date displayed in page headers using format. See the man page for the date command for a description of the format string. |
| -f | Use form feeds rather than carriage returns to separate pages. |
| -h header | In the center portion of the page header, use header rather than the name of the file being processed. |
| -l length | Set page length to length. The default is 66 (US letter at 6 lines per inch). |
| -n | Number lines. |
| -o offset | Create a left margin offset characters wide. |
| -w width | Set the page width to width. The default is 72. |

pr is often used in pipelines as a filter. In this example, we will produce a directory listing of /usr/bin and format it into paginated, three-column output using pr:

```
`[me@linuxbox ~]$ ls /usr/bin | pr -3 -w 65 | head`
```

```
2016-02-18 14:00                                      Page 1
[						]
411toppm					apturl				bsd-write
a2p					ar				bsh
a2ps					arecord				btclflash
a2ps-lpr-wrapper			arecordmidi			bug-buddy
					ark				buildhash
```

## Sending a Print Job to a Printer

The CUPS printing suite supports two methods of printing historically used on Unix-like systems. One method, called Berkeley or LPD (used in the Berkeley Software Distribution version of Unix), uses the lpr program, while the other method, called SysV (from the System V version of Unix), uses the lp program. Both programs do roughly the same thing. Choosing one over the other is a matter of personal taste.

### lpr—Print Files (Berkeley Style)

The lpr program can be used to send files to the printer. It may also be used in pipelines, as it accepts standard input. For example, to print the results of our previous multicolumn directory listing, we could do this:

```
`[me@linuxbox ~]$ ls /usr/bin | pr -3 | lpr`
```

The report would be sent to the system’s default printer. To send the file to a different printer, the -P option can be used like this:

```
lpr -P *printer_name*
```

Here, *printer_name* is the name of the desired printer. To see a list of printers known to the system, use this:
