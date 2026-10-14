
## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## UNIX Printing Primer

In this book, I sort of neglected telling you how to print files, partly because if you are using a word processor such as StarOffice, WordPerfect, or Applix, these programs already know how to print without going through this fuss (StarOffice is included on the CD that comes with this book.)

If you want to do UNIX text processing from the command line (as contrasted with word processing in a GUI), there are a few things you need to know that will affect the final presentation of the document you print. Printing under Linux and UNIX is radically different from printing under Windows or the Macintosh. Printing from the command line involves three steps:

- 1. Create a document with a text editor, adding any formatting commands to it as you need. These formatting commands, or macros, will depend on the formatting program you use. However, the idea of text markup (text processing, as UNIX folks like to call it) is the same.
- 2. Run your document through one or more filters (some filters might be as basic as the fmt command I talked about earlier); the final filter will typically produce a file that contains all the necessary printer control codes to render your document. Sometimes, the filter can send this output directly to the printer.
- 3. Send your filtered file to the printer using a program called lpr.

If you only need to print a plain text file, you'll have to do several things. The program you use will depend on the type of printer you have. Typically, printers are separated into two camps: those that have PostScript and those that don't.

If your printer has PostScript support, you'll probably use a program called enscript. If not, you'll use a program called pr. At the surface level, these programs are equivalent—save that enscript harnesses features available to PostScript so it has a lot more of them. These programs at the basic level allow you to specify margins, headers, and length of a line of text.

Not fancy, but they provide the basic formatting capabilities you need to generate a reasonably plain-looking document.

Here’s an example. If you wanted to print a text file called intro.txt, you would send it to pr:

```
pr intro.txt
```

The same file sent to a PostScript printer would be done like this:

```
enscript intro.txt
```

Both pr and enscript can send their output to the printer, and that is what they will do by default. That aside, these basic invocations will hardly produce the output you expect. What are the page margins? Where do the lines fold? You get the idea. You need to set up all these options on pr or enscript, or your document will use your printer’s default settings. Your defaults will be something like left and top margins 1/2" from the edge of the paper, line length of about 72 characters wide, and Courier (typewriter) typeface—more than likely not what you want. So what are you to do?

The first thing you need to do is read the man page and figure out the default settings you want for pr or enscript. In addition to those, you might have to use another formatting command such as fmt. When you figure out the various settings, you just use them over and over.

My typical enscript session goes something like this:

```
[alberto@digital alberto]$ fmt -w 65 intro.txt | enscript --margins=100:100:100:100 -h -B
[ 1 pages * 1 copy ] sent to printer
```

I use fmt to create lines that are about 65 characters wide and then pipe the output to enscript. I set the options for the margins at 100 pixels (72 pixels = 1"), and with the -h option, I suppress the printing of the banner page (a page that tells who printed the file and wastes paper). The -B option suppresses the printing of the header line that usually shows the document title, the last time it was saved, and the page number.

I could produce similar output using pr like this:

```
fmt -w 65 intro.txt | pr -o 15
```

The -o option specifies the number of characters for the left margin; 15 characters is about 1.5".

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## UNIX Text Processing

To produce fancier output, such as bold text, different typefaces, and so on, you need to use one of UNIX's formatters such as groff (GNU's version of the traditional troff formatting program). If you look at the source of a man page, you'll see the formatting codes that you use with groff. (To see the source, use zless on any document inside of /usr/man/man1/). Here's an example of what you'll see:

```
.TH man 1 "September 2, 1995"
.LO 1
.SH NAME
man \- format and display the on-line manual pages
.br
manpath \- determine user's search path for man pages
.SH SYNOPSIS
man [\-acd fhkKtwW] [\-m system] [\-p string] [\-C config_file] [\-M path] [\-P pager] [\-S section_list] [section] name ...
.SH DESCRIPTION
.B man
formats and displays the on-line manual pages. This version knows about the
.B MANPATH
and
.B (MAN) PAGER
environment variables, so you can have
your own set(s) of personal man pages and choose whatever program you like to display the formatted pages. If
.I section
is specified,
.B man
only looks in that section of the manual.
You may also specify the order to search the sections for entries
```

As you can see from this source text, groff (troff!) formatted files don't have any blank lines. Formatting commands (macros) must begin at the left margin. The name of the macro usually begins with a dot (.) or an apostrophe ('). Formatting continues until another macro overrides it.

The macros you use will depend on the type of document you are designing. The macros in the preceding listing are designed for formatting UNIX manual pages. Man, for example, defines macros such as .B for bold and .I for italics and more complex macros for defining headers, descriptions, and so on. If you have ever composed an HTML page using a text editor, formatting text from the UNIX command line is not all that different (conceptually anyway), except for the markup tags. Markup tags will change depending on the macro package you use. For example, another package called ms provides formatting for papers.

As you might have figured out, what you can do in reality depends on the macros you have. Besides the man macros mentioned earlier, other libraries such as ms, mm, and me are used to format other types of documents (see groff_ms, groff_mm, man, and me in section 7 of the UNIX manual; to get there, type man 7 keyword). The codes and how they format the document differ from package to package.

When your text is formatted in this (somewhat perverse) way, you can generate text, PostScript, HTML, output for LaserJet printers and other formats using the groff command. The resulting file is what you then send to the lpr command to print it. The lpr command takes whatever you give it and spools it to the printer. The syntax looks like this:

```
nroff -Tps -macropackage filename | lpr
```

Substitute macropackage with the name of the macros (man for man pages, ms, me, mm, and so on) and filename with the name of your file.

As you can tell, there’s quite a bit that you need to know in order to produce a simply formatted document. UNIX text processing doesn’t end with groff. Other more sophisticated typesetting systems such as TeX and LaTeX can produce professionally formatted documents. Many printed technical publications are developed and printed using TeX and LaTeX.

So why all the complication? The intent of the UNIX command-line printing system is to produce files with any text editor that can display and print properly to a wide range of devices, including the screen. So you can generate man pages, print them on paper, generate HTML pages, and generate pdf (Adobe Acrobat) files, all from the same formatted file. If you want simply to use word processing or desktop publishing, stick to a GUI word processor such as the one included in StarOffice. It will save you time when all you need is a nice-looking document printed on paper.
