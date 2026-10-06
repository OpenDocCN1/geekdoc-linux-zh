# 548 Chapter 12 The Shell II: The Bourne Again Shell

change some some aspect of how the command functions. the pipe symbol alters the source of standard input or the destination of standard output, the background task symbol causes the shell to execute the task in the background so you get a prompt back right away and can continue working on other things.

Each of the following commands initiates a single job comprising three tasks:

```
$ s | y | z
$ is | -1 | grep tmp | less
```

In the first job, the shell directs the output from task x to task y and directs y's output to z. Because the shell runs the entire job in the foreground, task z does not finish until task y finishes, and task y does not finish until task x finishes. In the second job, task x is an -l command, task y is grep tmp, and task z is the pager. You end up with a long (wide) listing of the filenames of all the files in the working directory that contain the string tmp, piped through less.

The next command line executes tasks d and e in the background and task f in the following:

```
$ d & e & f
[1] 14271
[2] 14272
```

The shell displays the job number between brackets [1] and the PID (process identification) number for each process running in the background. You get a prompt back as soon as f finishes.

Before displaying a prompt for a new command, the shell checks whether any background jobs have completed. For each job that has completed, the shell displays its job number, the word done, and each command line that invoked the job; then the shell displays the prompt. When the job numbers are listed, the number of the last job started is followed by a + character, and the job number of the previous job is followed by a - character. Any other jobs listed a SPACE character. After running the last command, the shell displays the following before issuing a prompt:

+   [1]- Done
[2]+ Done

The following command line executes all three tasks as background jobs. You get a shell prompt immediately:

```
$ d & e & f
[1] 14290
[2] 14291
[3] 14292
```