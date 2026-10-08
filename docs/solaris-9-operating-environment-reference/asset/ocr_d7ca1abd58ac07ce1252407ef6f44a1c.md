# sccs-delta, delta — Make a Delta to an SCCS File

# Synopsis

```
/usr/ccs/bin/delta [-dnps] [-g sid-list] [-gsid-list] [-m mr-list |
-mnr-list] [-r sid -rsid] [-y-comment] s.filename...
/usr/xpg4/bin/delta [-dnps] [-g sid-list] [-gsid-list] [-m mr-list |
-mnr-list] [-r sid -rsid] [-y-comment] s.filename...
```

Use the SCCS delta command to check in a record of line-by-line differences between a checked-out version of a file under SCCS control. These changes are taken from the writable copy that was retrieved with the SCCS get command (see sccs-get(1)). This working copy does not have the s prefix and is also referred to as a g-file.

If you specify a directory in place of the .filename, the delta command applies to all s. files in that directory. Unreadable s. files produce an error; processing continues with the next file (if any). The use of a dash (-) as the s.filename argument indicates that the names of file are to read from the standard input, s. file per line (requires -y, and in some cases, -m).

delta can issue prompts to the standard output depending on the options specified, the flags that are set in the s. file (see sccs-admin(1), and the m and -y options).

```
/usr/xpg4/bin/delta
sid of the delta is not echoed to output stdout.
```

# Options

+   -d
Use the diff(1) command instead of bdiff(1). Return exit status 2 if you do not specify the s.filename argument.

+   -g sid-list -gsid-list
Specify a list of deltas to omit when the file is accessed at the SCCS
version ID (sid) created by this delta. sid-list is a comma-separated
list of sids. To specify a range of deltas, use a hyphen (-) separator instead of a comma, between two sids in the list.

+   -m mr-list -mr-list
If the SCCS file has the v flag set (see sccs-admin(1)), you must supply one or more Modification Request (MR) numbers for the new delta. When you specify more than one MR on the command line, mr-list takes the form of a quoted, space-separated list. If you do not use -m and the standard input is a terminal, delta prompts with MRs for the list (before displaying the comments? prompt). If the v flag in the s. file has a value, take it to be the name of a program to validate the MR numbers. If that validation program returns a non-zero exit status, terminate without checking the changes.

+   -n
Retain the edited g-file that is normally removed at the completion of processing.

Options