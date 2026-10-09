
followed by a `--` character. Other jobs are followed by a `SPACE` character. After running the last command, the shell displays the following lines before issuing a prompt:

```
[1]– Done
[2]+ Done
```

The next command line executes all three tasks as background jobs. The shell displays a shell prompt immediately:

```
$ d && e && f &
[1] 14290
[2] 14291
[3] 14292
```

You can use pipes to send the output from one task to the next task and an ampersand (`&`) to run the entire job as a background task. Again the shell displays the prompt immediately. The shell regards the commands joined by a pipe as a single job. That is, it treats all pipes as single jobs, no matter how many tasks are connected with the pipe (`|`) symbol or how complex they are. The Bourne Again Shell reports only one process in the background (although there are three):

```
$ d | e | f &
[1] 14295
```

## **optional ( ) Groups Commands**

You can use parentheses to group commands. The shell creates a copy of itself, called a *subshell*, for each group. It treats each group of commands as a job and creates a new process to execute each command (refer to “Process Structure” on page 328 for more information on creating subshells). Each subshell (job) has its own environment, meaning that it has its own set of variables whose values can differ from those found in other subshells.

The following command line executes commands **a** and **b** sequentially in the background while executing **c** in the background. The shell displays a prompt immediately.

```
$ (a ; b) && c &
[1] 15520
[2] 15521
```

The preceding example differs from the earlier example `d && c && f &` in that tasks **a** and **b** are initiated sequentially, not concurrently.

Similarly the following command line executes **a** and **b** sequentially in the background and, at the same time, executes **c** and **d** sequentially in the background. The subshell running **a** and **b** and the subshell running **c** and **d** run concurrently. The shell displays a prompt immediately.

```
$ (a ; b) && (c ; d) &
[1] 15528
[2] 15529
```

The next script copies one directory to another. The second pair of parentheses creates a subshell to run the commands following the pipe. Because of these parentheses, the output of the first tar command is available for the second tar command despite the intervening cd command. Without the parentheses, the output of the first tar command would be sent to cd and lost because cd does not process input from standard input. The shell variables $1 and $2 represent the first and second command-line arguments (page 997), respectively. The first pair of parentheses, which creates a subshell to run the first two commands, allows users to call cpd1r with relative pathnames. Without them, the first cd command would change the working directory of the script (and consequently the working directory of the second cd command). With them, only the working directory of the subshell is changed.

```
$ cat cpd1r
(cd $1 ; tar -cf - . ) | (cd $2 ; tar -xvf - )
$ . /cpd1r /home/max/sources /home/max/memo/biblio
```

The cpd1r command line copies the files and directories in the /home/max/sources directory to the directory named /home/max/memo/biblio. This shell script is almost the same as using cp with the -r option. Refer to the cp and tar man pages for more information.

## JOB CONTROL

A job is a command pipeline. You run a simple job whenever you give the shell a command. For example, if you type date on the command line and press RETURN, you have run a job. You can also create several jobs with multiple commands on a single command line:

```
$ find . -print | sort | lpr & grep -l max /tmp/* > maxfiles &
[1] 18839
[2] 18876
```

The portion of the command line up to the first & is one job consisting of three processes connected by pipes: find, sort (page 168), and lpr (page 165). The second job is a single process running grep. The trailing & characters put each job in the background, so bash does not wait for them to complete before displaying a prompt.

Using job control you can move commands from the foreground to the background (and vice versa), stop commands temporarily, and list all commands that are running in the background or stopped.

### jobs: LISTS JOBS

The jobs builtin lists all background jobs. Following, the sleep command runs in the background and creates a background job that jobs reports on:

```
$ sleep 60 &
[1] 7809
$ jobs
[1] + Running s1eep 60 &
```

### fg: Brings A Job to the Foreground

The shell assigns a job number to each command you run in the background. For each job run in the background, the shell lists the job number and PID number immediately, just before it issues a prompt:

```
$ xclock &
[1] 1246
$ date &
[2] 1247
$ Tue Dec 7 11:44:40 PST 2010
[2]+ Done                date
$ find /usr -name ace -print > findout &
[2] 1269
$ jobs
[1]-  Running     xclock &
[2]+ Running       find /usr -name ace -print > findout &
```

Job numbers, which are discarded when a job is finished, can be reused. When you start or put a job in the background, the shell assigns a job number that is one more than the highest job number in use.

In the preceding example, the **jobs** command lists the first job, **xclock**, as job 1. The **date** command does not appear in the **jobs** list because it finished before **jobs** was run. Because the **date** command was completed before **find** was run, the **find** command became job 2.

To move a background job to the foreground, use the **fg** builtin followed by the job number. Alternatively, you can give a percent sign (%) followed by the job number as a command. Either of the following commands moves job 2 to the foreground. When you move a job to the foreground, the shell displays the command it is now executing in the foreground.

```
$ fg 2
find /usr -name ace -print > findout
or
$ %2
find /usr -name ace -print > findout
```

You can also refer to a job by following the percent sign with a string that uniquely identifies the beginning of the command line used to start the job. Instead of the preceding command, you could have used either **fg %find** or **fg %f** because both uniquely identify job 2. If you follow the percent sign with a question mark and a string, the string can match any part of the command line. In the preceding example, **fg %?ace** also brings job 2 to the foreground.

Often the job you wish to bring to the foreground is the only job running in the background or is the job that **jobs** lists with a plus (+). In these cases **fg** without an argument brings the job to the foreground.

### Suspending a Job

Pressing the suspend key (usually CONTROL-Z) immediately suspends (temporarily stops) the job in the foreground and displays a message that includes the word **Stopped**.

```
CONTROL-Z
[2]+ Stopped               find /usr -name ace -print > findout
```

For more information refer to “Moving a Job from the Foreground to the Background” on page 255.

### bg: Sends a Job to the Background

To move the foreground job to the background, you must first suspend the job (above). You can then use the **bg** builtin to resume execution of the job in the background.

```
$ bg
[2]+ find /usr -name ace -print > findout &
```

If a background job attempts to read from the terminal, the shell stops the program and displays a message saying the job has been stopped. You must then move the job to the foreground so it can read from the terminal.

```
$ (sleep 5; cat > mytext) &
[1] 1343
$ date
Tue Dec 7 11:58:20 PST 2010
[1]+ Stopped                     ( sleep 5; cat >mytext )
$ fg
( sleep 5; cat >mytext )
Remember to let the cat out!
CONTROL-D
$
```

In the preceding example, the shell displays the job number and PID number of the background job as soon as it starts, followed by a prompt. Demonstrating that you can give a command at this point, the user gives the command *date* and its output appears on the screen. The shell waits until just before it issues a prompt (after *date* has finished) to notify you that job 1 is stopped. When you give an *fg* command, the shell puts the job in the foreground and you can enter the data the command is waiting for. In this case the input needs to be terminated with CONTROL-D, which sends an EOF (end of file) signal to the shell. The shell then displays another prompt.

The shell keeps you informed about changes in the status of a job, notifying you when a background job starts, completes, or stops, perhaps because it is waiting for input from the terminal. The shell also lets you know when a foreground job is suspended. Because notices about a job being run in the background can disrupt your work, the shell delays displaying these notices until just before it displays a prompt. You can set *notify* (page 355) to cause the shell to display these notices without delay.
