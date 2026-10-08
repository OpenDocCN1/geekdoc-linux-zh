# Advanced Bash-Scripting Guide

printing or viewing on screen. Various options permit row and column manipulation, joining lines, setting margins, numbering lines, aligning page headers, and merging files, among other things. The pr command brings much of functionality of nl, paste, fold, column, and expand.

```
pr -o 5 --width=65 fileZZZ | more gives a paginated list to screen of
fileZZZ with margins at 5 and 65.
```

A particularly useful option is -d, forcing double-spacing (same effect as sed -G).

The gettext package is a set of utilities for localizing and translating the text output of programs into foreign languages. While originally intended for C programs, it now supports a number of programming and scripting languages.

The gettext program works on shell scripts. See the info page.

A program for generating binary message catalogs. It is used for localization.
A utility for converting file(s) to a different encoding (character set). Its chief use is for localization.

```
# Convert a string from UTF-8 to UTF-16 and print to the BookList
function write_utf8_string {
STRING=$$
BOOKLIST=$2
echo -n "$STRING" | iconv -f UTF8 -t UTF16 | \
tcut -b 3 | tr -d \n >> "$BOOKLIST"
}
```

```
# From Peter Knowles "booklistgen.sh" script
## for converting files to Sony Libre/PRS-50 format.
## (http://booklistgensh.peterknowles.com)
```

Consider this fancy version of iconv, above. This very versatile tool for converting a file to a different encoding scheme. Note that recode is not part of the standard Linux installation.

Tex and Postscript are mark languages used for printing or formatted video display.
Tex is Donald Knuth's elaborate typesetting system. It is often convenient to write a shell script encapsulating all the options and arguments passed to one of these languages.

Ghostscript (gs) is a GPL-ed Postscript interpreter.

Utility for processing pdf files. Found in /usr/bin on many Linux distros, is actually a shell wrapper that uses Perl to invoke Tex.

```
texec --pdfrange --result=Concatenated.pdf
# Concatenate all the pdf files in the current working directory
## into the merged file, Concatenated . .
# (--pdfpage option repaginates a pdf file. See also --combine)
# The above command-line could be parameterized and put into a shell script.
```

Utility for converting plain text to PostScript

# Chapter 16. External Filters, Programs and Commands