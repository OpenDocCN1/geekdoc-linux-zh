
## 21. PostScript

```
@sf(Debian): 'gs'
@sf(Debian): 'psutils'
@sf(WWW): http://www.gnu.org/pub/gnu/ghostscript/
@sf(WWW): http://ftp.dcs.ed.ac.uk/pub/ajcd/
@sf(WWW): http://www.cappella.demon.co.uk/tinyfiles/tinymenu.html
```

PostScript is a programming language, used to describe the way a "page" (usually a physical sheet of paper) should look. PostScript files are text files containing the PostScript commands for drawing images to be printed on pages.

Like plain text files, PostScript files are commonly found on the Internet (and are used by commercial printers) because, as with plain text, they can be shared across platforms and hardware without difficulty. The same PostScript file can be output on a high-end display or printed on a low-end printer, to the best of that hardware's capability. PostScript is a compact and elegant format.

While it's possible to write directly in the PostScript language, and some people have become adept at programming PostScript, so many tools and applications convert files to and from PostScript that you don't have to. See section Converting Plain Text for Output, for a way to convert plain text into PostScript.

Ghostscript is a free implementation of the PostScript language. The gs tool is a Ghostscript interpreter that is used to convert files from PostScript to other formats, usually for printing to a non-PostScript printer (see section Preparing a PostScript File for Printing). The ghostview tool is used to preview PostScript files on the screen (see section Previewing a PostScript File).

EPS, or Encapsulated PostScript, is a file format that describes the contents of a box within a page. EPS files can be embedded in the page of a PostScript file, and are therefore commonly used when inserting an illustration into a document (for example, all of the illustrations in the Cookbook are EPS format files). You can view and print EPS files just as you would PostScript files.

This chapter includes recipes for formatting and manipulating PostScript files. Recipes are separated according to whether they work on the individual, logical pages in a PostScript file (the numbered pages in the file that are not necessarily the physical pages of output), and those that work on the entire file as a whole.

Unless otherwise indicated, the tools in this chapter are part of Angus Duggan's PSUtils package. These tools can be useful for other purposes than those described below; see their respective man pages for more details.

- 21.1 Manipulating PostScript Pages Manipulating the pages of a PostScript file.
- 21.2 Manipulating PostScript Documents Manipulating a PostScript file as a whole.
- 21.3 Converting PostScript Converting PostScript to other formats.

# The Linux Cookbook: Tips and Techniques for Everyday Use:

Give the pages to select as arguments to the `-p` option; you can list single pages and ranges of pages separated by commas. Give ranges as two numbers between a hyphen; thus, `4-6` specifies pages four through six, inclusive. If you omit the first number in a pair, the first page is assumed, and if you omit the last number, the last page is assumed. Pages are written to the new file in the order they are specified.

To select page 47 from the PostScript file `newsletter.ps` and output it to the file `selection.ps`, type:

```
$ psselect -p47 newsletter.ps selection.ps RET
```

- To select the first ten pages, page 104, pages 23 through 28, and page 2 from the file `newsletter.ps` and write it to the file `selection.ps`, type:

```
$ psselect -p1-10,104,23-28,2 newsletter.ps selection.ps RET
```

In the preceding example, page 2 is selected twice.

Prefix a number with an underscore (`_`) to indicate that the given page number is relative to the last page, counting backwards toward the first page.

- To select the second-to-last through the tenth-to-last pages from the PostScript file `newsletter.ps` and output them to the file `selection.ps`, type:

```
$ psselect -p_2-_10 newsletter.ps selection.ps RET
```

- To select the second-to-last through the tenth pages from the PostScript file `newsletter.ps` and output them to the file `selection.ps`, type:

```
$ psselect -p_2-10 newsletter.ps selection.ps RET
```

Use the `-e` option to select all even-numbered pages, and use the `-o` option to select all odd-numbered pages.

- To select all of the even pages in the file `newsletter.ps` and write them to a new file, `even.ps`, type:

```
$ psselect -e newsletter.ps even.ps RET
```

- To select all of the odd pages in the file `newsletter.ps` and write them to a new file, `odd.ps`, type:

```
$ psselect -o newsletter.ps odd.ps RET
```
