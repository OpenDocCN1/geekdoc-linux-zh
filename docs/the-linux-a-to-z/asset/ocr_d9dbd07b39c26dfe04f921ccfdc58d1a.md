# 5.1.3 sort

The sort command is a filter which can sort the lines of text in its input into the order you specify on the command line and then send the sorted lines to the standard output device. The sort command is very versatile in that it can treat the input lines as a collection of several fields and perform sorting operations using one or more of these fields as the sort key. You can also choose the character that sort will use as its field delimiter so that you may sort files of different types.

In the examples that follow we shall make use of the following small (and fictitious) password file, called pw.test:

```
root:awmku76tr43d6:0:0::/root/:/bin/sh
pc:bdhd74hs9jh3h:500:50::/usr1/pc:/bin/bash
carey:esJ9ohd8HH89i:501:50::/usr1/carey:/bin/bash
mot:dhjd83kj dJS6D:1500:60::/usr1/mot:/bin/bash
grex:cj8AjoWE8h8fs:1500:60::/usr1/mot:/bin/sh
```

By default, sort uses whitespace characters (spaces, tabs, etc.) as its field separators. Therefore, the lines of pw.test, containing no whitespace characters, are each treated as a single field. If sort is run on this file, it will treat each line as though it is a single word and sort them into alphabetical order:

```
$ sort pw.test
carey:esJ9ohd8HH89i:501:50::/usr1/carey:/bin/bash
grex:cj8AjoWE8h8fs:1500:60::/usr1/mot:/bin/sh
mot:dhjd83kj dJS6D:1500:60::/usr1/mot:/bin/bash
pc:bdhd74hs9jh3h:500:50::/usr1/pc:/bin/bash
root:awmku76tr43d6:0:0::/root/:/bin/sh
```

The sort command will take its input from any files specified on the command line, or from the standard input device if there are none given.

Many command line switches are available with sort; the most useful are given in the following table:

| Switch | Description |
|---|---|
| -b | ignore leading space characters in sort keys; |
| -f | treat upper and lower case letters as the same; |
| -n | treat the sort key as numeric rather that text; |
| -r | sort from high to low rather than from low to high; |
| -o file | send output to file instead of standard output; |
| -t s | use s as field separator, instead of whitespace; |
| -k s1,s2 | use fields s1 to (s2-1) as the sort key. |

Actually, the specification of the sort key is a little more complex than is obvious from the previous table. To start with, it is permitted to give repeated -k switches, so that any combination of fields can be specified. The sort command uses the fields in the order given on the command line, which need not be the same as the