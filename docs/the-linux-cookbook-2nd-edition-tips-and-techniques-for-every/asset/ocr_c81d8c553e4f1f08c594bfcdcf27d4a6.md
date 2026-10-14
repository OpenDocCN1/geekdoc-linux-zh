⇒ To make a PostScript file from myfile.sgml, type:

```
$ linuxdoc -B latex myfile.sgml [RET]
$ latex myfile.latex [RET]
$ dvips -t letter -o myfile.ps myfile.dvi [RET]
$
```

In this example, linuxdoc writes a LaTeX input file from the SGML source file, and then the latex tool processes the LaTeX file to make DVI output, which is processed with dvips to get the final output: a PostScript file called myfile.ps with a paper size of “U.S. letter” (8.5 in×11 in).

To make a PDF file from the PostScript file, you need to take one more step and use ps2pdf, part of the gs (Ghostscript) package; this converts the PostScript to PDF.

⇒ To make a PDF file from the PostScript file myfile.ps, type:

```
$ ps2pdf myfile.ps myfile.pdf [RET]
```

# 15.7 Using Other Word Processors and Typesetting Systems

The following table describes other suggested word processors and typesetting tools available for Linux.

AbiWord
A graphical, WYSIWYG-style word processor for Linux systems. It can read Microsoft Word files and is reportedly similar to that famous word processor in some ways.
DEB: abiword-common
RPM: abiword
WWW: http://www.abisource.com/

ImPress
Full-featured, WYSIWYG layout and desktop publishing system.
DEB: impress
RPM: impress
WWW: http://www.ntlug.org/~ccox/impress/index.html