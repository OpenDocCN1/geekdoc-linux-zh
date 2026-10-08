An argument can be a message number (which normally appears in parentheses)
following each SCCS error or warning message) or a SCCS command name. help
responds with an explanation of the message or a usage line for the command.
When all else fails, try /usr/ccs/bin/help stuck.

```
/usr/lib/help
```

Directory containing files of message text.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUMsprot |

# See Also

sccs(1), sccs-admin(1), sccs-cdc(1), sccs-comb(1), sccs-delta(1),
sccs-get(1), sccs-prs(1), sccs-prt(1), sccs-rmdel(1), sccs-sact(1),
sccs-scsdiff(1), sccs-unset(1), sccs-val(1), what(1), sccsfile(4),
attributes

# sccs-prs, prs — Display Portions of an SCCS History

# Synopsis

```
/usr/ccs/bin/prs [-ael] [-cdate-time] [-ddataspec] [-rsid] s.filename.
```

# Description

Use the SCCS prs (peruse) command to display part or all of the SCCS file (see
sccsfile(4)) in a user-supplied format.

If you use a directory name in the s.filename argument, the prs command
applies to all s in that directory. Unreadable s. files produce an error, processing
continues with the next file (if any). The use of a dash (-) as the s.filename argument
indicates that the names of files are to read from the standard input, s. per
line.

# Options

In the absence of options, prs displays the delta table (version log). In the absence of -d
or -1, prs displays the entry for each delta indicated by the other options.

+   -a
  Include all deltas, those marked as removed (see
  sccs-rmdel(1)).
-e
  Request information for all deltas created earlier than, and including,
  the delta indicated with -r or -c.
-1
  Request information for all deltas created later than, and including, the
  delta indicated with -r or -c.