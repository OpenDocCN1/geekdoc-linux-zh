
The -u (--unique) option outputs repeated lines only once. When you use this option with -c, sort displays a message if the same line appears more than once in the input file, even if the file is in sorted order. The following example sorts (and merges) two copies of days. Without any options, the first command displays two copies of each day in alphabetic order. The second command uses the -u option and displays one copy of each day.

```
$ sort days days | head -5
Friday
Friday
Monday
Monday
Saturday
```

```
$ sort -u days days | head -5
Friday
Monday
Saturday
Sunday
Thursday
```

The next example works with the fol file, which holds the names of three months, each listed twice. One of each pair begins with an uppercase letter, the other with a lowercase letter. With just the -u option, the first command displays all six lines. The second command adds the -f option, which causes sort to consider upper- and lowercase letters to be equivalent. Now, the -u option considers each pair of months to be equivalent and sort displays only one of each pair of months.

```
$ sort -u fol
April
April
February
February
January
January
```

```
$ sort -uf fol
April
February
January
```

## tail: DISPLAYS THE LAST PART OF A FILE

The tail utility displays the last part, or end, of a file. See page 235 for a description of the related head utility.

## ARGUMENTS

The arguments are the pathnames of the files that tail displays. When you specify more than one file, tail displays the filename of each file before displaying lines from that file. If you do not specify an argument or if you specify a hyphen (-) instead of a filename, tail reads from standard input. By default tail displays the last ten lines of its input. The following example shows tail displaying the last ten lines of the months file.

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

## OPTIONS

### Bytes
The -c [+]/n (—bytes=[+]/n) option counts by bytes (characters) instead of lines. The n argument is an integer that specifies the number of bytes. The following example displays the last 16 bytes, including 2 NEWLINES, of the months file.

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

### Follow
The -f [-](—follow) option causes tail to enter an endless loop after copying the last line of the file, waiting for and copying additional lines from the file as the file grows. If you specify multiple files in the arguments with this option, tail includes a new header each time it displays output from a different file so you know which file is being added to. This option is useful for tracking the progress of a process that is running in the background and sending its output to a file. The tail utility continues to wait indefinitely, so you must use the interrupt key to terminate it.

### Lines
The -n [+]/n (—lines=[+]/n) option counts by lines (the default). The n argument is an integer that specifies the number of lines. Although it is not documented, you can use exit to specify a number of lines without using this option. The next example displays the last five lines of the months file.

```
$ tail -5 months
August
September
October
November
December
```

If you put a plus sign (+) in front of *n*, **tail** counts from the start of the file instead of the end. The **tail** utility still *displays lines through the end of the file*, even though it *starts counting from the beginning*. Thus **tail -n +5** causes **tail** to display from the fifth line through the last line of the file.

## **LE2**
**touch: CHANGES FILE MODIFICATION AND ACCESS TIMES**

The **touch** utility changes the modification and access times of a file to the system time or a time you specify. You can also use **touch** to create a file.

## **ARGUMENTS**

The arguments are the pathnames of the files that **touch** creates or updates. Without options, **touch** changes the access and modification times to the system time. When you do not specify the `-c` (`--no-create`) option, **touch** creates files if they do not exist.

The following example shows that **f1** exists in the working directory with a modification date of July 24, 2014, and that **f2** does not exist. The **date** utility shows the system time. When **touch** is given these two filenames as arguments, it updates the modification time of **f1** and creates **f2**. Use the `ls -lu` options to display access times.

```
$ ls -l
-rwxr-xr-x. 1 max pubs 898028 2014-07-24 f1

$ date
Wed May 8 15:20:36 PDT 2013

$ touch f1 f2

$ ls -l
-rwxr-xr-x. 1 max pubs 898028 05-08 15:20 f1
-rw-r--r--. 1 max pubs 0 05-08 15:20 f2
```

## **OPTIONS**

- **No create**: The `-c` (`--no-create`) option does not create files; it only modifies times on existing files.
- **Date**: The `-d *datestring*` (`--date=*datestring*`) option changes times using the date specified by *datestring*. Most familiar formats are permitted for *datestring*. Components of the date and time not included in *datestring* are assumed to be the current date and time. This option may not be used with **-t**. This example changes the date on **f1** to May 15, 2020.

```
$ touch -d 'may 15 2020' f1
$ ls -l f1
-rw-rw-r--. 1 max max 978160 2020-05-15 f1
```

- **Time**: The `-t [*cc*[`yy`]][`mm`][`dd`][`hh`]`mm`[.]*ss*]` option changes times to the date specified by the argument. The `mm` argument is the number of the month (01–12), `dd` is the day of the month (01–31), `hh` is the hour based on a 24-hour clock (00–23), and `mm` is the minutes (00–59). You must specify at least these fields. You can specify the number of seconds past the start of the minute using `.ss`.

The optional `cc` specifies the first two digits of the year (the value of the century minus 1), and `yy` specifies the last two digits of the year. When you do not specify a year, **touch** assumes the current year. When you do not specify `cc`, touch assumes 20 for yy in the range 0–68 and 19 for yy in the range 69–99. This option may not be used with –d.

The following example creates a file with a modification and access time of August (08) 2 (02) at 2:30 PM (1420). The command assumes the year known to the system and zero seconds.

```
$ touch -t 08021420 xx
$ ls -l xx
-rw-r--r-- 1 sam pubs 0 08-02 14:20 xx
```

## **WC: DISPLAYS THE NUMBER OF LINES, WORDS, AND BYTES IN FILES**

The **wc** (word count) utility displays the number of lines, words, and bytes in one or more files. When you specify more than one filename on the command line, **wc** displays totals for each file as well as combined totals for all files.

### ARGUMENTS

The arguments are the pathnames of one or more files that **wc** analyzes. The columns **wc** displays show the number of lines, words, and bytes, in that order. (A *word* is a sequence of characters bounded by SPACES, TABS, NEWLINES, or a combination of these characters.) Without any arguments, **wc** takes its input from standard input. The following commands show **wc** analyzing the days and months files. When you redirect its input, **wc** does not display the name of the file.

```
$ wc days months
 7   7   57 days
 12  12   86 months
 19  19  143 total
```

```
$ cat days months | wc
19  19  143
```

### OPTIONS

- **Lines** The `–1` (lowercase “el”; `—lines`) option displays only the number of lines (i.e., NEWLINE characters) in the input. The following example shows that there are seven lines in the days file.

```
$ wc -l days
7 days
```

- **Bytes** The `–m` (`—chars`) option displays only the number of bytes in the input. The next example shows that there are 57 bytes, including NEWLINES, in the days file.

```
$ wc -m days
57 days
```

- **Words** The `–w` (`—words`) option displays only the number of words in the input. The final example shows that there are seven words (each line holds one word) in the days file.

```
$ wc -w days
7 days
```
