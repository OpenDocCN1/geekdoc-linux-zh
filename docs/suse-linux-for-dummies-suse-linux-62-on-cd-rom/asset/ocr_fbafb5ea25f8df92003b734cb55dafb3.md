# 182 Part III: Using Linux

Now using a wildcard on a shell command line as follows:

```
maddog@localhost:~/reports > stuff *
The zeroth argument /home/maddog/bin/stuff
The first argument passwd1997007
The second argument passwd1997008
The third argument passwd1997009
The fourth argument passwd1997010
The number of expanded arguments 8
maddog@localhost:~/reports >
```

The shell expands the wildcard to include all the filenames that match the wildcard, in which case means all the files in the directory. The $$ argument reports eight arguments match the wildcard. Only four of the filenames are printed, however, because you requested only four arguments — filenames in this case — in your shell script.

To see that eight arguments are on the command line, type the following command:

```
echo *
```

The echo command echoes whatever appears to follow on it. If you type echo Hi here and press the Enter key, Hi there appears on the next line. If you type the command line echo 5342 and press Enter, 5342 appears on the line.

But when you type echo * in your reports directory and press Enter, something different from * appears on the next line. What appears the name of every file or directory name in the reports directory. This happens because the shell sees the * as a regular expression and expands it to match every filename or directory name in the directory that does not begin with a period. That expanded line is then presented to the echo command.

![](bbox=[0.085, 0.703, 0.193, 0.784])

The same thing happens to your shell script or any other shell script that has a regular expression passed to it as an argument. The shell — not the command or shell script you invoke — expands the regular expression. Because you created eight filenames in the reports directory, you know eight arguments are on the line (for the eight names in your directory), and not just the first.

Now add the proper regular expansion to cover all the files called passwd1998xx; there are six:

```
maddog@localhost:~/reports > stuff *1998\*
The zeroth argument /home/maddog/bin/stuff
The first argument passwd1998007
The second argument passwd1998008
The third argument passwd1998009
The fourth argument passwd1998010
```