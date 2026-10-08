# tail — Look at the Last Part of a File

# Synopsis

```
/usr/bin/tail [+number [lbcr]] [file]
/usr/bin/tail [-lbcr] [file]
/usr/bin/tail [+number [lbcf]] [file]
/usr/bin/tail [-lbcf] [file]
/usr/xpg4/bin/tail [-f -r] [-c number -n number] [file]
/usr/xpg4/bin/tail [+number [l|b|c|f]] [file]
/usr/xpg4/bin/tail [+number [f|r]] [file]
```

Use the tail command to look at the end of a file. By default, the last 10 lines are displayed. You can change the number of lines displayed by using the -n option to specify the number of lines to display. If you do not specify a file name, standard input is used.

Lines are displayed to standard output beginning at a point in the file indicated by the -c number, -n number, or number options (if you specify +number, the display begins at distance from the beginning; if you specify -number, the count is done from the end of the input; if number is null, the value 10 is assumed). number is counted in units of lines or bytes according to the -c or -n options. Alternatively, you can append l,b, or c to the number to specify the count in lines, blocks, or bytes. When you specify no units, counting is by lines.

> Note — Piped tails relative to the end of the file are stored in a buffer and thus are limited in length. Various kinds of anomalous behavior can happen with character files.

# Options

The following options are supported for /usr/bin/tail and /usr/xpg4/bin/tail. The -r and -f options are mutually exclusive. If you specify both, the -f option is ignored.

+   -b Display units of blocks.
-c Display units of bytes.

+   -f If the file is not a pipe, do not terminate after the line of the input file has been displayed; instead, enter an endless loop, sleep for a second, and then read and display further records from the input file. You can use this option to monitor the growth of a file that is written by some other process.

+   -1 Display units of lines.
-r Display lines from the specified starting point in the file in reverse order. The default is to display the entire file in reverse order.