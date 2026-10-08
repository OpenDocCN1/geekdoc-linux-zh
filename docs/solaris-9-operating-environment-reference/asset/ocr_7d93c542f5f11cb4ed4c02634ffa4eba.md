# sccs-cdc, cdc — Change the Commentary of an SCCS
Delta

Synopsis
/usr/ccs/bin/cdc -rsid [-mmr-list] [-y [comment]] s.filename...

Description
Use the SCCS cdc (change delta commentary) command to annotate the delta
commentary for the SCCS delta ID (sid) specified by the -r option in each name s. file.
If the v flag is set in the file, you can also use cdc to update the Modification
Request (MR) list.
If you checked in the delta or if you own the file and directory and write
permission, you can use cdc to annotate the commentary.
Instead of replacing the existing commentary, cdc inserts the new comment you
supply, followed by a line of the form above the existing commentary.

```
*** CHANGED *** yy/mm/dd hh:mm/ss username
```

If a directory is named as the s.filename argument, the cdc command applies to all
s in directory. Unreadable files produce an error: processing continues
with the next file (if any). If you specify a - (-) as s.filename argument, each
line of the standard input is taken as the name of an SCCS history file to be processed
and you must also use the -m and -y options.

# Options

+   -mmr-list Specify one or more MR numbers to add or delete. When specifying
than one MR on the command line, specify mr-list as a quoted,
space-separated list. To delete an MR number, precede it with a !
character (an empty MR list has no effect). Put a list of deleted MRs in the
comment section of the delta commentary. If you do not use the -m
option and the standard input is a terminal, cdc prompts with MR? for
the list is useful only when
v flag is set in the file. If that flag has a value, it is to
name of a program to validate the MR numbers. If that validation
program returns a non-zero exit status, cdc terminates and the delta
commentary remains unchanged.

+   -rsid Specify the delta to change.

+   -y [comment] Use comment as the annotation in the delta commentary. Retain
the previous comments; add the comment along with a notation that the
commentary was changed. A null comment leaves the commentary
unaffected. If you do not specify -y and the standard input is a
terminal, cdc prompts with comments? for the text of the notation to be
added. You terminate the annotation text with an unescaped newline