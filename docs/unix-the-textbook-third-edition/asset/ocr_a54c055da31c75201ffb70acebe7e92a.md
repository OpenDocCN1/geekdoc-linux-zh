```
11:00 A.M. - 12:00 P.M.
$ diff Fall_OH Spring_OH
1c1
< Office Hours for Fall 2014
---
> Office Hours for Spring 2015
6a7
> 1:00 - 2:00 P.M.
9d9
< 3:00 - 4:00 P.M.
12,13d11
< 2:00 - 3:00 P.M.
< 4:00 - 4:30 P.M.
$
```

The instruction 1c1 asks the ed editor to change the first line in the Fall_OH file (Office Hours for Fall 2014) to the first line in the Spring_OH file (Office Hours for Spring 2015). The 6a7 instruction asks the ed editor to append line 7 in Spring_OH after line 6 in Fall_OH. The 12,13d11 instruction asks the ed editor to delete lines 12 and 13 from Fall_OH.

The following session illustrates use of the -e option with the diff command and how the output of this command can be given to the ed editor in order to make Fall_OH the same as Spring_OH. The command is used to show you what the output of the command looks like. The second diff command (with > diff.script) is used to save the command output (the ed script) in the diff.script file. The cat >> diff.script command is used to convert the diff.script file into a complete working script for the ed editor by adding two lines containing w and q. As previously stated, this command terminates with <Ctrl+D>. Finally, the ed command is run to change the contents of Fall_OH, according to the script produced by the diff -e command, and make it the same as Spring_OH. The numbers 209 and 177 show the sizes of the Fall_OH file before and after the execution of the ed command. The last command, diff Fall_OH Spring_OH, is run to confirm that the two files are the same.

```
$ diff -e Fall_OH Spring_OH
12,13d
9d
6a
1:00 - 2:00 P.M.
.
1c
Office Hours for Spring 2015
.
$ diff -e Fall_OH Spring_OH > diff.script
$ cat >> diff.script
w
q
```