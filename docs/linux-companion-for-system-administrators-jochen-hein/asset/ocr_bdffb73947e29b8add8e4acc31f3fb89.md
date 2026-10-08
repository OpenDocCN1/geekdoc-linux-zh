# FILE MANAGEMENT 265

# 10.1.1 Searching for files with the find command

The find command can be used to search the file system for files that satisfy specific criteria. The output is a list of found files which can then be processed by other programs, such as awk (Section 10.5). Alternatively, a UNIX command can be specified which is executed on every file by the find command.

The find command can be passed the starting directory as the first parameter. All subdirectories of this directory are searched. The nesting depth can be restricted by means of the -maxdepth option; the whole search can be limited to a single file system with the option -xdev.

Various search criteria that the files must satisfy can be specified. Possible criteria are, for example, the file name (or a search pattern), the file type, or the last access, modification, or creation date. To search for a file name, the criterion would be input as -name file name.

Another parameter must tell the find command what to do if a matching file is found. Possible options are, simply to output the file name (option -print) or to start other UNIX programs with the found name as a parameter (option -exec). The GNU program find -print as the default action if nothing different was specified; other UNIX systems may or not do the same. If you want to remain portable, you should always specify -print. 10.1 searches for all files in the directory /etc whose names match the pattern *net.

```
(Linux):$ find /etc -name *net* -print
/etc/cd/rc.inet1
/etc/cd/rc.inet2
/etc/inet
/etc/inetd.conf
/etc/networks
```

+   Listing 10.1 Searching for files with find

For /etc specifies the directory to be searched. The parameter -name '*net*' tells find to search for files whose names match the search pattern *net*. The file name should be enclosed in single quotes so that the shell calls does not interpret the special characters. The -print parameter instructs find to output the complete file name.

When the -print option is specified, the output can be modified by means of a format specification, for example, to include modification date, file owner, or file size in the output. The -ls option is a very convenient way to get an output similar to the ls program. The man page for find contains a complete overview of possible formats. Several additional output formats can be set, for