# Advanced Bash-Scripting Guide

```
# short script by Omair Ashkenazi.
# Used in ABS Guide with permission (thanks!).

mkfifopipe1 # Yes, pipes can be given names.
mkfifopipe2 # Hence the designation "named pipe."

(cut -d' -f1 tr "a-z" "A-Z") >pipe2 & 
ls -1 | tr -s | cut -d' -f3,9- | tee pipe |
cut -d' -f2 | paste - pipe2

rm -f pipe1
rm -f pipe2

# No need to kill background processes when script terminates (why not)?

exit $$

Invoke, the script and explain the output:
sh mkfifo-example.sh

4830.tar.gz BOZO
pipe1 BOZO
pipe2 BOZO
mkfifo-example.sh BOZO
Mixed.msg BOZO
```

pathchk checks the validity of a file. If the filename exceeds the maximum allowed (255 characters) one or more of the directories in its path is not searchable, then an error message results.

Unfortunately, pathchk does not return a recognizable error code, and therefore is pretty much useless in script. Consider instead the file test operators.

Though this might seem obscure and feared data duplicator command originated for exchanging data on magnetic tapes within UNIX minicomputers and IBM mainframes, it still has its uses. The dd command simply copies a file (or stdin/stdout), but with conversions. Possible conversions include ASCII/EBCDIC [86] uppercase, swapping of byte pairs between input and output, and skipping/or truncating the head or tail of the file.

> Converting a file to all uppercase:

```
dd if=$file conv=ucase > $filename.uppercase
case # For lower case conversion
```

Some basic options to dd are:

+   if=INFILE
INFILE is the source file.
of=OUTFILE
OUTFILE is the target file, the file that will have the data written to it.
bs=BLOCKSIZE

This is the size of each block of data being read and written, usually a power of 2.
skip=BLOCKS

Chapter 16. External Filters, Programs and Commands