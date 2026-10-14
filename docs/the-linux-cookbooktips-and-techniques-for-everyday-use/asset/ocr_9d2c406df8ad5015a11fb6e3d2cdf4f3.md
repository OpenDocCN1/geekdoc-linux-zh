# 16.2 Converting Plain Text for Output

@sf(Debian): `enscript`
@sf(WWW): http://www.iki.fi/~mtr/enscript/
The simplest way to typeset plain text is to convert it to PostScript. This is often done to prepare text for printing; the original source text file remains as unformatted text, but the text of the printed output is formatted in basic ways, such as being set in a font.

The main tool for converting text to PostScript is called `enscript`; it converts the text file that is specified as an argument into PostScript, making any number of formatting changes in between. It's great for quickly making nice output from a plain text file—you can use it to do things such as output text in a font of your choosing, or paginate text with graphical headers at the top of each page.

By default, `enscript` paginates its input, outputs it in a 10-point Courier font, and puts a simple header at the top of each page containing the file name, date and time, and page number in bold. Use the `-B` option to omit this header.

If you have a PostScript printer connected to your system, `enscript` can be set up to spool its output right to the printer. You can verify if your system is set up this way by looking at the `enscript` configuration file, `/etc/enscript.cfg`. The line

```
DefaultOutputMethod: printer
```

specifies that output is spooled directly to the printer; changing it to `stdout` instead of `printer` sends the output to the standard output instead.

Even if your default printer does not natively understand PostScript, it may be able to take `enscript` output, anyway. Most Linux installations these days have print filters set up so that PostScript spooled for printing is automatically converted to a format the printer understands (if your system doesn't have this setup for some reason, convert the PostScript to a format recognized by your printer with the `gs` tool, and then print that—see Converting PostScript).

+   - To convert the text file `saved-mail` to PostScript, with default formatting, and spool the output right to the printer, type:

```
$ enscript saved-mail RET
```

To write the output to a file instead of spooling it, give the name of the file you want to output as an argument to the `-p` option. This is useful when you don't have a PostScript printer and you need to convert the output first, or for when you just want to make a PostScript image file from some text, or for previewing the output before you print it. In the latter case, you can view it on the display screen with a PostScript viewer application such as `ghostview` (see section Previewing a PostScript File).