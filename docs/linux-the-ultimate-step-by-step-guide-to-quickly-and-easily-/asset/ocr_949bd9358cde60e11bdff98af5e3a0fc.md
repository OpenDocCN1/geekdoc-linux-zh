command prompt returned. This may not always be desirable. For instance, you may end up leaving a bunch of temporary files that will not get cleaned up.

Trapping these signals is quite easy, the trap command has the following syntax –

```
$ trap commands signals
```

Here command can be any valid Unix command, or even a user-defined function, and signal can be a list of any number of signals you want to trap.

There are three common uses for trap in shell scripts –

+   - Clean up temporary files

+   - Ignore signals

# Cleaning Up Temporary Files

As an example of the trap command, the following shows how you can remove files and then exit if someone tries to abort the program from the terminal –

```
$ trap "rm -f $WORKDIR/work1$$ $WORKDIR/dataout$$; exit" 2
```

From the point in the shell program that this trap is executed, the two files work1$$ and dataout$$ will be automatically removed if signal number 2 is received by the program. Therefore, if the user interrupts execution of the program after this trap is executed, you can be assured that these two files will be cleaned up. The exit command that follows the rm is necessary because without it execution would continue in the program at the point that it left off when the signal was received.

Signal number 1 is generated for hangup: Either someone intentionally hangs up the line or the line gets accidentally disconnected. You can modify the preceding trap to also remove the two specified files in this case by adding signal number 1 to the list of signals –$ trap "rm $WORKDIR/work1$$ $WORKDIR/dataout$$; exit" 1 2. Now these files will be removed if the line gets hung up or if the Ctrl+C key gets pressed. The commands specified to trap must be enclosed in quotes if they contain more than one command. Also, note that the shell scans the command line at the time that the trap command gets executed and also when one of the listed signals is received.

So in the preceding example, the value of WORKDIR and $$ will be substituted at the time that the trap command is executed. If you wanted this substitution to occur at the time that either signal 1 or 2 was received you can put the commands