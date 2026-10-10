In addition to the usual eight manual sections, you may find supplementary articles and technical papers describing the UNIX system. These are usually grouped together and called something like “Documents for Use with the UNIX System,” or “UNIX User’s Supplement,” or perhaps “UNIX Programmer’s Manual, Volume 2.” We won’t say much about this second part of the manual—if you happen to find a copy, you might want to browse through it to see if it contains anything of interest to you.

# ## B.2 Using the man Command

If your system has an on-line manual, you can read it using the man command, which has the general form

```
    $ man command (Return)
```

For example, to read the manual entry for the cal command, you would type

```
    $ man cal (Return)
```

If your system has an on-line manual, this command will list a man page for cal, as shown in Listing B-1.

# ## B.3 Organization of a Manual Entry

All manual entries follow much the same format. Let’s examine the various parts of the entry for the cal command:

+   * CAL (1)      USER COMMANDS      CAL (1)

The first line begins and ends with the name of the command, written entirely in caps (CAL). The number in parentheses (1) gives the section of the manual in which this entry is found.

+   * NAME
+       cal – display a calendar

The name and a one-line description of the command are listed next.

+   * SYNOPSIS
+       cal [ [ month ] year ]

This is probably the most useful part of the man page. It shows how the command is actually used. Anything shown in square brackets [ ] is optional. In this case, the brackets show that you can use the cal command either by itself, with the year only, or with the month and year. Thus, each of the following commands would be legal: