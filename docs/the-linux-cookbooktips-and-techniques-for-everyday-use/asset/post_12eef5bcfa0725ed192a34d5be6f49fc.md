
```
$ enscript -B -f "Helvetica12" saved-mail RET
```

- To make a PostScript file called `saved-mail.ps` containing the contents of the text file `saved-mail`, with text set in the Helvetica font at 12 points, type:

```
$ enscript -B -f "Helvetica12" -p saved-mail.ps saved-mail RET
```

The `-B` option was used in the preceding examples to omit the output of a header on each page. When headers are used, they're normally output in 10-point Courier Bold; to specify a different font for the text in the header, give its name as an argument to the `-F` option.

- To print the contents of the text file `saved-mail` to a PostScript printer, with text set in 10-point Times Roman and header text set in 18-point Times Bold, type:

```
$ enscript -f "Times-Roman10" -F "Times-Bold18" saved-mail RET
```

- To make a PostScript file called `saved-mail.ps` containing the contents of the text file `saved-mail`, with text and headers both set in 16-point Palatino Roman, type:

```
$ enscript -f "Palatino-Roman16" -F "Palatino-Roman16" -p saved-mail.ps saved-mail RET
```

## 16.2.2 Outputting Text as a Poster or Sign

You can output any text you type directly to the printer (or to a PostScript file) by omitting the name of the input file; enscript will read the text on the standard input until you type C-d on a new line.

This is especially useful for making a quick-and-dirty sign or poster--to do this, specify a large font for the text, such as Helvetica Bold at 72 points, and omit the display of default headers.

- To print a sign in 72-point Helvetica Bold type to a PostScript printer, type:

```
$ enscript -B -f "Helvetica-Bold72" RET
RET
CAUTION RET
RET
WET PAINT! RET
C-d
```

72-point type is very large; use the `--word-wrap` option with longer lines of text to wrap lines at word boundaries if necessary. You might need this option because at these larger font sizes, you run the risk of

making lines that are longer than could fit on the page. You can also use the `-r` option to print the text in landscape orientation, as described in Outputting Text in Landscape Orientation.

- To print a sign in 63-point Helvetica Bold across the long side of the page, type:

```
$ enscript -B -r --word-wrap -f "Helvetica-Bold63" RET
RET
RET
CAUTION -- WET PAINT! RET
C-d
```

NOTE: To make a snazzier or more detailed message or sign, you would create a file in a text editor and justify the words on each line in the file as you want them to print, with blank lines where necessary. If you're getting that complicated with it, it would also be wise to use the `-p` option once to output to a file first, and preview the file before printing it (see section Previewing a PostScript File).

[ < ] [ > ] [ << ] [ Up ] [ >> ] [Top] [Contents] [Index] [ ? ]

## 16.2.3 Outputting Text with Language Highlighting

The enscript tool currently recognizes the formatting of more than forty languages and formats, from the Perl and C programming languages to HTML, email, and Usenet news articles; enscript can highlight portions of the text based on its syntax. In Unix-speak, this is called pretty-printing.

The following table lists the names of some of the language filters that are available at the time of this writing and describes the languages or formats they're used for.

| FILTER | LANGUAGE OR FORMAT |
| ada | Ada95 programming language. |
| asm | Assembler listings. |
| awk | AWK programming language. |
| bash | Bourne-Again shell programming language. |
| c | C programming language. |
| changelog | ChangeLog files. |
| cpp | C++ programming language. |
| csh | C-Shell script language. |
| delphi | Delphi programming language. |
| diff | Normal "difference reports" made from diff. |
| diffu | Unified "difference reports" made from diff. |
| elisp | Emacs Lisp programming language. |
| fortran | Fortran77 programming language. |
| haskell | Haskell programming language. |

### The Linux Cookbook: Tips and Techniques for Everyday Use:

| html | HyperText Markup Language (HTML). |
| idl | IDL (CORBA Interface Definition Language). |
| java | Java programming language. |
| javascript | JavaScript programming language. |
| ksh | Korn shell programming language. |
| m4 | M4 macro processor programming language. |
| mail | Electronic mail and Usenet news articles. |
| makefile | Rule files for make. |
| nroff | Manual pages formatted with nroff. |
| objc | Objective-C programming language. |
| pascal | Pascal programming language. |
| perl | Perl programming language. |
| postscript | PostScript programming language. |
| python | Python programming language. |
| scheme | Scheme programming language. |
| sh | Bourne shell programming language. |
| skill | Cadence Design Systems Lisp-like language. |
| sql | Sybase 11 SQL. |
| states | Definition files for states. |
| synopsys | Synopsys dc shell scripting language. |
| tcl | Tcl programming language. |
| tcsh | TC-Shell script language. |
| vba | Visual Basic (for Applications). |
| verilog | Verilog hardware description language. |
| vhdl | VHSIC Hardware Description Language (VHDL). |
| vrml | Virtual Reality Modeling Language (VRML97). |
| zsh | Z-shell programming language. |

To pretty-print a file, give the name of the filter to use as an argument to the `-E` option, without any whitespace between the option and argument.

- To pretty-print the HTML file `index.html`, type:

```
$ enscript -Ehtml index.html RET
```

- To pretty-print an email message saved to the file `important-mail`, and output it with no headers to a file named `important-mail.ps`, type:

```
$ enscript -B -Email -p important-mail.ps important-mail RET
```
