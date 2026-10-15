awk processes and one sort process. In addition, vi and ps are listed as running. Note that my login shell (bash) isn’t in this listing.

Figure 15.1 explains each field, and Table 15.2 lists possible values for the STAT program status column.

![](bbox=[0.15, 0.18, 0.85, 0.38])

# FIGURE 15.1 The ps default process output.

| Value | Meaning |
| --- | --- |
| R | Running |
| S | Sleeping (20 seconds or less) |
| I | Idle (sleeping more than 20 seconds) |
| T | Stopped |
| Z | Zombie process |

# TABLE 15.2 Possible Process Status Values

Other process states exist, but they rarely show up for most users. A zombie process is one that has ended but hasn’t freed up its resources. Usually, it takes a second or two for the system to completely recover all memory used by a program. Sometimes, zombies are stuck in the process table for one reason or other. Unix folk refer to this as a wedged process, and such a process has an annoying habit of staying around until the system is rebooted. Sometimes these zombie processes can be listed as <defunct> in process listings. Any process that is preceded by a sleep command is noted as sleeping.

4. Adding some flags can change the output of ps quite dramatically:

Click here to view code image

```
$ ps -x
  PID TT STAT TIME COMMAND
 4352 Ah T 0:00 vi dickens.note
 6171 Ah R 0:02 awk - : {print $1""
 6172 Ah R 0:01 awk - , {print $1}
 6173 Ah S 0:01 -k { if (NF > 2) print $0 } (awk)
 6174 Ah S 0:00 sort
 6177 Ah R 0:00 ps -x
19189 Ah S 0:06 -bash (bash)
19649 Ah I 0:02 newmail
$
```

Two new processes show up here: -bash (the shell), which is, finally, my login shell; and newmail, a program that automatically starts in the background when I