# 372 Hour 17

Two new processes show up here: -csh (the shell) which is—finally—login
shell, and newwait, a program that automatically starts up in the background when
I log in the system (it's located at the end of my .login).

> The shell process is shown with a leading dash to indicate that it's a login
shell. Any other copies of csh that I run wont that leading dash.
That's one way the C shell knows not to read through the .login file every
time's run.

![](bbox=[0.165, 0.215, 0.275, 0.305])

5. To see more about what's happening, I did yet another flag, -u, to expand the
out on the display:

```
% ps -xu
USER PID %CU %MEM SZ RSS TT STAT ENG TIME COMMAND
taylor 7011 10.4 0.2 184 100 Ah R 6 0:02 awk - : {print "$1"
taylor 7012 6.3 0.1 160 92 Ah S 0:01 awk - : (print $1)
taylor 7013 5.9 0.1 160 116 Ah S 3 0:01 k - : (NF > 2)
print
taylor 19189 1.1 0.2 256 148 Ah S 0:07 (csh)
taylor 7014 1.0 0.1 316 64 Ah S 0:00 ps -xu
taylor 7022 0.0 0.2 452 168 Ah T 0 0:00 sort
taylor 19649 0.0 0.1 124 60 Ah I 0:02 newmail
%
```

Figure 17.2 explains these fields.

USER PID %CU %MEM SZ RSS TT STAT ENG TIME COMMAND
taylor 7011 10.4 0.2 104 100 Ah R 0:02 awk -.
name of the user amount of CPU used virtual memory used CPU terminal used time used
process ID amount of RAM used memory status
Because this is a multi-processor machine, this field indicates which process is idly running on.

Figure 17.2 - The user-oriented output of ps.

6. We won't show the output of the -aux flags, but we would look at the number of
lines produced by both the -ag and -ax flags:

```
% ps -ag | wc -
377
% ps -ag | head
PID TT STAT TIME COMMAND
1403 iw 0:01 -csh (csh)
2200 p iw 0:18 server
```

![](bbox=[0.095, 0.925, 0.145, 0.965])