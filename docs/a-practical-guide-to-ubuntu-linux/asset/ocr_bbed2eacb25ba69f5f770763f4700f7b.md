The first trap in addbanner causes it to exit with a status of 1 when it receives a hangup, software interrupt (terminal interrupt or quit signal), or software termination. The second trap uses a 0 in place of signal-number, which causes trap to execute its command whenever the script exits because it reaches an exit or its end. These traps remove a temporary file whether the script terminates normally or prematurely. Standard error of the second trap is sent to /dev/null when trap attempts to remove a nonexistent temporary file. In those cases rm sends an error message to standard error; because standard error is redirected, the user does not see the message.

See page 975 for another example that uses trap.

# kill: ABORTS PROCESS

The kill builtin sends a signal to a process or job. The kill command has the following syntax:

```
kill [-signal] PID
```

where signal is the signal name or number (for example, INT or 2) and PID is the process identification number of the process that is to receive the signal. You can specify a job number (예 2.4) as %n in PID. If you omit kill, kill sends a TERM (software termination, number 15) signal. For more information on signal names and numbers, see Table 27-5 on page 1009.

The following command sends the TERM signal to job number 1, regardless of whether it is in the foreground (running) or in the background (running or stopped):

```
$ kill %1
```

Because TERM is the default signal for kill, you can also give this command as kill %1. Give the command kill -l (lowercase "-L") to display a list of signal names.

A program that is interrupted can leave matters in an unpredictable state: Temporary files may be left behind (when they are normally removed), and permissions may be changed. A well-written application traps, detects signals, and cleans up before exiting. Most carefully written applications trap the INT, QUIT, and TERM signals.

To terminate a program, first TRY (press CTRL-C), if the job is running in the foreground. Because an application can be written to ignore these signals, you may need to use the KILL signal, which cannot be trapped or ignored; it is a "sure kill.
For more information refer to "kill: Sends a Signal to a Process" on page 455.

# getopts: PARSES OPTIONS

The getopts builtin parses command-line arguments, making it easier to write programs that follow the Linux argument conventions. The syntax for getopts is

```
getopts optstring varname [arg]
```

where optstring is a list of the valid option letters, varname is the variable that receives the options one at a time, and arg is the optional list of parameters to be processed. If arg is not present, getopts processes the command-line arguments. If optstring starts with a colon (:), the script must take care of generating error messages; otherwise, getopts generates error messages.