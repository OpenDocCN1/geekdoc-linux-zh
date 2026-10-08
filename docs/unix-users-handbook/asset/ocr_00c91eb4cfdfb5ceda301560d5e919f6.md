-V Set the verbose variable before .cshrc is executed so that all .cshrc commands are also echoed to the standard output.

-X Set the echo variable before .cshrc is executed so that all .cshrc commands are also echoed to the standard output.

After processing the command options, if arguments remain in the argument list, and the -C, -I, -S, or -t options were not specified, the first remaining argument is taken as the name of a file of commands to be executed.

# COMMANDS

A simple command is a sequence of words, the first of which specifies the command to be executed. A sequence of simple commands separated by vertical bar (|) characters forms a pipeline. The output of each command in a pipeline becomes the input for the next command in the pipeline. Sequences of pipelines can be separated by semicolons (;) which causes them to be executed sequentially. A sequence of pipelines can be executed in background mode by adding an ampersand character (&) after the last entry.

Any pipeline can be placed in parentheses to form a simple command which, in turn, can be a component of another pipeline. Pipelines can also be separated by || or && indicating, as in the C language, that the second pipeline is to be executed only if the first fails or succeeds, respectively.

# Jobs

csh associates a job with each pipeline and keeps a table of current jobs (printed by the jobs command) and assigns them small integer numbers. When a job is started asynchronously using &, the shell prints a line resembling:

```
(1) 1234
```

indicating that the job which was started asynchronously was job number 1 and had one (top-level) process, whose process id was 1234.

If you are running a job and want to do something else, you can type the currently defined suspend character (see termio(7)) which sends a stop signal to the current job. csh then normally indicates that the job has been Stopped, and prints another prompt. You can then manipulate the state of this job, putting it in the background with the bg command, run some other commands, and then eventually bring the job back into the foreground with the foreground command fg. A suspend takes effect immediately and is like an interrupt in that pending output and unread input are discarded when it is typed. There is a delayed suspend character which does not generate a stop signal until a program attempts to read(2) it. This can usefully be typed ahead when you have prepared some commands for a job which you want to stop after it has read them.

A job being run in the background stops if it tries to read from the terminal. Background jobs are normally allowed to produce output, but this can be disabled by giving the command stty tostop (see tty(1)). If you set this TTY option, background jobs stop when they try to produce output, just as they do when they try to read input. Keyboard signals and line-hangup signals from the terminal interface are not sent to background jobs on such systems. This means that background jobs are immune to the effects of logging out or typing the interrupt, quit, suspend, and delayed suspend characters (see termio(7)).

There are several ways to refer to jobs in the shell. The character % introduces a job name. If you wish to refer to job number 1, you can