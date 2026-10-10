prepare the script for the consequences of the signal.

# ## Generating signals

The Bash shell allows you to generate two basic Linux signals using key combinations on the keyboard. This feature comes in handy if you need to stop or pause a runaway script.

# ### Interrupting a process

The Ctrl+C key combination generates a $SIGINT$ signal and sends it to any processes currently running in the shell. You can test this by running a command that normally takes a long time to finish and pressing the Ctrl+C key combination:

```
```
$ sleep 60
^C
$```

```

The $sleep$ command pauses the shell's operation for the specified number of seconds and returns the shell prompt. The Ctrl+C key combination sends a $SIGINT$ signal, which simply stops the current process running in the shell. By pressing the Ctrl+C key combination before the time passed (60 seconds), you permanently terminated the $sleep$ command.

# ### Pausing a process

Instead of terminating a process, you can pause it in the middle of whatever it's doing. Sometimes, this can be a dangerous thing (for example, if a script has a file lock open on a crucial system file), but often it allows you to peek inside what a script is doing without actually terminating the process.

The Ctrl+Z key combination generates a $SIGTSTP$ signal, stopping any processes running in the shell. Stopping a process is different than terminating the process. Stopping the process leaves the program in memory and able to continue running from where it left off. In the “Controlling the Job” section later in this chapter, you learn how to restart a process that's been stopped.

When you use the Ctrl+Z key combination, the shell informs you that