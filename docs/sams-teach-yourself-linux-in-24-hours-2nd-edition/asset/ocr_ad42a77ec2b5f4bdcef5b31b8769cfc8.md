Not all the output is shown, but as you can see, the fmt command is used to convert the text stream into a 26-character wide column. This output is then fed to pr, which formats the text in two columns. The -s option is followed by a backslash (\ ) and a vertical bar (|) to specify the vertical bar as a column separator. The -o option sets the left margin to two spaces, and the -t option turns off headers and footers. The -w 60 option sets a page width of 60 characters, which is certainly suitable for most printers.

But what if you want to save paper and see at least two pages of output on a single page? In this case, use the mpage, or multiple page, command to print several sheets of paper on a single page. Look at the following example:

```
# mpage -2 myfile.txt >myfile.ps
```

This command line uses the mpage command, found under the /usr/bin directory, to create a PostScript file you can later print that contains the contents of the myfile.txt document as two side-by-side pages on each sheet of paper. To preview the PostScript file during an X11 session, use the gv previewer, like this:

```
# gv myfile.ps
```

![](bbox=[0.25, 0.7, 0.35, 0.78])

> You can use the mpage command's -O, -E, or -R options to print full-duplex (back-to-back) documents. This can be handy for producing small booklets using letter-size paper with a printer that's not capable of printing on both sides of each sheet. You also can set different margins, fonts, and the order of printed pages. See the mpage manual page for details.

Using the fmt, pr, or mpage commands, along with other text filters, you can perform quick and dirty rudimentary text formatting. If you want to try more complex formatting, use a text formatting program.

# Formatting Text with the groff Formatter

If you've used OpenLinux for the past several hours and have read some manual pages, you're probably familiar with at least one complex formatting program: groff. When you read a manual page with

```
# man ls
```

it is equivalent to the following:

```
# nroff -man /usr/man/man1/ls.1 | less
```