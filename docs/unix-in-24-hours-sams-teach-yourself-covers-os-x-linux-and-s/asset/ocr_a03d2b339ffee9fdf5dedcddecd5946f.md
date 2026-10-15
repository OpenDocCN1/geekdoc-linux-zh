log in to the system (it’s located at the end of my .login).

# Note

The shell process is shown with a leading dash to indicate that it’s a login shell. Any other copies of bash that I run won’t have that leading dash. This is one way the shell knows not to read through the .login file every time it’s run.

5. To see more about what’s happening, I add yet another flag, -f, to expand the output on the display:

Click here to view code image

```
$ ps -xf
USER       PID %CPU %MEM    SZ   RSS TT  STAT ENG   TIME COMMAND
taylor    7011 10.4  0.2  184   100 Ah R       6   0:02 awk - : {print $1""
 taylor    7012  6.3  0.1  160    92 Ah S           0:01 awk - , {print $1}
taylor    7013  5.9  0.1  160    92 Ah R       3   0:01 -k { if (NF > 2)
print
taylor   19189  1.1  0.2  256   148 Ah S           0:07 -bash (bash)
taylor    7014  1.0  0.1  316    64 Ah S           0:00 sort
taylor    7022  0.1  0.2  180   116 Ah R       0   0:00 ps -xu
taylor    4352  0.0  0.3  452   168 Ah T           0:00 vi dickens.note
taylor   19649  0.0  0.1  124    60 Ah I           0:02 newmail
$
```

Figure 15.2 explains these fields.

![](bbox=[0.08, 0.76, 0.9, 0.9])

# FIGURE 15.2 The -f user-oriented output of ps.

6. On a Solaris workstation, the output of the ps command is a bit different:

Click here to view code image

```
$ ps
  PID TTY      TIME COMMAND
 8172 pts/2   0:00 -bash (bash)
 8182 pts/2   0:00 vi
 8186 pts/2   0:00 ps
$
```

In many ways, though, these different Unixes still have very similar output from the ps commands. For example, consider this Mac OS X output from ps -ef to the ps -xu output on the Solaris system that I showed earlier: