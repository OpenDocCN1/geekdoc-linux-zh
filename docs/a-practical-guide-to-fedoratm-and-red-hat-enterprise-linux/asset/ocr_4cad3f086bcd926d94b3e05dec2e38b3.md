*kill* [–*signal*] *PID*

where *signal* is the signal name or number (for example, INT or 2) and *PID* is the process identification number of the process that is to receive the signal. You can specify a job number (page 163) as *%n* in place of *PID*. If you omit *signal*, *kill* sends a *TERM* (software termination, number 15) signal. For more information on signal names and numbers, see Table 27-5 on page 1047.

The following command sends the *TERM* signal to job number 1, regardless of whether it is running or stopped in the background:

```
$ kill --TERM %1
```

Because *TERM* is the default signal for *kill*, you can also give this command as *kill* *%1*. Give the command *kill* -l (lowercase “el”) to display a list of signal names. A program that is interrupted can leave matters in an unpredictable state: Temporary files might be left behind (when they are normally removed), and permissions might be changed. A well-written application traps signals and cleans up before exiting. Most carefully written applications trap the INT, QUIT, and *TERM* signals. To terminate a program, first try INT (press CONTROL-C, if the job running is in the foreground). Because an application can be written to ignore this signal, you might need to use the *KILL* signal, which cannot be trapped or ignored; it is a “sure kill.” For more information refer to “Kill: Sends a Signal to a Process” on page 465.

# eval: SCANS, EVALUATES, AND EXECUTES A COMMAND LINE

The *eval* builtin scans the command that follows it on the command line. In doing so, *eval* processes the command line in the same way *bash* does when it executes a command line (e.g., it expands variables, replacing the name of a variable with its value). For more information refer to “Processing the Command Line” on page 403. After scanning (and expanding) the command line, it passes the resulting command line to *bash* to execute.

The following example first assigns the value *frog* to the variable *name*. Next *eval* scans the command *\$name=88* and expands the variable *\$name* to *frog*, yielding the command *frog=88*, which it passes to *bash* to execute. The last command displays the value of *frog*.

```
$ name=frog
$ eval \$name=88
$ echo \$frog
88
```

with a sequence expression

The next example uses *eval* to cause brace expansion with a sequence expression (page 406) to accept variables, which it does not normally do. The following command demonstrates brace expansion with a sequence expression:

```
$ echo {2..5}
2 3 4 5
```