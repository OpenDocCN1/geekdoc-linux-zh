# unzip

# 1481

[-x file(s)]

An optional list of archive items to be excluded from processing.
Because wild-card characters match directory separators (/), you can use this option to exclude any files that are in subdirectories.
unzip foo *. [ch] -x * /

extracts C source files in the main directory, but none in any subdirectories. Without the -x option, extract all C source files in all directories within the.

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

+   -p extract files to pipes, no messages
-f overwrite existing files, create none
-u update files, create necessary
-x exclude files that follow in (list)

+   -l list files (short format)
-t compressed archive date
-z display archive comment
-d extract files into output

+   modifiers:
-n never overwrite existing files
-o overwrite files WITHOUT prompting
-j junk paths (do not make directories)
-c match filenames case-sensively
-r restore UID/GID info

+   -q quiet mode (-qq quieter)
-a auto-convert any text files
-s treat ALL files as text
-v be/verbose version info
-L make (some) lowercase
-v retain VMS version numbers
-m pipe through "more" page

Examples see unzip.doc for more
unzip data -x joe => extract all files except joe data.zip
unzip -p foo | => send contents of foo.zip pipe into program more