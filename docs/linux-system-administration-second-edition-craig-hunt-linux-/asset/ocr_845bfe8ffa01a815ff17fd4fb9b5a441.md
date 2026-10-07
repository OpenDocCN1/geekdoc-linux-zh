# lp rm

```
lp rm [-P printer] [-] [job #] [user]
```

The lp rm (line printer remove) command is used to remove print jobs from the queue of the specified or default printer. If a job number is specified, only that job will be removed. If a username is specified by the superuser, all jobs for that user will be removed. If only a dash is given, all jobs owned by the user who issued the command will be removed. If the superuser gives this command with the – (dash) option, the printer spool will be emptied.

# Other Useful Commands

A few commonly used commands don't fit into any of the other categories.

# date

```
date [options] [+FORMAT]
date [options] [MMDDhhmm[[CC]YY][.ss]]
```

The date command prints or sets the system's date and time. If no option is specified, the current date and time will be printed to stdout in this format:

```
[DAY MON DD hh:mm:ss TIMEZONE YYYY]
```

You may change the format by adding + and a format string to the command. The format string can take any form you like as long as you use a defined set of symbols, which you can find in the man page.

Here are a couple of examples:

```
# date +%m/%d/%y
9/1/00
```

When you specify date information as an argument in the form:

```
[MMDDhhmm[[CC]YY][.ss]]
```

the system's date will be changed to the given date and time:

```
# date 0901182600.00
Fri Sep 1 18:26:00 CDT 2000
```

# hdparm

```
hdparm [options] device
```

The hdparm (hard disk parameters) command retrieves or sets specified parameters of the specified hard drive. This command was primarily developed for use with IDE hard drives, but some parameters apply to SCSI drives, too.

# dmesg

```
dmesg [-c] [-n message_level] [-s buffersize]
```

107