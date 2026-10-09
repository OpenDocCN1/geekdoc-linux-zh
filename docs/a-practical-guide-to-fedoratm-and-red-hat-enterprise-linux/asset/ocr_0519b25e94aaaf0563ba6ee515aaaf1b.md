tail reads from standard input. By default tail displays the last ten lines of its input. The following example shows tail displaying the last ten lines of the months file.

```
$ tail months
March
April
May
June
July
August
September
October
November
December
```

# OPTIONS

**Bytes** The -c [+]/n (—bytes=[+]/n) option counts by bytes (characters) instead of lines. The n argument is an integer that specifies the number of bytes. The following example displays the last 16 bytes, including 2 NEWLINES, of the months file.

```
$ tail -c 16 months
vember
December
```

If you put a plus sign (+) in front of n, tail counts from the start of the file instead of the end. The tail utility still displays characters through the end of the file, even though it starts counting from the beginning. This example shows that tail -c +16 causes tail to display from the 16th character through the end of the file.

```
$ tail -c +16 months
y
March
April
...
```

**Follow** The -f [-](—follow) option causes tail to enter an endless loop after copying the last line of the file, waiting for and copying additional lines from the file as the file grows. If you specify multiple files in the arguments with this option, tail includes a new header each time it displays output from a different file so you know which file is being added to. This option is useful for tracking the progress of a process that is running in the background and sending its output to a file. The tail utility continues to wait indefinitely, so you must use the interrupt key to terminate it.

**Lines** The -n [+]/n (—lines=[+]/n) option counts by lines (the default). The n argument is an integer that specifies the number of lines. Although it is not documented, you can use exit to specify a number of lines without using this option. The next example displays the last five lines of the months file.

```
$ tail -5 months
August
September
October
November
December
```