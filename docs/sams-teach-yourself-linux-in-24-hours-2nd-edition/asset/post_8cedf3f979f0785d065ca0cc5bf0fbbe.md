
| Option | Description |
|---|---|
| -e[x[y]] | Convert tabs (or x) to spaces, use y tab character width |
| -f, -F | Output form feed between pages |
| -h str | Use str as page header instead of filename |
| -l[x[y]] | Convert spaces (or x) to tabs, use y spaces in tabs |
| -l xx | Page length set to xx |
| -m | Print multiple files in parallel columns on page |
| -n[x[y]] | Use line numbers (with a following character x), and y digits for the numbers |
| -o x | Set left margin to x |
| -r | Turn off warning messages |
| -s[x] | Use character x to separate columns |
| -t | Turn off default headers and footers |
| -v | Show unprintable characters in base 8 (octal notation) |
| -w xx | Set page width to xx characters |
| -x | Format page into x columns |

Look at the following example:

```
# pr +4 -h "Draft Number 1" -o 8 <pilotprimer.txt > output.txt
```

This command line formats the file pilotprimer.txt, starting at page 4, with a header containing the date, time, page number, and the words Draft Number 1; the left margin is 8 spaces. Using the > redirection operator, the formatted output is then saved to a file called output.txt, which you can print at a later time.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_360_0.png)

> Pipe the output through the less pager to preview your formatting before printing.

The pr program also formats selected streams of text. One handy use is to create formatted columns. For example, if you have a paragraph, you can quickly create columns of text by combining several filter programs and then formatting the text with the -COLUMN command-line option (a hyphen, followed by the number of columns; -3 in the following example):

```
# cat cities.txt
Cincinnati, San Francisco, Philadelphia, Chicago, Miami, Norfolk,
Savannah, Seattle, Pittsburgh, St. Louis, Phoenix, Nashville, Las Vegas,
Atlantic City, Raleigh
# cat cities.txt | sed 's/, /#/g' | tr '#' '\n' | sort | pr -l 1 -w 1 -3
Atlantic City      Chicago            Cincinnati
Las Vegas          Miami              Nashville
Norfolk            Philadelphia        Phoenix
Pittsburgh         Raleigh             San Francisco
Savannah           Seattle             St. Louis
```

The preceding example uses a list of cities separated by commas. By using several filters, including the pr command, the text is formatted as a readable list, sorted alphabetically. The command line works by first using the sed stream editor (discussed in Hour 14) to change each comma and space to a pound (#) sign. The pound sign is translated to a carriage return by the tr command (also discussed in Hour 14). The text, now a list of words, one per line, is fed into the sort command. The sorted text is fed into the pr command to produce three columns of text (the -l (or page length) option, with a value of 1, is used to inhibit the page header).

You also can use the fmt command with the pr command to change the word wrap, or width, of your text documents. The following example is part of a public-domain software license (found under the /usr/doc/shadow-misc directory):

```
# cat LICENSE
...
1. You may make and give away verbatim copies of the source form of the Standard Version of this Package without restriction, provided that you duplicate all of the original copyright notices and associated disclaimers.

2. You may apply bug fixes, portability fixes and other modifications derived from the Public Domain or from the Copyright Holder. A Package modified in such a way shall still be considered the Standard Version.
...
```

Although this text might be okay when printed on the screen or by using the default settings with the pr command, the text overruns lines if you use a left margin of 10 spaces. Look at the following example:

```
# pr -o 10 <LICENSE
...
1. You may make and give away verbatim copies of the source fo
rm of the
Standard Version of this Package without restriction, provided
that you
duplicate all of the original copyright notices and associated
disclaimers.
2. You may apply bug fixes, portability fixes and other modifi
cations
Package derived from the Public Domain or from the Copyright Holder. A
version modified in such a way shall still be considered the Standard V
ersion.
...
```

The preceding example certainly doesn't look nice when printed! To fix this, use the fmt command to format the text with a smaller line width before formatting with the pr command:

```
# cat LICENSE | fmt -w 60 | pr -o 10
```

+   1. You may make and give away verbatim copies of the source form of the Standard Version of this Package without restriction, provided that you duplicate all of the original copyright notices and associated disclaimers.
+   2. You may apply bug fixes, portability fixes and other modifications derived from the Public Domain or from the Copyright Holder. A Package modified in such a way shall still be considered the Standard Version.
+   ...

As you can see, the text now fits nicely on your page when printed. You can also create more sophisticated effects by combining the output of fmt with the multiple-column option of the pr command. For example, to format the previous example document, pilotprimer.txt, use the fmt command to reformat the text into a thin column of 26 characters, and then send the text through the pr command to format the text into multiple columns, like this:

```
# fmt -26 <pilotprimer.txt | pr -2 -s\| -o 2 -t -w 60
```

| HACKING THE 3COM PALM
PILOT PERSONAL DIGITAL
ASSISTANT

Although most manufacturers tout their brand of Personal Digital Assistant, or PDA, as the 'easiest to use,' or most 'convenient' device, when it comes to connecting to the Internet, novice PDA and Internet users may still have a hard time in making that first connection to | Information You Need
to Connect

There are several things you need to know before you can starting web browsing, Usenet news reading, or sending and receiving email on your Pilot. When you signed up for your Internet service, you should have received an information packet from your ISP. This information should include: |

Not all the output is shown, but as you can see, the fmt command is used to convert the text stream into a 26-character wide column. This output is then fed to pr, which formats the text in two columns. The -s option is followed by a backslash (\ ) and a vertical bar (|) to specify the vertical bar as a column separator. The -o option sets the left margin to two spaces, and the -t option turns off headers and footers. The -w 60 option sets a page width of 60 characters, which is certainly suitable for most printers.

But what if you want to save paper and see at least two pages of output on a single page? In this case, use the mpage, or multiple page, command to print several sheets of paper on a single page. Look at the following example:

```
# mpage -2 myfile.txt >myfile.ps
```

This command line uses the mpage command, found under the /usr/bin directory, to create a PostScript file you can later print that contains the contents of the myfile.txt document as two side-by-side pages on each sheet of paper. To preview the PostScript file during an X11 session, use the gv previewer, like this:

```
# gv myfile.ps
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_363_0.png)

> You can use the mpage command's -O, -E, or -R options to print full-duplex (back-to-back) documents. This can be handy for producing small booklets using letter-size paper with a printer that's not capable of printing on both sides of each sheet. You also can set different margins, fonts, and the order of printed pages. See the mpage manual page for details.

Using the fmt, pr, or mpage commands, along with other text filters, you can perform quick and dirty rudimentary text formatting. If you want to try more complex formatting, use a text formatting program.

## Formatting Text with the groff Formatter

If you've used OpenLinux for the past several hours and have read some manual pages, you're probably familiar with at least one complex formatting program: groff. When you read a manual page with

```
# man ls
```

it is equivalent to the following:

```
# nroff -man /usr/man/man1/ls.1 | less
```
