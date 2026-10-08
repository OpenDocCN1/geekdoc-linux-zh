# 1370

/usr/xpg4/bin/tail
The following options are supported for /usr/xpg4/bin/tail only.

+   -c number Specify number as a decimal integer whose sign affects the location in
t file, measured in bytes, to begin the display.

+   + Start the display relative to the beginning of the file.
+ Start the display relative to the end of the file.

+   none The origin for counting is 1; that is, -c +1 represents the
first byte of the file, -c -1 the last.

+   -n number Equivalent to -c number, except measure starting location in the
file in lines instead of bytes. The origin for counting is 1; that is, -n +1
represents the first byte of the file, -n -1 the last.

# Operands

+   file

A path name of an input file. If you specify no file, use the
standard input.

# Usage

See largefile(5) for the description of the behavior of tail when encountering files
greater than or equal to 2 Gbytes (\*\*31 bytes).

# Examples

The following command displays the last 10 lines of the file /var/adm/sug followed by
ay lines that are appended to the file between the time you initiate tail and the time you
yill it.

```
# tail -f /var/adm/sug
SU 04/04 15:13 + pts/6 winsorroot
SU 04/04 17:25 + pts/6 winsorroot
SU 04/05 12:46 + pts/6 winsorroot
SU 04/05 12:48 + pts/6 winsorroot
SU 04/05 17:41 + pts/6 winsorroot
SU 04/06 09:46 + pts/3 winsorroot
SU 04/06 18:22 + pts/6 winsorroot
SU 04/07 08:56 + pts/6 winsorroot
SU 04/07 13:41 + pts/3 winsorroot
SU 04/07 16:17 + pts/6 winsorroot
SU 04/07 16:17 + pts/3 winsorroot
SU 04/07 16:17 + pts/3 winsorroot
SU 04/07 16:18 + pts/3 winsorroot
^C
```

The following example displays the last 15 lines of the file /var/adm/sug followed by
ay lines that are appended to the file between the time you initiate tail and the time you
yill it.

```
# tail -15cf /var/adm/sug
/3 winsorroot
SU 04/07 16:22 + pts/5 winsorroot
```