
```
$ date | tr -s ' '
Sun Jun 4 17:27:23 BST 1995
```

The cut command can now be used with a space field delimiter to extract the time of day field (field four):

```
$ date | tr -s ' ' | cut -d' ' -f4
17:27:23
```

The output from this pipeline is now a string which itself consists of three colon delimited fields of which we want to extract the value in the middle field. Again, cut is the ideal solution, as follows:

```
$ date | tr -s ' ' | cut -d' ' -f4 | cut -d: -f2
27
```

A simpler solution to the same problem will still use cut but relies on noticing that all the fields in the output from date are of fixed size. Even when numeric fields are less than 10, so that they are only one digit instead of two, the sizes of the fields are maintained by padding them out. This allows for a solution which uses the -b switch to cut with a range of byte positions carefully calculated to coincide with the field of interest (bytes 15 to 16 in this example):

```
$ date | cut -b15-16
27
```

## 5.3.2 Comparing File Contents

There are several commands available for comparing the contents of two files for any differences. The simplest command is effectively used just to tell you whether or not two files are the same. This command is called cmp. All it does is to compare the two files given as parameters byte by byte until it either finds a difference or until it reaches the end of the files. The general form of the command is:

```
cmp file1 file2
```

If either file1 or file2 is just a hyphen (-) then the text for this file will be taken from the standard input device, which will be from the keyboard unless input redirection is used. The output from the cmp command is the first byte and the line number where the two files differ.

If the lines in the two files to be compared are sorted into order then it is possible to use the comm command to do the comparison between them. The general form for the comm command is:

```
comm options file1 file2
```

If no options are specified then the output from comm is displayed in three columns. Output lines beginning in column 1 are those lines that appear in file1 but not in file2. Column 2 contains the lines that appear in file2 but not in file1 and column 3 lists lines contained in both files.

As an example, let us sort the contents of pw.test into the file pw1.test:

```
$ sort pw.test -o pw1.test
$ cat pw1.test
carey:esJ9ohd8HH89i:501:50::/usr1/carey:/bin/bash
grex:cj8AJoWE8h8fs:1500:60::/usr1/mot:/bin/sh
mot:dhjd83kjdJS6D:1500:60::/usr1/mot:/bin/bash
pc:bdhd74hs9jh3h:500:50::/usr1/pc:/bin/bash
root:awmku76tr43d6:0:0::/root/:/bin/sh
```

Then, modify some of the lines in pw.test with sed and sort the result, sending the sorted output into the file pw2.test:

```
$ sed /pc/,/carey/s/bash/sh/ <pw.test | sort >pw2.test
$ cat pw2.test
carey:esJ9ohd8HH89i:501:50::/usr1/carey:/bin/sh
grex:cj8AJoWE8h8fs:1500:60::/usr1/mot:/bin/sh
mot:dhjd83kjdJS6D:1500:60::/usr1/mot:/bin/bash
pc:bdhd74hs9jh3h:500:50::/usr1/pc:/bin/sh
root:awmku76tr43d6:0:0::/root/:/bin/sh
```

Finally, use comm on the two sorted files to observe the result:

```
$ comm pw1.test pw2.test
carey:esJ9ohd8HH89i:501:50::/usr1/carey:/bin/bash
        carey:esJ9ohd8HH89i:501:50::/usr1/carey:/bin/sh
                grex:cj8AJoWE8h8fs:1500:60::/usr1/mot:/bin/sh
                mot:dhjd83kjdJS6D:1500:60::/usr1/mot:/bin/bash
pc:bdhd74hs9jh3h:500:50::/usr1/pc:/bin/bash
        pc:bdhd74hs9jh3h:500:50::/usr1/pc:/bin/sh
                root:awmku76tr43d6:0:0::/root/:/bin/sh
```

The main options you can specify are -1, -2 and -3 which suppress the output of the corresponding columns. For example, to see just the lines in pw1.test which do not occur in pw2.test you need to suppress the column two and column three outputs, as follows:

```
$ comm -2 -3 pw1.test pw2.test
carey:esJ9ohd8HH89i:501:50::/usr1/carey:/bin/bash
pc:bdhd74hs9jh3h:500:50::/usr1/pc:/bin/bash
```

Similarly, to see only the lines which appear in both files, you need to suppress the output from columns 1 and 2:

```
$ comm -1 -2 pw1.test pw2.test
grex:cj8AjoWE8h8fs:1500:60::/usr1/mot:/bin/sh
mot:dhjd83kjdJS6D:1500:60::/usr1/mot:/bin/bash
root:awmku76tr43d6:0:0::/root/:/bin/sh
```

The other main command for comparing file contents is diff. This command performs a really sophisticated check compared to cmp and comm. In fact, this command will systematically work through a pair of files, which need not be sorted in any way, and display all the lines where the two files differ:

