
“Quiet”. Do not print the introductory and copyright messages. These messages are also suppressed in batch mode.

### -batch
Run in batch mode. Exit with status 0 after processing all the command files specified with -x (and .gdbinit, if not inhibited). Exit with nonzero status if an error occurs in executing the GDB commands in the command files.

Batch mode may be useful for running GDB as a filter, for example to download and run a program on another computer; in order to make this more useful, the message `Program exited normally.`

(which is ordinarily issued whenever a program running under GDB control terminates) is not issued when running in batch mode.

### -cd=directory
Run GDB using *directory* as its working directory, instead of the current directory.

### -fullname
### -f
Emacs sets this option when it runs GDB as a subprocess. It tells GDB to output the full file name and line number in a standard, recognizable fashion each time a stack frame is displayed (which includes each time the program stops). This recognizable format looks like two \032 characters, followed by the file name, line number and character position separated by colons, and a newline. The Emacs-to-GDB interface program uses the two \032 characters as a signal to display the source code for the frame.

### -b bps
Set the line speed (baud rate or bits per second) of any serial interface used by GDB for remote debugging.

### -tty=device
Run using *device* for your program’s standard input and output.

## SEE ALSO

The full documentation for GDB is maintained as a Texinfo manual. If the `info` and `gdb` programs and GDB’s Texinfo documentation are properly installed at your site, the command

```
info gdb
```

should give you access to the complete manual.

*Using GDB: A Guide to the GNU Source-Level Debugger*, Richard M. Stallman and Roland H. Pesch, July 1991.

## COPYRIGHT

Copyright © 1988-2015 Free Software Foundation, Inc.

Permission is granted to copy, distribute and/or modify this document under the terms of the GNU Free Documentation License, Version 1.3 or any later version published by the Free Software Foundation; with the Invariant Sections being “Free Software” and “Free Software Needs Free Documentation”, with the Front-Cover Texts being “A GNU Manual,” and with the Back-Cover Texts as in (a) below.

(a) The FSF's Back-Cover Text is: “You are free to copy and modify this GNU Manual. Buying copies from GNU Press supports the FSF in developing GNU and promoting software freedom.”

## GDBM_DUMP

## NAME

gdbm_dump - dump a GDBM database to a file

## SYNOPSIS

**gdbm_dump** [-H *FMT*] [--format=*FMT*] *DB_FILE* [*FILE*]

**gdbm_dump** [-Vh] [--help] [--usage] [--version]

## DESCRIPTION

The **gdbm_dump** utility creates a dump of the specified (3) database file. The name for the output dump file is supplied by the second argument (*FILE*). If not specified, the output goes to the standard error.

The created dump can be given as argument to the (1) utility in order to re-create an exact copy of the *DB_FILE*.

## OPTIONS

- -H, --format=FMT

Select dump format. The value **binary** (or **0**) instructs `gdbm_dump` to produce a binary dump, compatible with earlier **gdbm** versions (up to version 1.9). The value **ascii** (or **1**) instructs it to create an ASCII dump (this is the default). The latter is preferred because, apart from the actual data, it also contains meta-information which will allow (1) to recreate an exact copy of the file.

- -h, --help

Print a short usage summary.

- --usage

Print a list of available options.

- -V, --version

Print program version

## SEE ALSO

(1), (1), (3).

For a detailed description of **gdbm_dump** and other **gdbm** utilities, refer to the **GDBM Manual** available in Texinfo format. To access it, run:

```
info gdbm
```

## REPORTING BUGS

Report bugs to <>.

## COPYRIGHT

Copyright © 2013 Free Software Foundation, Inc. License GPLv3+: GNU GPL version 3 or later <> This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## GDBM_LOAD

## NAME

gdbm_load - re-create a GDBM database from a dump file.

## SYNOPSIS

