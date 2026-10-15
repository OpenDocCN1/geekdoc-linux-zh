![](bbox=[0.09, 0.12, 0.92, 0.38])

# FIGURE 9.6 Error redirection: (a) standard descriptors and standard files for command; (b) semantics of error redirection.

With this syntax, command takes its input from the keyboard, sends its output to the monitor screen, and any error messages produced by command are sent to error-file. The semantics of the command syntax are shown in Figure 9.6. Command input may come from a file passed as a command line argument.

The command grep "John" Phones 2> error.log takes input from the Phones file, sends output to the display screen, and any error message produced by grep goes to a file called error.log. If error.log already exists, it is overwritten; otherwise, it is created. The following example shows how the standard error of ls -l can be redirected to a file.

```
$ ls -l foo 2> error.log
... long listing for foo if no errors ...
$
```

The output of ls -l foo goes to the display screen, and error messages go to error.log. Thus, if foo does not exist, the error message ls: foo: No such file or directory goes into the error.log file, as shown in the following session. The actual wording of the message varies from system to system, but it basically informs you that foo does not exist.

```
$ ls -l foo 2> error.log
$ cat error.log
ls: foo: No such file or directory
$
```

Keeping standard error attached to the display screen and not redirecting it to a file is useful in many situations. For example, when the cat lab1 lab2 lab3 > all command is executed to concatenate files lab1, lab2, and lab3 into a file called all, you would want to know whether any of the three input files are nonexistent or if you do not have permission to read any of them. In this case, redirecting the error message to a file does