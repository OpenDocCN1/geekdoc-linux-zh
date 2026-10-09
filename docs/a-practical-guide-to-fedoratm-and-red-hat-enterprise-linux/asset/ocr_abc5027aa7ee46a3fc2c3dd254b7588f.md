**Combining options** When you need to use several options, you can usually group multiple single-letter options into one argument that starts with a single hyphen; do not put SPACES between the options. You cannot combine options that are preceded by two hyphens in this way. Specific rules for combining options depend on the program you are running. The next example shows both the -t and -x options with the ls utility. Together these options generate a list of filenames in horizontally sorted rows in reverse alphabetical order.

```
$ ls -rx
zach    test    temp    personal    oldstuff    office
names   max     mark    house       hold
```

Most utilities allow you to list options in any order; thus ls -xr produces the same results as ls -rx. The command ls -x -r also generates the same list.

# The -—help option

**tip** Many utilities display a (sometimes extensive) help message when you call them with an argument of --help. All utilities developed by the GNU Project (page 3) accept this option. Following is the help message displayed by the bzip2 compression utility (page 245).

```
$ bzip2 -—help
bzip2, a block-sorting file compressor.  Version 1.0.6, 6-Sep-2010.

usage: bunzip2 [flags and input files in any order]

-h  -—help      print this message
-Z  -—decompression      force decompression
-z  -—compress  force compression
-k  -—keep    keep (don't delete) input files
-f  -—force   overwrite existing output files
...
If invoked as 'bzip2', default action is to compress.
as 'bunzip2', default action is to decompress.
as 'bzcat', default action is to decompress to stdout.
...
```

**Option arguments** Some utilities have options that require arguments. These arguments are not optional. For example, the gcc utility (C compiler) has a -o (output) option that must be followed by the name you want to give the executable file that gcc generates. Typically an argument to an option is separated from its option letter by a SPACE:

```
$ gcc -o prog prog.c
```

Some utilities sometimes require an equal sign between an option and its argument. For example, you can specify the width of output from diff in two ways:

```
$ diff -W 60 filea fileb
*or*
$ diff -W width=60 filea fileb
```

**Arguments that start with a hyphen** Another convention allows utilities to work with arguments, such as filenames, that start with a hyphen. If a file named -ls is in the working directory, the following command is ambiguous: