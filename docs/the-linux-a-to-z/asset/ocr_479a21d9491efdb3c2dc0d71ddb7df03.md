# 5.4 Other Tools

There are several other tools available under Linux that are worth mentioning at this time. The first of these is the pr command. The function of this command is to split a file up into pages of the correct size to send to a printer. By default, the pages have a heading inserted which contains the date and time, the file name and the page number:

```
```
$ pr pw.test

Jun 1 09:20 1995 pw.test Page 1

root:awmku76tr43d6:0:0::/root/:/bin/sh
pc:bdhd74hs9jh3h:500:50::/usr1/pc:/bin/bash
carey:esJ9ohd8HH89i:501:50::/usr1/carey:/bin/bash
mot:dhjd83kjdJS6D:1500:60::/usr1/mot:/bin/bash
grex:cj8AjoWE8h8fs:1500:60::/usr1/mot:/bin/sh
```
```

It is also possible to use the -n command line switch to get the pr command to add line numbers to the text:

```
```
$ pr -n pw.test

Jun 1 09:20 1995 pw.test Page 1

1 root:awmku76tr43d6:0:0::/root/:/bin/sh
2 pc:bdhd74hs9jh3h:500:50::/usr1/pc:/bin/bash
3 carey:esJ9ohd8HH89i:501:50::/usr1/carey:/bin/bash
4 mot:dhjd83kjdJS6D:1500:60::/usr1/mot:/bin/bash
5 grex:cj8AjoWE8h8fs:1500:60::/usr1/mot:/bin/sh
```
```

The next command to look at is called od. This command allows you to examine the contents of a text or data file as a set of bytes. Each line of output consists of a number which is the current byte offset into the file followed by a set of sixteen byte values. All the data byte and offset values in the output can be displayed in several formats, including ASCII characters, and octal or hexadecimal numbers:

```
```
$ od /tmp/text/motd
0000000 064514 072556 020170 027061 027062 027061 024040 047520
0000020 044523 024530 005056
0000026
```
```

The default display from od is all in octal, which is where it gets its name from (Octal Dump). This is not usually the most useful display however, and a more informative output can be created with the display set, for instance, to a combination of ASCII characters and hexadecimal values: