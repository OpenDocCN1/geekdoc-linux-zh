# # Sending Signals

As discussed in Chapter 21, “Optimizing Performance,” the Bash shell can send signals to processes running on the system. This allows you to stop or interrupt a runaway application process if necessary. While the `kill` and `pkill` commands discussed in Chapter 21 are good for stopping background processes, applications running in the foreground on the console are harder to control. Fortunately, there are two basic Linux signals you can generate using key combinations on the keyboard to interrupt or stop a foreground process.

# ## Interrupting a Process

The `Ctrl+C` key combination generates a signal interrupt (SIGINT) signal and sends it to any processes currently running in the shell. You can test this by running a command that normally takes a long time to finish and pressing the `Ctrl+C` key combination:

```
$ sleep 100

$

```

The `Ctrl+C` key combination doesn’t produce any output on the monitor; it just stops the current process running in the shell.

# ## Pausing a Process

Instead of terminating a process, you can pause it in the middle of whatever it’s doing. Sometimes this can be a dangerous thing (for example, if a script has a file lock open on a crucial system file), but often it allows you to peek inside what a script is doing without actually terminating the process.

The `Ctrl+Z` key combination generates a signal terminal stop (SIGTSTP) signal, stopping any processes running in the shell. Stopping a process is different than terminating the process, as stopping the process leaves the program still in memory and able to continue running from where it left off. In the following section, “Job Control,” you’ll learn how to restart a process that’s been stopped.

When you use the `Ctrl+Z` key combination, the shell informs you that the process has been stopped:

```
$ sleep 100
[1]+ Stopped sleep 100
$

```