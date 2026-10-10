the entire system. Either of these numbers can be used to interact with the program through **bash**. As you can see, the pid is used to kill the running program.

# Example 3.14

```
```
$ ./job-cntrl &
[1] 3510
$ kill 3510
$
[1]+ Terminated        ./job-cntrl
```
```

The **jobs** command is a **bash** command that is used to examine all the programs **bash** is currently executing. To suspend a process running in the foreground, press Ctrl+z (denoted by <sup>^</sup>Z in the examples). After the foreground process is suspended, you can then manipulate it using the commands **bg** (background the command) and **fg** (return the command to the foreground). You can also refer to the command by its job number by placing a % sign in front of its job number. All this is shown in Example 3.15.

# Example 3.15

```
```
$ ./job-cntrl
^Z
[1]+ Stopped           ./job-cntrl
$ bg
[1]+ ./job-cntrl &
$ jobs
[1]+ Running           ./job-cntrl &
$ kill %1
[1]+ Terminated        ./job-cntrl
```
```

Here job-cntrl is started, suspended with Ctrl+z, and backgrounded with bg. Then the jobs running are examined, and the job is killed using its job number (kill %1).

# ## Shell Syntax

Because **bash** is a Bourne-style shell, it shares a largely common syntax with **sh** and other Bourne-type shells. The way you address commands, arguments, values, and program shell scripts is one of the major distinguishing features among the major shell types. Bourne syntax is visually different from C shell and from Korn shell (although the differences with Korn shell are somewhat less obvious). The major linguistic constructs needed to work and program within **bash** follow.

Linux supports long filenames (up to 255 characters) and has for quite a long time now. It also supports spaces in names—files, variables, and the like. People don’t often use spaces, but it is important and useful to know how. It is, however, necessary to quote or escape spaces and some other special characters in order to get **bash** to recognize them. You quote them by enclosing them in single (`''`) or double (`""`) quotes or by using the