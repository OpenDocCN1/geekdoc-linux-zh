```
```sh
if [ "$mailopt" = FALSE ] ; then
    echo "$user has logged on"
else
    runner=$(who am i | cut -c1-8)
    echo "$user has logged on" | mail $runner
fi
) &
$ 
```
```

The entire program could have been enclosed in parentheses, but we decided to do the argument checking and parsing prior to moving the program into the background.

```
```sh
$ waitfor fred
$
...
fred has logged on
```
```

*Prompt comes back so you can continue working*

Note that a process ID is not printed by the shell when a command is sent to the background within a shell program.

# Another Way to Pass Variables to a Subshell

If you want to send the value of a variable to a subshell, there’s another way to do it besides exporting the variable. On the command line, precede the command with the assignment of one or more variables. For example,

```
```sh
DBHOME=/uxn2/data DBID=452 dbrun
```
```

places the variables DBHOME and DBID, and their indicated values, into the environment of dbrun, then dbrun gets executed. These variables will not be known to the current shell, however, because they’re only created for the execution of dbrun.

In fact, the preceding command behaves identically to typing

```
```sh
(DBHOME=/uxn2/data; DBID=452; export DBHOME DBID; dbrun)
```
```

Here’s a short example:

```
```sh
$ cat foo1
echo $x:
foo2
$ cat foo2
echo :$x:
$ foo1
::
$ x=100 foo1
:100
:100
$ echo :$x:
::
$
```
```

*x not known to foo1 or foo2*

*Try it this way*

*x is known to foo1*

*and to its subshells*

*Still not known to current shell*