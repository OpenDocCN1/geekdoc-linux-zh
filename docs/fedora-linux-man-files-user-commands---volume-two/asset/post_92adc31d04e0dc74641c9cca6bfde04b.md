
inverse, 39 for default foreground color, 30 to 37 for foreground colors, 90 to 97 for 16-color mode foreground colors, 38;5;0 to 38;5;255 for 88-color and 256-color modes foreground colors, 49 for default background color, 40 to 47 for background colors, 100 to 107 for 16-color mode background colors, and 48;5;0 to 48;5;255 for 88-color and 256-color modes background colors.

**LC_ALL, LC_COLLATE, LANG** These variables specify the locale for the **LC_COLLATE** category, which determines the collating sequence used to interpret range expressions like **[a-z]**. **LC_ALL, LC_CTYPE, LANG** These variables specify the locale for the **LC_CTYPE** category, which determines the type of characters, e.g., which characters are whitespace. **LC_ALL, LC_MESSAGES, LANG** These variables specify the locale for the **LC_MESSAGES** category, which determines the language that **grep** uses for messages. The default C locale uses American English messages.

**POSIXLY_CORRECT** If set, **grep** behaves as POSIX requires; otherwise, **grep** behaves more like other GNU programs. POSIX requires that options that follow file names must be treated as file names; by default, such options are permuted to the front of the operand list and are treated as options. Also, POSIX requires that unrecognized options be diagnosed as "illegal", but since they are not really against the law the default is to diagnose them as "invalid". **POSIXLY_CORRECT** also disables **_N_GNU_nonoption_argv_flags_**, described below. **_N_GNU_nonoption_argv_flags_** (Here N is **grep**'s numeric process ID.) If the $i$th character of this environment variable's value is 1, do not consider the $i$th operand of **grep** to be an option, even if it appears to be one. A shell can put this variable in the environment for each command it runs, specifying which operands are the results of file name wildcard expansion and therefore should not be treated as options. This behavior is available only with the GNU C library, and only when **POSIXLY_CORRECT** is not set.

## EXIT STATUS

Normally the exit status is 0 if a line is selected, 1 if no lines were selected, and 2 if an error occurred. However, if the -q or —quiet or —silent is used and a line is selected, the exit status is 0 even if an error occurred.

## COPYRIGHT

Copyright 1998-2000, 2002, 2005-2014 Free Software Foundation, Inc.

This is free software; see the source for copying conditions. There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

## BUGS

### Reporting Bugs

Email bug reports to the bug-reporting address <email: bug-grep@gnu.org>. An email archive <URL: http://lists.gnu.org/mailman/listinfo/bug-grep> and a bug tracker <URL: http://debbugs.gnu.org/cgi/pkgreport.cgi?package=grep> are available.

### Known Bugs

Large repetition counts in the ${n,m}$ construct may cause grep to use lots of memory. In addition, certain other obscure regular expressions require exponential time and space, and may cause grep to run out of memory.

Back-references are very slow, and may require exponential time.

## SEE ALSO

### Regular Manual Pages

- awk(1),
- cmp(1),
- diff(1),
- find(1),
- gzip(1),
- perl(1),
- sed(1),
- sort(1),
- xargs(1),
- zgrep(1),
- read(2),
- pcre(3),
- pcresyntax(3),
- pcrepattern(3),
- terminfo(5),
- glob(7),
- regex(7).

### POSIX Programmer's Manual Page

- grep(1p).

### Full Documentation

A complete manual <URL: http://www.gnu.org/software/grep/manual/> is available. If the **info** and **grep** programs are properly installed at your site, the command

```
info grep
```

should give you access to the complete manual.

## NOTES

This man page is maintained only fitfully; the full documentation is often more up-to-date.

## NAME

**file** - determine file type

## SYNOPSIS

words [ -bcEhiklILNnprsvz0 ] [ --apple ] [ --mime-encoding ] [ --mime-type ] [ -e testname ] [ -F separator ] [ -f namefile ] [ -m magicfiles ] [ -P name=value ] file ... -C [ -m magicfiles ] [ --help ]

## DESCRIPTION

This manual page documents version 5.22 of the command.

tests each argument in an attempt to classify it. There are three sets of tests, performed in this order: filesystem tests, magic tests, and language tests. The *first* test that succeeds causes the file type to be printed.

The type printed will usually contain one of the words *text* (the file contains only printing characters and a few common control characters and is probably safe to read on an **ASCII** terminal), *executable* (the file contains the result of compiling a program in a form understandable to some **UNIX** kernel or another), or *data* meaning anything else (data is usually “binary” or non-printable). Exceptions are well-known file formats (core files, tar archives) that are known to contain binary data. When modifying magic files or the program itself, make sure to *preserve these keywords* Users depend on knowing that all the readable files in a directory have the word “text” printed. Don’t do as Berkeley did and change “shell commands text” to “shell script”

The filesystem tests are based on examining the return from a stat(2) system call. The program checks to see if the file is empty, or if it’s some sort of special file. Any known file types appropriate to the system you are running on (sockets, symbolic links, or named pipes (FIFOs) on those systems that implement them) are intuitied if they are defined in the system header file In sys/stat.h .

The magic tests are used to check for files with data in particular fixed formats. The canonical example of this is a binary executable (compiled program) **a.out** file, whose format is defined in In elf.h, In a.out.h and possibly In exec.h in the standard include directory. These files have a “magic number” stored in a particular place near the beginning of the file that tells the **UNIX** operating system that the file is a binary executable, and which of several types thereof. The concept of a “magic” has been applied by extension to data files. Any file with some invariant identifier at a small fixed offset into the file can usually be described in this way. The information identifying these files is read from the compiled magic file /usr/share/misc/magic.mgc or the files in the directory /usr/share/misc/magic if the compiled file does not exist. In addition, if $HOME/.magic.mgc or $HOME/.magic exists, it will be used in preference to the system magic files.

If a file does not match any of the entries in the magic file, it is examined to see if it seems to be a text file. ASCII, ISO-8859-x, non-ISO 8-bit extended-ASCII character sets (such as those used on Macintosh and IBM PC systems), UTF-8-encoded Unicode, UTF-16-encoded Unicode, and EBCDIC character sets can be distinguished by the different ranges and sequences of bytes that constitute printable text in each set. If a file passes any of these tests, its character set is reported. ASCII, ISO-8859-x, UTF-8, and extended-ASCII files are identified as “text” because they will be mostly readable on nearly any terminal; UTF-16 and EBCDIC are only “character data” because, while they contain text, it is text that will require translation before it can be read. In addition, will attempt to determine other characteristics of text-type files. If the lines of a file are terminated by CR, CRLF, or NEL, instead of the Unix-standard LF, this will be reported. Files that contain embedded escape sequences or overstriking will also be identified.

Once has determined the character set used in a txt-type file, it will attempt to determine in what language the file is written. The language tests look for particuIar strings (cf. In names.h) that can appear anywhere in the first few blocks of a file. For example, the keyword .br indicates that the file is most likely a troff(1) input file, just as the keyword struct indicates a C program. These tests are less reliable than the previous two groups, so they are performed last. The language test routines also test for some miscelIany (such as tar(1) archives).

Any file that cannot be identified as having been written in any of the character sets listed above is simply said to be “data”
