
## 9.6.2 The Suspend Key Sequence and Background Jobs

To suspend a program, the suspend key sequence, Ctrl-Z, is issued. The job is now suspended (stopped), the shell prompt is displayed, and the program will not resume until the fg or bg commands is issued. (When using the vi editor, the ZZ command writes and saves a file. Do not confuse this with Ctrl-Z, which would suspend the vi session.) If you try to log out when a job is suspended, the message There are stopped jobs appears on the screen.

## 9.6.3 The jobs Command

The C/TC shell jobs built-in command displays the programs that are currently active and either running or suspended in the background. Running means the job is executing in the background. When a job is stopped, it is suspended; it is not in execution. In both cases, the terminal is free to accept other commands.

### EXAMPLE 9.26

```
(The Command Line)
1
% jobs
2
[1] + Stopped      vi filex
[2] - Running      sleep 25

3
% jobs -l
[1] + 355 Stopped  vi filex
[2] - 356 Running  sleep 25

4
[2] Done sleep 25
```

### EXPLANATION

- 1 The jobs command lists the currently active jobs.
- 2 The notation [1] is the number of the first job; the plus sign indicates that the job is not the most recent job to be placed in the background; the dash indicates that this is the most recent job put in the background; Stopped means that this job was suspended with ^Z and is not currently active.
- 3 The -l option (long listing) displays the number of the job as well as the PID of the job. The notation [2] is the number of the second job, in this case, the last job placed in the background. The dash indicates that this is the most recent job. The sleep command is running in the background.
- 4 After sleep has been running for 25 seconds, the job will complete and a message saying that it has finished appears on the screen.

## 9.6.4 The Foreground and Background Commands

The fg command brings a background job into the foreground. The bg command starts a suspended job running in the background. A percent sign and the number of a job can be used as arguments to the fg and bg commands if you want to select a particular job for job control.

### EXAMPLE 9.27

```
1  % jobs
   [1] + Stopped    vi file
   [2] - Running    cc prog.c -o prog

3  % fg %1
   vi file
   (vi session starts)

4  % kill %2
   [2] Terminated  cc prog.c -o prog

5  % sleep 15
   (Press ^Z)
   Stopped

6  % bg
   [1] sleep 15 &
   [1] Done       sleep 15
```

### EXPLANATION

- 1. The jobs command lists currently running processes, called jobs.
- 2. The first job stopped is the vi session, the second job is the cc command.
- 3. The job numbered [1] is brought to the foreground. The number is preceded with a percent sign.
- 4. The kill command is built-in. It sends the TERM (terminate) signal, by default, to a process. The argument is either the number or the PID of the process.
- 5. The sleep command is stopped by pressing ^Z. The sleep command is not using the CPU and is suspended in the background.
- 6. The bg command causes the last background job to start executing in the background. The sleep program will start the countdown in seconds before execution resumes.

## 9.7 Shell Metacharacters

Metacharacters are special characters that are used to represent something other than themselves. As a rule of thumb, characters that are neither letters nor numbers may be metacharacters. Like grep, sed, and awk, the shell has its own set of metacharacters, often called shell wildcards. Shell metacharacters can be used to group commands together, to abbreviate filenames and pathnames, to redirect and pipe input/output, to place commands in the background, and so forth. Table 9.3 presents a partial list of shell metacharacters.

### Table 9.3 Shell Metacharacters

| Metacharacter | Purpose | Example | Meaning |
|---|---|---|---|
| $ | Variable substitution | set name=Tom echo $name Tom | Sets the variable name to Tom; displays the value stored there. |
| ! | History substitution | !3 | Re-executes the third event from the history list. |
| * | Filename substitution | rm * | Removes all files. |
| ? | Filename substitution | ls ?? | Lists all two-character files. |
| [ ] | Filename substitution | cat f[123] | Displays contents of f1, f2, f3. |
| ; | Command separator | ls;date;pwd | Each command is executed in turn. |
| & | Background processing | lp nbox& | Printing is done in the background. Prompt returns immediately. |
| > | Redirection of output | ls > file | Redirects standard output to file. |
| < | Redirection of input | ls < file | Redirects standard input from file. |
| >& | Redirection of output and error | ls >& file | Redirects both output and errors to file. |
| >! | If noclobber is set, override it | ls >! file | If file exists, truncate and overwrite it, even if noclobber is set. |
| >>! | If noclobber is set, override it | ls >>! file | If file does not exist, create it; even if noclobber is set. |

> 4. Programs such as grep, sed, and awk have a set of metacharacters, called regular expression metacharacters, for pattern matching. These should not be confused with shell metacharacters.
