
# postprint

# postprint — PostScript Translator for Text Files

# Synopsis

```
/usr/lib/lp/postprint [-c num] [-f name] [-l num] [-m num] [-n num]
[-o list] [-p mode] [-r num] [-s num] [-t num] [-x num] [-y num]
[file...]
/usr/lib/lp/postscript/postprint
```

# Description

The postprint filter translates text files into PostScript and writes the results to the standard output. If you specify no files or if - is one of the input files, the standard input is read.

# Options

- -c num copies of each page. By default, print only one copy.
- -f name files, using font name. You can use PostScript font, although the best results are obtained with constant-width fonts. The default font is Courier.
- -l num Set the length of a page to lines. By default, num is 66. Setting num to 0 is allowed, and postprint guesses a value, based on the page size.
- -m num Magnify each logical page by the factor num. Scale pages uniformly about the origin, which is located near the upper-left corner of each page. The default magnification is 1.0.
- -n num Print num logical pages on each piece of paper where num can be any positive integer. By default, num is set to 1.
- -o list Print pages whose numbers are given in the comma-separated list. The list contains multiple number ranges N1-N2. A missing N1 means the lowest-numbered page, a missing N2 means the highest. The page range is an expression of logical pages instead of physical sheets of paper. For example, if you are printing two logical pages to a sheet and you specified a range of 4, then two sheets of paper containing four layouts would print. If you specified a page range of 3-4 when requesting logical pages to a sheet, only page 3 and 4 layouts would print and they would appear on one physical sheet of paper.
- -p mode Print files in either p (portrait) or l (landscape) mode. Only the first character of mode is significant. The default mode is portrait.
- -r num Choose Return behavior. Ignore Returns if num 0, go to column 1 if num is 1, and generate a newline if num is 2. The default num is 0.
- -s num Print files, using point size num. When printing in landscape mode, scale num by a factor that depends on the imaging area of the device. The default size for portrait mode is 10. Note that increasing point size increases virtual image size, so you either need to load larger paper or use the -l option to scale the number of lines per page.
- -t num Assume Tabs are set every num columns, starting with the first column. By default, Tabs are set every 8 columns.
- -x num Translate the origin num inches along the positive x axis. The default coordinate system has the origin fixed near the upper-left corner of the page, with x to the right and y down the page. Positive num moves everything to the right. The default offset is 0.25 inches.
- -y num Translate the origin num inches along the positive y axis. Positive num moves text up the page. The default offset is -0.25 inches.

A new page is started after 66 lines have been printed on the current page or whenever an ASCII character is read. You can change the number of lines per page with the -l option. Unprintable ASCII characters are ignored, and lines that are too long are silently truncated by the printer.

# Examples

The following example prints file1 and file2 in landscape mode.
```
lpr postprint -pl file2
```

The following example prints three logical pages on each physical page in portrait mode.
```
lpr postprint -n3 file
```

# Exit Status

- 0 Successful completion.
- non-zero An error occurred.

# Files

```
/usr/lib/lp/postscript/forms.ps
/usr/lib/lp/postscript/ps.requests
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | numpsf |

# See Also

```
download(1), dpost(1), postdaisy(1), postmd(1), postio(1), postreverse(1), posttek(1), attributes(5)
```

# postreverse

# postreverse — Reverse the Page Order in a PostScript File

# Synopsis

```
/usr/lib/lp/postreverse [-o list] [-r] [file]
/usr/lib/lp/postscript/postreverse
```

# Description

The postreverse filter reverses the page order in files that conform to Adobe's Version 1.0 or Version 2.0 file structuring conventions and writes the results to the standard output. Only one input file is allowed, and if you specify no file, the standard input is read.

The postreverse filter can handle a limited class of files that violate page independence, provided global definitions are bracketed by %%BeginGlobal and %%EndGlobal; label ordinal commands also mark the end of each page with %%EndPage label reverse order properly, provided the prologue and trailer sections can be located. If postreverse fails to find an %%Prolog or %%EndSetup, the entire file is copied, unmodified, to the standard output.

Because global definitions are extracted from individual pages and put in the prologue, the output file can be minimally conforming if the input file was not.

> Note — No attempt has been made to redefinitions of global variables or procedures. If standard input is used, the input file is read three times before being reversed.

# Options

- -o list Print pages whose are given in the comma-separated list. The list contains single numbers N and ranges NI-NJ. A missing NI means the lowest-numbered page, a missing NJ means the highest. The page range is an exception of logical pages instead of physical sheets of paper. For example, if you are printing two logical pages to a sheet and you specified a range of 4, then two sheets containing four page layouts would print. If you specify a range of 3-4 when requesting page 3 and page 4 layouts would print and they would appear on one physical sheet of paper.
- -r Do reverse the pages in file.

# Examples

The following example reverses pages 1 to 100 from file.
```
lpr postreverse -ol1-100 file
```

The following example prints four logical pages on each physical page and reverses all pages.
```
lpr postprint -n4 file | postreverse
```

The following example produces a minimally conforming file from output generated by dpost without reversing the pages.
```
dpost file | postreverse -r
```

# Exit Status

- 0 Successful completion.
- non-zero An error occurred.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNwpsf |

# See Also

download(1), dpost(1), postdaisy(1), postmd(1), postio(1), postmd(1), postprint(1), posttek(1), attributes(5)

# posttek

# posttek — PostScript Translator for Tektronix 4014 Files

# Synopsis

```
/usr/lib/lp/posttek [-c num] [-f name] [-m num] [-n num] [-o list]
[-p mode] [-w num] [-x num] [-y num] [file...]
/usr/lib/lp/postscript/posttek
```

# Description

The posttek filter translates Tektronix 4014 graphics files into PostScript and the results to the standard output. If you specify no files or if - is one of the input files, the standard output is read.

> Note — The line width is too small for write-white print engines such as the one used by the PS-2400.

# Options

- -c num Print num copies of each page. By default, only one copy is printed.
- -f name Print text, using font name. You can use any PostScript font, although the best results are obtained with constant-width fonts. The default font is Courier.
- -m num Magnify each logical page by the factor num. Scale pages uniformly about the origin which is located near the upper-left corner of each page. The default magnification is 1.0.
- -n num Print num logical pages on each page of paper, where num can be any positive integer. By default, num is set to 1.
- -o list Print pages whose numbers are given in the comma-separated list. The list contains single number NI and ranges NI-N2. A missing NI means the lowest-numbered page, a missing N2 means the highest. The page range is an expression of logical pages instead of physical sheets of paper. For example, if you are printing two logical pages to a sheet and you specified a range of 4, then two sheets of paper containing four layouts would print.
- -p mode Print files in either p (portrait) or l (landscape) mode. Only the first character of mode is significant. The default mode is portrait.
- -w num Set the line width for graphics to num points, where a point is approximately 1/72 of an inch. By default, num is set to 0 points, which forces lines to be 1 pixel wide.
- -x num Translate the origin num inches along the positive x axis. The default coordinate system has the origin fixed at the center of the page, with positive x to the right and positive y up the page. Positive num moves everything right. The default offset is 0.0 inches.
- -y num Translate the origin num inches along the positive y axis. Positive num moves everything up the page. The default offset is 0.0.
