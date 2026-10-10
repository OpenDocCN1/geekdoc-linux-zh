# ## DESCRIPTION

The **gdbmtool** utility allows you to view and modify an existing GDBM database or to create a new one.

The *DBFILE* argument supplies the name of the database to open. If not supplied, the default name **junk.gdbm** is used instead. If the named database does not exist, it will be created. An existing database can be cleared (i.e. all records removed from it) using the `--newdb` option (see below).

Unless the **-N** (`--norc`) option is given, after startup **gdbmtool** looks for file named ***.gdbmtoolrc*** first in the current working directory, and, if not found there, in the home directory of the user who started the program. If found, this file is read and interpreted as a list of **gdbmtool** commands.

Then **gdbmtool** starts a loop, in which it reads commands from the standard input, executes them and prints the results on the standard output. If the standard input is attached to a console, the program runs in interactive mode.

The program terminates when the **quit** command is given, or end-of-file is detected on its standard input.

A **gdbmtool** command consists of a command verb, optionally followed by one or more arguments, separated by any amount of white space. A command verb can be entered either in full or in an abbreviated form, as long as that abbreviation does not match any other verb.

Any sequence of non-whitespace characters appearing after the command verb forms an argument. If the argument contains whitespace or unprintable characters it must be enclosed in double quotes. Within double quotes the usual escape sequences are understood, as shown in the table below:

Escape Expansion
| _ | \a Audible bell character (ASCII 7)
| _ | \b Backspace character (ASCII 8)
| _ | \f Form-feed character (ASCII 12)
| _ | \n Newline character (ASCII 10)
| _ | \r Carriage return character (ASCII 13)
| _ | \t Horizontal tabulation character (ASCII 9)
| _ | \v Vertical tabulation character (ASCII 11)
| _ | \\ Single slash

In addition, a backslash immediately followed by the end-of-line character effectively removes that character, allowing to split long arguments over several input lines.