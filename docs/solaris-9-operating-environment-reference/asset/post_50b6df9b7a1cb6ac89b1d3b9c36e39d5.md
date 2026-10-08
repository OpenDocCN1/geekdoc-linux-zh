
# postdmd

# 1069

# Options

- -b num Pack the bitmap in the output file, using num byte patterns. A value of 0 turns off all packing of the output file. By default, num is 6.
- -c num Print copies of each page. By default, only one copy is printed.
- -f Flip the sense of the bits in files before printing the bitmaps.
- -m num Magnify each logical page by the factor num Scale uniformly about the origin which, by default, is located at the center of each page. The default magnification is 1.0.
- -n num Print logical pages on each piece of paper where num can be any positive integer. By default, num is set to 1.
- -o list Print pages whose numbers are given in the comma-separated list. The list contains single numbers and and ranges N1-N2. A missing N1 means the lowest-numbered page, a missing N2 means the highest. The page range is an extension of logical pages instead of physical sheets of paper. For example, if you are printing two logical pages to a sheet and you specified a range of 4, then two sheets of paper containing four layouts would print. If you specified a range of 3-4 when requesting two pages to a sheet, then only page 3 and 4 layouts would print and they would appear on one physical sheet of paper.
- -p mode Print in p (portrait) or l (landscape) mode. Only the first character of mode is significant. The default mode is portrait.
- -x num Translate the origin inches along the positive x axis. The default coordinate system has the origin fixed at the center of the page, with x to the right and y up the page. Positive num moves everything right. The default offset is 0 inches.
- -y num Translate the origin inches along the positive y axis. Positive num moves everything up the page. The default offset is 0.

Only one bitmap is printed on each logical page, and each of the input files must contain contents of at least one bitmap. Decreasing the pattern size with the -b option may help throughput on printers with fast processors (such as PS-810s), while increasing the page size often is the right move on older models (such as PS-800s).

# Exit Status

- 0 Successful completion.
- non-zero An error occurred.

# Files

```
/usr/lib/lp/postscript/forms.ms/usr/lib/lp/postscript/ps.requests
```

# 1070

# postio

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNwps |

# See Also

- download(1), dpost(1), postdaisy(1), postio(1), postmd(1), postprint(1), postreverse(1), posttek(1), attributes(5)

# postio — Serial Interface for PostScript Printers

# Synopsis

```
/usr/lib/lp/postio -l line [-i] [-q] [-t] [-S] [-B speed] [-B num]
[-L file] [-P string] [-R num] [file...]
/usr/lib/lp/postscript/postio
```

# Description

The postio sends commands to the PostScript printer attached to line. If you specify no flags, the standard input is sent.

# Notes

The input files are handled as a single Postscript job. Sending several different jobs, each with its own end-of-job mark (*D) is not guaranteed to work properly. postio can quit before all the jobs have completed and can be restarted before the last finishes.

All the capabilities described below may not be available on every machine or across the different versions of the UNIX system that are currently supported by the program.

There may be no default line, using the -l option is strongly recommended. If you use the -l option, postio may try to connect to the printer using the standard output. If data is involved, the -b option may be ineffective and attempts by postio to impose control over data in both directions may not work. The -q option can help the printer is connected to RADIAN. The -s option is not generally recommended and should be used only if all other attempts to establish a reliable connection fail.

# Options

The following group of options should be sufficient for most applications.

- -b speed Transmit data over line at baud rate Recognized baud rates are 1200, 2400, 4800, 9600, and 19200. The default speed is 9600.
- -B num The internal buffer size for reading and writing files to num bytes. By default, num is 2048 bytes.
- -D Enable debug mode. Guarantee that everything on line is added to the log file (standard error by default).

# 1071

- -l line Connect to the printer attached to line. In most cases, there is no default and postio must be able to read and write line. If the line does not begin with a /, it may be treated as a Datakit destination.
- -L file Put data received on line in file. The default log file is standard error. Printer or status messages that don't show a change in state are normally written to file but can be forced with the -D option.
- -P string Send string to the printer.
- -R num Run the printer.
- -q Help the printer is connected to RADIAN.
- -i Run the printer attached to line.
- -t Write data received on line.
- -s Not generally recommended and should be used only if all other attempts to establish a reliable connection fail.

Only one bitmap is printed on each logical page, and each of the input files must contain contents of at least one bitmap. Decreasing the pattern size with the -b option may help throughput on printers with fast processors (such as PS-810s), while increasing the page size often is the right move on older models (such as PS-800s).
