The following commands show how to cancel a print job. You can display the job IDs of the print jobs on a printer by using the lpstat or lpq command, as shown is Section 6.8.3. The first command cancels the print job mpr-3991. The second command cancels all print requests by the user sarwar on all printers. You can cancel your own print jobs only. The last command, therefore, works only when run by sarwar or the superuser.

```
$ cancel mpr-3991
request "mpr-3991" canceled
$ cancel -u sarwar mpr
request "mpr-3992" canceled
request "mpr-3995" canceled
$
```

The BSD counterpart of the cancel command is lprm. The following is a brief description of the command.

# SYNTAX

```
lprm [options] [jobID-list] [user(s)]
```

Purpose: Cancel the print requests made by using the lpr command—i.e., remove these jobs from the print queue; the jobIDs in jobID-list are taken from the output of the lpq command

Commonly used options/features:
- Remove all the print jobs owned by user
-P ptr Specify the print queue for the ptr printer

The following lprm commands perform the same tasks as the cancel commands described in the previous session.

```
$ lprm -P mpr 3991
mpr-3996 dequeued
$ lprm -P mpr sarwar
mpr-3997 dequeued
mpr-3998 dequeued
$
```

When run without an argument, the lprm command removes the job that is currently active, provided it is one of your jobs.

The following in-chapter exercises will give you practice on using the printing-related commands.

# EXERCISE 6.11

How would you print five copies of the file memo on the printer ece_hpl? Give commands for both System V and BSD UNIX.