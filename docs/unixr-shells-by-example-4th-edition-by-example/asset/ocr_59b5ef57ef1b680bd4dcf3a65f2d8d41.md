# EXAMPLE 13.27 (CONTINUED)

```
7  $ jobs -x echo %1
4537

8  $ kill %1    # or kill 4537
[1]+  Stopped      vi
Vim: Caught deadly signal TERM
Vim: Finished.
[1]+  Exit 1      vi
```

# EXPLANATION

1 After the vi editor is invoked, you can press ^Z (Ctrl-Z) to suspend the vi session. The editor will be suspended in the background, and after the message Stopped appears, the shell prompt will appear immediately.

2 The ampersand at the end of the command causes the sleep command, with an argument of 25, to execute in the background. The notation [2] means that this is the second job to be run in the background and the PID of this job is 4538.

3 The jobs command displays the jobs currently in the background.

4 The jobs command with the -l option displays the processes (jobs) running in the background and the PID numbers of those jobs.

5 The %% argument causes jobs to display the most recent command put in the job table.

6 The fg command followed by a percent sign and the job number will bring that numbered job into the foreground. Without a number, fg brings the most recently backgrounded job back into the foreground.

7 The -x option can be used to print just the PID number of the job. %1 refers to the vi session that was stopped in the first example.

8 The kill command sends a TERM signal to the process and kills it. The vi program is killed. You can specify either the job number or the PID number as arguments to the kill command.

# Table 13.3 Job Control Commands

| Command | Meaning |
|---|---|
| bg | Starts running the stopped job in the background |
| fg | Brings a background job to the foreground |
| jobs | Lists all the jobs running |
| kill | Sends the kill signal to a specified job |
| stop | Suspends a background job |