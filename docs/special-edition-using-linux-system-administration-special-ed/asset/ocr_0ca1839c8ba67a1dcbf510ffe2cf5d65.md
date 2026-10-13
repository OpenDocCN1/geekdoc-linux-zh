# # RM

# ## NAME

rm—Remove files or directories.

# ## SYNOPSIS

```
rm [OPTION]... FILE...
```

# ## DESCRIPTION

This manual page documents the GNU version of rm. rm removes each specified file. By default, it does not remove directories. If a file is unwritable, the standard input is a tty, and the -f or --force option is not given, rm prompts the user for whether to remove the file. If the response does not begin with ‘y’ or ‘Y’, the file is skipped.

GNU rm, like every program that uses the getopt function to parse its arguments, enables you to use the -- option to indicate that all following arguments are non-options. To remove a file called -f in the current directory, you could type either

```
rm -- -f
```

or

```
rm ./-f
```

The UNIX rm program’s use of a single - for this purpose predates the development of the getopt standard syntax.

# ## OPTIONS

Remove (unlink) the FILE(s).

+   - `-d, --directory`—Unlink directory, even if non-empty (super-user only)
+   - `-f, --force`—Ignore nonexistent files, never prompt
+   - `-i, --interactive`—Prompt before any removal
+   - `-r, -R, --recursive`—Remove the contents of directories recursively
+   - `-v, --verbose`—Explain what is being done
+   - `--help`—Display this help and exit
+   - `--version`—Output version information and exit

# ## REPORTING BUGS

Report bugs to <bug-fileutils@gnu.org>.