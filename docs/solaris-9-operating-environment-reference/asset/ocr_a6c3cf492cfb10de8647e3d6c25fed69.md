# sccsdiff

# 1225

# See Also

bdiff(1), diff(1), sccs(1), sccs-admin(1), sccs-cdc(1), sccs-get(1),
sccs-help(1), sccs-prs(1), sccs-prt(1), sccs-rmdel(1), sccs-sccsd(1),
sccs-unset(1), what(1), sccsfile(4), attributes(5), XPG4(5)

# Diagnostics

Use the SCCS help command for explanations (see sccs-help(1)).

# Warnings

Lines beginning with an ASCII SOH character (binary 001) cannot be put into the SCCS file unless you escape the SOH. character has special meaning to SCCS (see sccsfile(4)) and produces an error.

# sccsdiff — Compare Two Versions of an SCCS File

# Synopsis

```
/usr/ccs/bin/sccsdiff [-p] -r sid -r sid [diff-options]
s.filename
```

# Description

See sccs-sccsdiff(1).

# sccs-get, get — Retrieve a Version of an SCCS File

# Synopsis

```
/usr/ccs/bin/get [-begkmpst] [-p] [-sequence] [-c date-time |
[-date-time] [-G-file] [-i sid-list] [-isid-list] -r[sid]
-x sid-list [-xid-list] s.filename...
/usr/pg4/bin/get [-begkmpst] [-p] [-a sequence] [-c date-time |
[-date-time] [-G-file] [-i sid-list] [-isid-list] -r sid [-rsid]
-x sid-list [-xid-list] s.filename ...
```

# Description

Use the SCCS get to retrieve a working copy from the SCCS history file, using the specified options.

For each s.filename argument, get displays the SCCS delta ID (sid) and number of lines retrieved.
If you use a directory name in place of the s.filename argument, the get command applies to all s.files in directory. Unreadable files produce an error, processing continues with the next file (if any). A dash (-) as the s.filename indicates that the names of files to be read from the standard input, one s.file per line.

The retrieved file normally has the same file-name base as the s.file, less the prefix, and is referred to as the g-file.
For each file processed, get responds (to the standard output) with the sid being and with the number of lines retrieved from the s.file.