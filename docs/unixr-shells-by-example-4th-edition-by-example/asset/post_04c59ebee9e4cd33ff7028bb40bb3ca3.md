
## EXPLANATION (CONTINUED)

8 Prints all files on the root partition that belong to user ellie.

9 Moves files that are older than 31 days into a directory, /old, and prints the files as it moves them.

## finger—displays information about local and remote users

```
finger [ -bfhiImpqsw ] [ username... ]
finger [-l] username@hostname...
```

By default, the finger command displays information about each logged-in user, including login name, full name, terminal name (prepended with an * if write permission is denied), idle time, login time, and location if known.

## fmt—simple text formatters

```
fmt [ -c ] [ -s ] [ -w width | -width ] [ inputfile... ]
```

fmt is a simple text formatter that fills and joins lines to produce output lines of (up to) the number of characters specified in the -w width option. The default width is 72. fmt concatenates the input files listed as arguments. If none are given, fmt formats text from the standard input.

## EXAMPLE A.28

```
fmt -c -w45 letter
```

## EXPLANATION

Formats letter. The -c switch preserves the indentation of the first two lines within the paragraph and aligns the left margin of each subsequent line with that of the second line. The -w switch fills the output line of up to 45 columns.

## fold—folds long lines

```
fold [ -w width | -width ] [ filename ... ]
```

Folds the contents of the specified filenames, or the standard input if no files are specified, breaking the lines to have maximum width. The default for width is 80. Width should be a multiple of 8 if tabs are present, or the tabs should be expanded.

## ftp—file transfer program

```
ftp [ -dgin tv ] [ hostname ]
```

The ftp command is the user interface to the Internet standard File Transfer Protocol (FTP). ftp transfers files to and from a remote network site. The file transfer program is not limited to UNIX machines.

## EXAMPLE A.29

```
1 ftp ftp.uu.net
2 ftp -n 127.150.28.56
```

## EXPLANATION

- 1 ftp to the machine ftp.uu.net, a large repository run by the UU NET service that handles e-mail and net news for UNIX systems.
- 2 Opens a connection to the machine at 127.45.4.1 and does not attempt to auto-login.

## free—displays amount of free and used memory in the system

```
free [-b | -k | -m] [-o] [-s delay ] [-t] [-v]
```

free displays the total amount of free and used physical and swap memory in the system, as well as the shared memory and buffers used by the kernel.

## EXAMPLE A.30

```
% free
Mem: total used free shared buffers cached
64148 54528 9620 45632 3460 29056
-/- buffers/cache: 22012 42136
Swap: 96352 0 96352
```

## fuser—identifies processes using files or sockets

```
fuser [-a|-s] [-n space] [-signal] [-kmuv] name ...[-] [-n space] [-signal] [-kmuv] name ...
fuser -l
fuser -V
```

The fuser command displays the PIDs of processes using the specified file or filesystems. In the default display mode, each filename is followed by a letter denoting the type of access.

## EXAMPLE A.31

```
% fuser --help
usage: fuser [-a | -q ] [-n space ] [ -signal ] [ -kmuv ] filename ... [ -n space ] [ -signal ] [ -kmuv ] name ...
...
fuser -l
fuser -V
-a display unused files too
-k kill processes accessing that file
```

## EXAMPLE A.31 (CONTINUED)

- -l list signal names
- -m mounted FS
- -n space search in the specified name space (file, udp, or tcp)
- -s silent operation
- -signal send signal instead of SIGKILL
- -u display user ids
- -v verbose output
- -V display version information
- - reset options

udp/tcp names: [local_port][,[rmt_host][,[rmt_port]]]

## gawk—pattern scanning and processing language

```
gawk [ POSIX or GNU style options ] -f program-file [--] file ...
gawk [ POSIX or GNU style options ] [ -- ]program-text file ...
```

gawk is the GNU Project's implementation of the awk programming language. It conforms to the definition of the language in the POSIX 1003.2 Command Language And Utilities Standard. This version is in turn based on the description in The AWK Programming Language, by Aho, Kernighan, and Weinberger, with the additional features found in the System V Release 4 version of UNIX awk. gawk also provides more recent Bell Labs awk extensions, and some GNU-specific extensions.

## gcc, g++—GNU project C and C++ Compiler (v2.7)

```
gcc [ option | filename ]...
g++ [ option | filename ]...
```

## getopt(s)—parses command-line options

The getopts command supersedes getopt. getopts is used to break up options in command lines for easy parsing by shell procedures and to check for legal options.

## grep—searches a file for a pattern

```
grep [ -bchilnsvw ] limited-regular-expression [ filename ... ]
```

grep searches files for a pattern and prints all lines that contain that pattern. Uses regular expression metacharacters to match the patterns. egrep has an extended set of metacharacters.

## EXAMPLE A.32

```
1  grep Tom file1 file2 file3
2  grep -in 'Atom savage' *
```
