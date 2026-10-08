
# unzip

# 1481

[-x file(s)]

An optional list of archive items to be excluded from processing. Because wild-card characters match directory separators (/), you can use this option to exclude any files that are in subdirectories.
unzip foo *. [ch] -x * /

extracts C source files in the main directory, but none in any subdirectories. Without the -x option, extract all C source files in all directories within the de.

[-d exdir] An optional directory to extract files. By default, all files and subdirectories are recreated in the current directory; the -d option enables you to extract into an arbitrary directory (assuming you have permission to write to the directory). This option need not appear at the end of the command line; it is also accepted before the file specification (with the normal options), immediately after the file specification, or between the file(s) and the -x option. You can concatenate the option and directory without any white space between them, but note that this may suppress normal shell behavior. In particular, -d ~ (tilde) is expanded by UNIX shell into the user's home directory, but -d~ is treated as a literal subdirectory ~ of the current directory.

# Options

> Note — To support obsolete hardware, the unzip usage screen is limited to 22 or 23 lines. Consider the usage as a reminder of only the basic unzip syntax instead of an exhaustive list of all possible options.

The following example shows the unzip usage screen.

```
castle$ unzip
Unzip 5.32 of 3 November 1997, by InfoZIP. Maintained by Greg Roelfs. Send
reports to the authors at Zip-Bugs@lists.wku.edu; Send README for details.
unzip: unzip [-z] [-opts[modifiers]] file[.zip] [list] [-x xlist] [-d exdir]
Default action is to extract files, except those in xlist, to exdir;
file[.zip] may be a wildcard. -z ZipInfo pipe ("unzip -Z" for usage).
```

- -p extract files to pipes, no messages
- -f overwrite existing files, create none
- -u update files, create necessary
- -x exclude files that follow in (list)

- -l list files (short format)
- -t compressed archive date
- -z display archive comment
- -d extract files into output

- modifiers:
- -n never overwrite existing files
- -o overwrite files WITHOUT prompting
- -j junk paths (do not make directories)
- -c match filenames case-sensively
- -r restore UID/GID info

- -q quiet mode (-qq quieter)
- -a auto-convert any text files
- -s treat ALL files as text
- -v be/verbose version info
- -L make (some) lowercase
- -v retain VMS version numbers
- -m pipe through "more" page

Examples see unzip.doc for more
unzip data -x joe => extract all files except joe data.zip
unzip -p foo | => send contents of foo.zip pipe into program more

# 1482

# unzip

unzip -fo foo README => quietly replace existing README if archive file castlet

The exhaustive list of options is shown below.

- -A Print extended help for the DLL programming interface (API) (OS/2, UNIX DLL).

- -c Extract files to standard output. This option is similar to the -p option, except print the name of each file as it is extracted. Allow the -a option, automatically perform ASCII-EBCDIC conversion if appropriate. This option is not listed in the unzip screen.

- -f Freshen existing files; that, is extract only those files that already exist on disk and are newer than the disk queries. By default overwriting, you can use the -o option to suppress the queries. Note that under many operating systems, the TZ (time zone) environment variable must be set correctly for -f and -u to work properly (under UNIX the variable is usually set automatically). TZ must be set to resolve the differences between DOS-format file times (always local time) and UNIX-format times (always in GMT). A typical TZ value is PST (U.S. Pacific time with automatic adjustment for standard or daylight saving).

- -l List files (short format). Print the names, sizes and dates of the specified files, and for all files specified. If unzip was compiled with OS2_EAS then, the -l option also lists columns for the sizes of OS/2 extended attributes (EAS) and OS2 access control lists (ACLs). In addition, display the zip file comment and individual file comments (if any). If a file was archived from a single-case file system (for example, the MS-DOS FAT file system) and you specify the -L option, convert the file to lower case, and prefix it with a caret (^).

- -p Extract files to pipe (standard output). Send nothing but file data to standard output, and always extract the files in binary format just they are stored (no conversions).

- -t Test archive. Extract each specified file in memory, and compare the cyclic redundancy (CRC, an enhanced checksum) of the expanded file with that of the original file's stored CRC value.

- -u Update existing files, and create new ones if needed. This option performs the same function as the -f option, extracting (with query) files that are newer than those with the same name on disk. In addition, extract those files that do not already exist on disk. See -f for information on setting the time properly.

- -v Verbose, or print version information. This option behaves as an option and a modifier.

# 1483

# unzip

As an option, -v has two purposes: when archived from single-case file system (for example, the MS-DOS FAT file system) and you specify the -L option, convert the file to lower case, and prefix it with a caret (^). Depending on the archiver, store files archived under single-case file systems (like V) as uppercase names. The default behavior can be ugly or inconvenient when extracting to a case-preserving file system as OS2 HPFS or a case-sensitive one as UNIX. By default, unzip lists and extracts file names exactly as they are (except truncation, conversion of unsupported characters, and so on). On some systems, the number of available lines on the screen is not detected, in which case unzip assumes the height is 24 lines.

- -z Display only comment
- -a Autoconvert files
- -b Treat all files as binary
- -B Save a backup of each overwritten file
- -M Pipe all output through an internal pager
- -n Never overwrite existing files
- -j Junk paths
- -L Convert to lower case
- -N Extract file comments as Amiga file notes.

# 1484

# unzip

- -C Match filenames case insensitively. Because some file systems are case sensitive, the default behavior is to match wild-card and literal. In the example above, you can use the -C option to force all names to match case.