```
$ diff pw1.test pw2.test
1c1
< carey:esJ9ohd8HH89i:501:50::/usr1/carey:/bin/bash
---
> carey:esJ9ohd8HH89i:501:50::/usr1/carey:/bin/sh
4c4
< pc:bdhd74hs9jh3h:500:50::/usr1/pc:/bin/bash
---
> pc:bdhd74hs9jh3h:500:50::/usr1/pc:/bin/sh
```

The lines in the output display which are preceded by a less than (<) symbol are the lines in the first input file which do not match the corresponding lines in the second file. Similarly, lines preceded by a greater than (>) symbol are those contained in the second input file, but not in the first.

## 5.3.3 uniq

Once a file has been manipulated, for example, cut and then ordered with sort, it is possible for there to be duplicate lines in the output file. These duplicate records can be removed from the file to leave only unique instances of each record with the command uniq:

```
$ cat pw.test | cut -d: -f7 | sort | uniq
/bin/bash
/bin/sh
```

This pipeline sends the contents of the file pw.test into the cut command, which extracts each user's shell name (i.e. field seven). This is then piped into sort, which ensures that any pairs of duplicate lines are next to each other in its output. Finally, this sorted list is piped into uniq, which will remove one of any pair of duplicate lines discovered on a pass through its input.

## 5.4 Other Tools

There are several other tools available under Linux that are worth mentioning at this time. The first of these is the pr command. The function of this command is to split a file up into pages of the correct size to send to a printer. By default, the pages have a heading inserted which contains the date and time, the file name and the page number:

```
$ pr pw.test

Jun 1 09:20 1995 pw.test Page 1

root:awmku76tr43d6:0:0::/root/:/bin/sh
pc:bdhd74hs9jh3h:500:50::/usr1/pc:/bin/bash
carey:esJ9ohd8HH89i:501:50::/usr1/carey:/bin/bash
mot:dhjd83kjdJS6D:1500:60::/usr1/mot:/bin/bash
grex:cj8AjoWE8h8fs:1500:60::/usr1/mot:/bin/sh
```

It is also possible to use the -n command line switch to get the pr command to add line numbers to the text:

```
$ pr -n pw.test

Jun 1 09:20 1995 pw.test Page 1

1 root:awmku76tr43d6:0:0::/root/:/bin/sh
2 pc:bdhd74hs9jh3h:500:50::/usr1/pc:/bin/bash
3 carey:esJ9ohd8HH89i:501:50::/usr1/carey:/bin/bash
4 mot:dhjd83kjdJS6D:1500:60::/usr1/mot:/bin/bash
5 grex:cj8AjoWE8h8fs:1500:60::/usr1/mot:/bin/sh
```

The next command to look at is called od. This command allows you to examine the contents of a text or data file as a set of bytes. Each line of output consists of a number which is the current byte offset into the file followed by a set of sixteen byte values. All the data byte and offset values in the output can be displayed in several formats, including ASCII characters, and octal or hexadecimal numbers:

```
$ od /tmp/text/motd
0000000 064514 072556 020170 027061 027062 027061 024040 047520
0000020 044523 024530 005056
0000026
```

The default display from od is all in octal, which is where it gets its name from (Octal Dump). This is not usually the most useful display however, and a more informative output can be created with the display set, for instance, to a combination of ASCII characters and hexadecimal values:

```
$ od -Ax -tcx1 /tmp/text/motd
000000  m  o  t  d    c  o  n  t  e  n  t  s    i  n
6d 6f 74 64 20 63 6f 6e 74 65 6e 74 73 20 69 6e
000010  h  e  r  e  .  \n
20 68 65 72 65 2e 0a
000017
```

The -A switch allows you to specify what format to use for the offset values. The choices are:

- x hexadecimal;
- o octal (default);
- d decimal;
- n no offset output.

The -t switch lets you specify one or more formats in which to display the byte values in the file. The main choices here are:

- xn hexadecimal;
- on octal (o2 is default);
- dn signed decimal;
- un unsigned decimal;
- c ASCII character or backslash sequence.

The number given for n specifies how many bytes to use for each value displayed. Other options for this command are explained in the associated manual page.

The final command in this section is called file. The purpose of this command is to give you some information about another file to help you to classify its contents. The file command runs through a set of tests to try to identify a file's type and stops to print a message as soon as it thinks it has a positive identification. Due to the nature of some of the tests, it is possible for file to be fooled, but this is rare and should not present any major problems:

```
$ file *
book.dvi:      TeX DVI file data
book.log:      TeX transcript text
book.ps:       PostScript document
book.tex:      English text
fdr:           ascii text
inc:           directory
```

## 5.5 Dos Files

A portable set of tools exist, called mtools, which allow various operating systems, including Linux, to copy files and directories to and from standard DOS disks. This
