# sccs-sccdiff, sccsdiff

# See Also

sccs(1), sccs-delta(1), sccs-get(1), sccs-help(1), sccs-prs(1), sccs-prt(1), what(1), sccsfile(4), attributes(5)

# Diagnostics

Use the SCCS help command for explanations (see sccs-help(1)).

# Bugs

sact is not recognized as a subcommand of sccs(1).

# sccs-sccdiff, sccdiff — Compare Two Versions of an SCCS File

# Synopsis

```
/usr/ccs/bin/sccdiff [-p] -r sid -r sid [diff-options] s.filename
```

# Description

Use the SCCS sccdiff command to compare two versions of an SCCS file and display the differences between the two versions. You can specify any number of SCCS files; the options specified applied to all named s. files.

# Options

+   -p Pipe output for each file through pr(1).
-r sid Specify a version corresponding to the indicated SCCS delta ID (sid) for comparison. Versions are passed to diff(1) in the order given.

```
diff-options Pass options to diff(1), including -b, -c, -C number, -D string-e, -f, -w
-h, -u, and -U number.
```

# Files

```
/tmp/get????
```

Temporary files.

# Attributes

Use attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUMsprot |

# See Also

diff(1), sccs(1), sccs-delta(1), sccs-get(1), sccs-help(1), sccs-prs(1), sccs-prt(1), what(1), sccsfile(4), attributes(5)