# SCCS

# 1213

-1
Display information for all deltas later than,
including, that specified by -c -r.

-cdate-time (/usr/ccs/bin/sccs)
-c date-time | -cdate-time

Specify the latest delta checked in the indicated
delta and date-time argument takes the
form yy{dd [hb][mm[ss]]}}.

-rsid (/usr/ccs/bin/sccs)
-r sid | -rsid (/usr/xpg4/bin/sccs)

Specify a given delta by sid

prt [-y]
Display the delta table, but omit the field (sccsfile(4) for more
information on this field). See sccs-prt(1).

-y
Display the most recent delta entry. The format
is a single output line for each file argument;
format is convenient for use in a pipeline with awk(1)
or sed(1).

rmdel -rsid (/usr/ccs/bin/sccs)
rmdel -r sid (/usr/xpg4/bin/sccs)

Remove the indicated delta from the history file. That delta must be
t most recent (left) delta in its branch. See sccs-rmdel(1).

sact
sccsdiff -old-sid -new-sid diff-options
Show activity status of an SCCS file. See sccs-sact(1).

Compare versions corresponding to the indicated sid (deltas),
using diff. See sccs-sccsdiff(1).

tell [-b] [-u username] (/usr/ccs/bin/sccs)
tell [-b] [-u username] [-U] (/usr/xpg4/bin/sccs)

Display the list of files that are currently checked out, one per line.

-b
-u[username] (/usr/ccs/bin/sccs)
-u [username] | -U (/usr/xpg4/bin/sccs)

List only files checked out to. When you specify
username, list only files checked out to that user. For
/usr/xpg4/bin/sccs, the -U option is equivalent to -u
current-user.

undUndo the last edit or get -e, and return the working copy to its
previous condition. undedit backs all pending changes made since
the file was checked out.

unset
Same as undedit. See sccs-unset(1).

val
Validate the history file. See sccs-val(1).

what
Display any expanded ID keyword strings contained in a binary
(object) or text file. See what(1) for more information.