```
gdbm_load [-Mmn] [-b NUM] [-c NUM] [-m MODE] [-u NAME|UID[:NAME|GID]]
    [--block-size=NUM] [--cache-size=NUM] [--mmap=NUM]    [--
mode=MODE] [--no-meta] [--replace]      [--
user=NAME|UID[:NAME|GID]] FILE [DB_FILE]
gdbm_load [-Vh] [--help] [--usage] [--version]
```

## DESCRIPTION

Create a **gdbm** database file *DB_FILE* from the dump file *FILE*. If the *FILE* argument is not supplied, output the created database to the standard error.

If the input file is in ASCII dump format, the mode and ownership of the created database are restored from the information in the dump. This can be overridden using the command line options (see below).

## OPTIONS

- -b, --block-size=NUM
  Sets block size.
- -c, --cache-size=NUM
  Sets cache size.
- -M, --mmap
  Use memory mapping.
- -m, --mode=MODE
  Set database file mode (octal number).
- -n, --no-meta
  Do not attempt to restore database meta-data (mode and ownership).
- -r, --replace
  If the database exists, replace records in it.
- -u, --user=NAME|UID[:NAME|GID]
  Set file ownership.
- -h, --help
  Print a short usage summary.
- --usage
  Print a list of available options.
- -V, --version
  Print program version

## SEE ALSO

(1), (1), (3).

For a detailed description of **gdbm_load** and other **gdbm** utilities, refer to the **GDBM Manual** available in Texinfo format. To access it, run:

```
info gdbm
```

## REPORTING BUGS

Report bugs to <>.

## COPYRIGHT

Copyright © 2013 Free Software Foundation, Inc. License GPLv3+: GNU GPL version 3 or later <> This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## Gdbmtool

## NAME

gdbmtool - examine and modify a GDBM database

## SYNOPSIS

gdbmtool [-lmNnqrs] [-b SIZE] [-c SIZE] [-f FILE] [--block-size=SIZE] [--cache-size=SIZE] [--file FILE] [--newdb] [--no-lock] [--no-mmap] [--norc] [--quiet] [--read-only] [--synchronize] [DBFILE]

gdbmtool [-Vh] [--help] [--usage] [--version]

## DESCRIPTION

The **gdbmtool** utility allows you to view and modify an existing GDBM database or to create a new one.

The *DBFILE* argument supplies the name of the database to open. If not supplied, the default name **junk.gdbm** is used instead. If the named database does not exist, it will be created. An existing database can be cleared (i.e. all records removed from it) using the `--newdb` option (see below).

Unless the **-N** (`--norc`) option is given, after startup **gdbmtool** looks for file named ***.gdbmtoolrc*** first in the current working directory, and, if not found there, in the home directory of the user who started the program. If found, this file is read and interpreted as a list of **gdbmtool** commands.

Then **gdbmtool** starts a loop, in which it reads commands from the standard input, executes them and prints the results on the standard output. If the standard input is attached to a console, the program runs in interactive mode.

The program terminates when the **quit** command is given, or end-of-file is detected on its standard input.

A **gdbmtool** command consists of a command verb, optionally followed by one or more arguments, separated by any amount of white space. A command verb can be entered either in full or in an abbreviated form, as long as that abbreviation does not match any other verb.

Any sequence of non-whitespace characters appearing after the command verb forms an argument. If the argument contains whitespace or unprintable characters it must be enclosed in double quotes. Within double quotes the usual escape sequences are understood, as shown in the table below:

| Escape | Expansion |
| :--- | :--- |
| \a | Audible bell character (ASCII 7) |
| \b | Backspace character (ASCII 8) |
| \f | Form-feed character (ASCII 12) |
| \n | Newline character (ASCII 10) |
| \r | Carriage return character (ASCII 13) |
| \t | Horizontal tabulation character (ASCII 9) |
| \v | Vertical tabulation character (ASCII 11) |
| \\ | Single slash |

In addition, a backslash immediately followed by the end-of-line character effectively removes that character, allowing to split long arguments over several input lines.
