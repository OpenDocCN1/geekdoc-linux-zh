# 21.3 Converting PostScript

These recipes show how to convert PostScript files to other formats. See also the recipes for preparing PostScript files for printing. Preparing a PostScript File for Printing.

21.3.1 Converting PostScript to PDF

21.3.2 Converting PostScript to Plain Text

Converting PostScript to plain text.

# 21.3.1 Converting PostScript to PDF

Use ps2pdf, part of the gs "Ghostscript" package, to convert a PostScript file to PDF. Give as arguments the name of the PostScript file to read from, and the name of the PDF file to write to.

+   - To make a PDF file `sutra.pdf` from the input file `sutra.ps`, type:

```
$ ps2pdf sutra.ps sutra.pdf RET
```

This command writes a new file in PDF format called `sutra.pdf`. The original file, `sutra.ps`, is not altered.

NOTE: To make proper PDF conversions, make sure that you have gs version 6.01 or higher installed: use the `-v` option with gs to output the installed version.

# 21.3.2 Converting PostScript to Plain Text

To convert a PostScript file to plain text, use ps2ascii. Give as arguments the name of the PostScript file to read from, and the name of the text file to write to.