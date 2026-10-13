
## Redirecting and Piping the Standard Error: >& , 2>

When you execute commands, an error could possibly occur. You may give the wrong number of arguments, or some kind of system error could take place. When an error occurs, the system issues an error message. Usually such error messages are displayed on the screen, along with the standard output. Linux distinguishes between standard output and error messages, however. Error messages are placed in yet another standard byte stream, called the standard error. In the next example, the cat command is given as its argument the name of a file that does not exist, myintro. In this case, the cat command simply issues an error:

```
$ cat myintro
cat: myintro not found
$
```

Because error messages are in a separate data stream from the standard output, error messages still appear on the screen for you to see even if you have redirected the standard output to a file. In the next example, the standard output of the cat command is redirected to the file mydata. However, the standard error, containing the error messages, is still directed to the screen.

```
$ cat myintro > mydata
cat: myintro not found
$
```

You can redirect the standard error, as you can the standard output. This means you can save your error messages in a file for future reference. This is helpful if you need a record of the error messages. Like the standard output, the standard error has the screen device for its default destination. However, you can redirect the standard error to any file or device you choose using special redirection operators. In this case, the error messages will not be displayed on the screen.

Redirection of the standard error relies on a special feature of shell redirection. You can reference all the standard byte streams in redirection operations with numbers. The numbers 0, 1, and 2 reference the standard input, standard output, and standard error, respectively. By default, an output redirection, >, operates on the standard output, 1. You can modify the output redirection to operate on the standard error, however, by preceding the output redirection operator with the number 2. In the next example, the cat command again will generate an error. The error message is redirected to the standard byte stream represented by the number 2, the standard error.

```
$ cat nodata 2> myerrors
$ cat myerrors
cat: nodata not found
$
```

You can also append the standard error to a file by using the number 2 and the redirection append operator, >>. In the next example, the user appends the standard error to the myerrors file, which then functions as a log of errors:

```
$ cat nodata 2>> myerrors
```

## Jobs: Background, Kills, and Interruptions

In Linux, you not only have control over a command's input and output, but also over its execution. You can run a job in the background while you execute other commands. You can also cancel commands before they have finished executing. You can even interrupt a command, starting it again later from where you left off. Background operations are particularly useful for long jobs. Instead of waiting at the terminal until a command has finished execution, you can place it in the background. You can then continue executing other Linux commands. You can, for example, edit a file while other files are printing. The background commands, as well as commands to cancel and interrupt jobs, are listed in Table 8-5.

Table 8-5: Job Management Operations

| Background Jobs | Execution |
|---|---|
| & | Execute a command in the background. |
| fg %jobnum | Bring a command in the background to the foreground or resume an interrupted program. |
| bg | Place a command in the foreground into the background. |
| CTRL-Z | Interrupt and stop the currently running program. The program remains stopped and waiting in the background for you to resume it. |
| notify %jobnum | Notify you when a job ends. |
| kill %jobnum
kill processnum | Cancel and end a job running in the background. |
| jobs | List all background jobs. The jobs command is not available in the Bourne shell, unless it is using the jsh shell. |
| ps | List all currently running processes, including background jobs. |
| at time date | Execute commands at a specified time and date. The time can be entered with hours and minutes and qualified as A.M. or P.M. |

### Running Jobs in the Background

You execute a command in the background by placing an ampersand on the command line at the end of the command. When you do so, a user job number and a system process number are displayed. The user job number, placed in brackets, is the number by which the user references the job. The system process number is the number by which the system identifies the job. In the next example, the command to print the file mydata is placed in the background:

```
$ lpr mydata &
[1]  534
$
```

You can place more than one command in the background. Each is classified as a job and given a name and a job number. The command jobs lists the jobs being run in the background. Each entry in the list consists of the job number in brackets, whether it is stopped or running, and the name of the job. The + sign indicates the job currently being processed, and the – sign indicates the next job to be executed. In the next example, two commands have been placed in the background. The jobs command then lists those jobs, showing which one is currently being executed.

```
$ lpr intro &
[1]  547
```

```
$ cat *.c > myprogs &
[2] 548
$ jobs
[1] + Running lpr intro
[2] - Running cat *.c > myprogs
$
```

### Job Notification

After you execute any command in Linux, the system tells you what background jobs, if you have any running, have been completed so far. The system does not interrupt any operation, such as editing, to notify you about a completed job. If you want to be notified immediately when a certain job ends, no matter what you are doing on the system, you can use the notify command to instruct the system to tell you. The notify command takes a job number as its argument. When that job is finished, the system interrupts what you are doing to notify you the job has ended. The next example tells the system to notify the user when job 2 has finished:

```
$ notify %2
```

### Bringing Jobs to the Foreground

You can bring a job out of the background with the foreground command, fg. If only one job is in the background, the fg command alone will bring it to the foreground. If more than one job is in the background, you must use the job's number with the command. You place the job number after the fg command, preceded with a percent sign. A bg command also places a job in the background. This command is usually used for interrupted jobs. In the next example, the second job is brought back into the foreground. You may not immediately receive a prompt again because the second command is now in the foreground and executing. When the command is finished executing, the prompt appears and you can execute another command.

```
$ fg %2
cat *.c > myprogs
$
```

### Stopping and Suspending Jobs

If you want to stop a job running in the background, you can force it to end with the kill command. The kill command takes as its argument either the user job number or the system process number. The user job number must be preceded by a percent sign, %. You can find out the job number from the jobs command. In the next example, the jobs command lists the background jobs; then job 2 is canceled:

```
$ jobs
[1] + Running lpr intro
[2] - Running cat *.c > myprogs
$ kill %2
```

You can also cancel a job using the system process number, which you can obtain with the ps command. The ps command displays a great deal more information than the jobs command does. The next example lists the processes a user is running. The PID is the system process number, also known as the process ID. TTY is the terminal identifier. The time is how long the process has taken so far. COMMAND is the name of the process.

```
$ ps
```

| PID | TTY | TIME | COMMAND |
| --- | --- | ---- | ------- |
| 523 | tty24 | 0:05 | sh |
| 567 | tty24 | 0:01 | lpr |
