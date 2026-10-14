# Figure 5-3 The output of a simple sort command

When you have multiple versions of a file, Linux provides several commands that help you see differences in those versions. These commands are most frequently used for programming—to see what changes have been made to source code—but they are also useful for configuration files, Web pages, and documentation.

The diff command is the most widely used of these comparison commands. When you include two file names on the diff command line, it displays the differences between the two files. The output format of diff is strange when you first see it, but it is a standard format that is understood by thousands of programmers and system administrators. Suppose, for example, that you made a backup copy of a configuration file called smb.conf and then edited the original (this file controls the Samba server, which is not discussed in this book). If you changed the workgroup name in that file and added a comment describing the change you made (a good practice), the following diff command would show your changes:

```
$ diff oldsmb.conf smb.conf
18c18,19
< workgroup = MYGROUP
---
> #Changed MYGROUP to HOME on 5-23-05
> workgroup = HOME
```

The first line of the output indicates the line numbers where the difference was found—lines 18 and 19. Lines starting with < indicate lines that were not found in the second file; lines starting with > indicate lines that were not found in the first file. Another way to think of this is that if the second file listed on the command line is the more recent file, the < and > indicate lines that have been removed and inserted, respectively, when compared to the older file. The output of the diff command can be handy to review manually, but it is also used by many programming commands to automatically make