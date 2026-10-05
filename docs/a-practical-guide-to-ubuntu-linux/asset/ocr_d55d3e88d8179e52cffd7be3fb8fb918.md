unfinished command. In the next example, the first RETURN is quoted (escaped) so the shell treats it as a separator and does not interpret it literally.

```
$ echo "Please enter the three values \\n> required to complete the transaction."
Please enter the three values required to complete the transaction.
```

Single quotation marks cause the shell to interpret a backslash literally:

```
$ echo 'Please enter the three values \\n> required to complete the transaction.'
Please enter the three values \
> required to complete the transaction.
```

# AND & SEPARATE COMMANDS AND DO SOMETHING ELSE

The pipe symbol (!) and the background task symbol (&) are also command separators. They do not start execution of a command but do change some aspect of how the command functions. The pipe symbol alters the source of standard input or the destination of standard output. The background task symbol causes the shell to execute the task in the background and display a prompt immediately; you can continue working on other tasks.

Each of the following command initiates a single job comprising three tasks:

```
$ x l | z
$ ls -1 | grep tmp | less
```

In the first job, the shell redirects standard output of task x to standard input of y and redirects y's output to z's standard input. Because it runs the entire job in the foreground, the shell does not display a prompt until z runs to completion: Task z does not finish until y finishes, and y does not finish until x finishes. In the second job, task x is an ls -l command, task y is grep tmp, and task z is the pager. The shell displays a job number (wide) listing of the files in the working directory that contain the string tmp, piped through less.

The next command executes tasks d and e in the background and task f in the foreground:

```
$ d e & & f
[1] 14271
[2] 14272
```

The shell displays the job number between brackets and the PID number for each process running in the background. It displays a prompt as soon as f finishes, which may be before d or finishes.

Before displaying a prompt for a new command, the shell checks whether any background jobs have completed. For completed job, the shell displays its job number, the word Done, and the command that invoked the job; the shell then displays a prompt. When jobs are listed, the number of the last job started is followed by a + character and the job number of the previous is