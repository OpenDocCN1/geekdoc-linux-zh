LC_MESSAGES Determines the locale that should be used to affect the format and contents of diagnostic messages written to standard error and informative messages written to standard output.

NLSPATH Determines the location of message catalogues for the processing of LC_MESSAGES.

LINES Overrides the system-selected vertical screen size, used as the number of lines in a screenful. The -n option takes precedence over the LINES variable for determining the number of lines in a screenful.

MORE Determines a string containing options, preceded with hyphens and blank-character-separated as on the command line. Any command-line options are processed after those in the MORE variable. The MORE variable takes precedence over the TERM and LINES variables for determining the number of lines in a screenful.

TERM Determines the name of the terminal type.

# International Code Set Support

Single- and multi-byte character code sets are supported.

# EXAMPLES

To view a simple file, use:

```
more filename
```

To preview nroff output, use a command resembling:

```
nroff -mm +2 doc.n | more -s
```

If the file contains tables, use:

```
tbl file | nroff -mm | col | more -s
```

To display file stuff in a fifteen line-window and convert multiple adjacent blank lines into a single blank line:

```
more -s -n 15 stuff
```

To examine each file with its last screenful:

```
more -P G file1 file2
```

To examine each file starting with line 100 in the current position (third line, so line 98 is the first line written):

```
more -p 100g file1 file2
```

To examine the file that contains the tagstring tag with line 30 in the current position:

```
more -t tag -p 30g
```

# WARNINGS

Standard error, file descriptor 2, is normally used for input during interactive use and should not be redirected (see Input/Output section in the manpage of the shell in use).

# FILES

/usr/share/lib/terminfo/?/* compiled terminal capability data base