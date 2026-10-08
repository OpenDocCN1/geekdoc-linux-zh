# 7. On a Sun workstation, the output of the ps commands is a bit different:

```
% ps
PID TT STAT TIME COMMAND
8172 qb S 0:00 -csh (csh)
8182 qb T 0:00 vi
8186 qb R 0:00 ps
```

In many ways, these different artworks have very similar output from the ps commands. For example, compare this Sequent output from ps -xu to the ps -xu output on the Sun that I showed:

```
% -xu
USER PID %CPU MEM SZ RSS TT STAT START TIME COMMAND
taylor 8191 7 0.4 284 538 q R 19:16 0:00 ps -xu
taylor 8182 0 0.4 144 132 q T 19:16 0:00 vi
taylor 8172 0 0.3 68 400 q S 19:16 0:00 -csh (csh)
taylor 8180 0 0.1 52 144 q S 19:16 0:00 newmail
```

The ENG column of the previous examples is replaced by a START column on the Sun workstation. The numbers in the ENG column indicate the exact time that the processes were started on.

UNIX works with processes. Your login shell, the edit session you run, and even the program listing your files are all processes in the operating system. This means you can work with processes. You can stop programs temporarily to do something else, restart them as you choose, and even look at all the programs you're running at any time, including other hidden processes such as your login shell itself.

# Task 17.4: Terminating Processes with kill

Now that you know how to create processes, suck some into the background, and find processes, you need some way to permanently stop them from running. The command to accomplish this in UNIX is kill. For the most part, use kill, you specify the process ID numbers of those programs you want to terminate. Both the C shell and Korn have a convenient shorthand that you've already seen: the percent-job-number notation.

There are a variety of signals that the kill can send to a process. To do a job control action, you need to specify one of different signals. Table 17.3 lists signals you can use with kill.

# Table 17.3. Some signals to use with kill.

| Number | Name | Meaning |
|---|---|---|
| 1 | SIGHUP | Hang up |
| 2 | SIGINT | Interrupt |

![](bbox=[0.05, 0.88, 0.155, 0.97])