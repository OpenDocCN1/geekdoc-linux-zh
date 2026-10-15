
![](img/02e070097d401d3bf7de4bf1c470b267_350_0.png)

## FIGURE 9.6 Error redirection: (a) standard descriptors and standard files for command; (b) semantics of error redirection.

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

Keeping standard error attached to the display screen and not redirecting it to a file is useful in many situations. For example, when the cat lab1 lab2 lab3 > all command is executed to concatenate files lab1, lab2, and lab3 into a file called all, you would want to know whether any of the three input files are nonexistent or if you do not have permission to read any of them. In this case, redirecting the error message to a file does not make much sense because you want to see the immediate results of the command execution.

## 9.8 REDIRECTING stdout AND stderr IN ONE COMMAND

Standard output and standard error can be redirected to the same file. One obvious way to do so is to redirect stdout and stderr to the same file by using file descriptors with the > symbol, as in the following command.

```
$ cat lab1 lab2 lab3 1> cat.output 2> cat.errors
$
```

In this case, the input of the cat command comes from the lab1, lab2, and lab3 files, its output goes to the cat.output file, and any error message goes to the cat.errors file, as shown in Figure 9.7. Note that, although not shown in Figure 9.7b, files lab1, lab2, and lab3 have file descriptors assigned to them when they are opened for reading by the cat command. The command produces an error message if any one of the three "lab" files does not exist or if you do not have read permission for any of these files.

The following command redirects the stdout and stderr of the cat command to the cat.output.errors file. Thus, the same file (cat.output.errors) contains the output of the cat command, along with any error messages that may be produced by the command.

```
$ cat lab1 lab2 lab3 1> cat.output.errors 2>&1
$
```

In this command, the string 2>&1 tells the command shell to make descriptor 2 a duplicate of descriptor 1, resulting in the error messages going to the same place that the command output goes to. Similarly, the string 1>&2 can be used to tell the command shell to make descriptor 1 a duplicate of descriptor 2. Thus, the following command accomplishes the same task. Figure 9.8 shows the semantics of the two commands.

![](img/02e070097d401d3bf7de4bf1c470b267_351_0.png)

![](img/02e070097d401d3bf7de4bf1c470b267_352_0.png)

FIGURE 9.8 Error redirection: (a) file descriptors and standard files; (b) semantics of the cat lab1 lab2 lab3 1> cat.output.errors 2>&1 and cat lab1 lab2 lab3 2> cat.output.errors 1>&2 commands.

```
$ cat lab1 lab2 lab3 2> cat.output.errors 1>&2
$
```

The evaluation of the command line content for file redirection is left to right. Therefore, redirections must be specified in the left-to-right order if one notation is dependent on another. In the preceding command, first, stderr is changed to the file cat.output.errors, and then stdout becomes a duplicate of stderr. Thus, the output and errors for the command both go to the same file, cat.output.errors.

The following command therefore does not have the effect of the two commands just discussed. The reason is that, in this command, stderr is made a duplicate of stdout before output redirection. Therefore, stderr becomes a duplicate of stdout (the display screen at this time) first, and then stdout is changed to the file cat.output.errors. Thus, the output of the command goes to cat.output.errors and errors go to the display screen. The sequence shown in Figure 9.9 illustrates the semantics of this command.

```
$ cat lab1 lab2 lab3 2>&1 1> cat.output.errors
$
```

Note that Figure 9.9a and b are identical because the execution of cat lab1 lab2 lab3 2>&1 does not make any changes to stdout and stderr—they stay attached to the display screen before and after the command is executed.

## 9.9 REDIRECTING stdin, stdout, AND STDERR IN ONE COMMAND

Standard input, standard output, and standard error can be redirected in a single command according to the following syntax.
