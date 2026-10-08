the -b and -q options, and the interpretation of single- and/or multibyte characters within file names.

LC_TIME determines the date and time strings output by the -g, -l (ell), -n, and -o options.

LC_MESSAGES determines the language in which messages (other than the date and time strings) are displayed.

If any internationalization variable contains an invalid setting, ls behaves as if all internationalization variables are set to "C" (see environ(5)).

# International Code Set Support

Single- and multibyte character code sets are supported.

# RETURN VALUE

ls exits with one of the following values:

+   0 All input files were listed successfully.  
>0 ls was aborted because errors occurred when accessing files.  
The following conditions cause an error:

+   - Specified file not found.
- User has no permission to read the directory.
- Process could not get enough memory.
- Invalid option specified.

# EXAMPLES

Print a long listing of all the files in the current working directory (including the file sizes). List the most recently modified (youngest) file first, followed by the next older file, and so forth, to the oldest. Files whose names begin with a . are also printed.

```
ls -alst
```

# WARNINGS

Setting options based on whether the output is a login (tty) device is undesirable because ls -s is very different from ls -s | lp. On the other hand, not using this setting makes old shell scripts that used ls almost inevitably fail.

Unprintable characters in file names may confuse the columnar output options.

# DEPENDENCIES

NFS The -l (ell) option does not display a plus sign (+) after the access permission bits of networked files to represent existence of optional access control list entries.

# AUTHOR

ls was developed by AT&T, the University of California, Berkeley and HP.

# FILES

/etc/passwd to get user IDs for ls -l (ell) and ls -o.
/etc/group to get group IDs for ls -l (ell) and ls -g.
/usr/share/lib/termiInfo/?/* to get terminal information.

# SEE ALSO