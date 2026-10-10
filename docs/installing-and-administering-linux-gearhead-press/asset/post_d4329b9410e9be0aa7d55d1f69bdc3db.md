
`$ bash<Enter>`

Now, we check the PID of the new bash subshell:

```
$ echo $$<Enter>
395
```

The system tells us that the subshell has a PID of 395. And now, the moment of truth: We ask what the value of the user-defined variable x is.

```
$ echo $x<Enter>
4
```

The value of x has indeed been inherited by this child process. Now, at this subshell process level, we change the value of x to 400.

```
$ x=400<Enter>
```

As a check, we request the value of x.

```
$ echo $x<Enter>
400
```

As expected, the value of x in this subshell is now 400. We now leave the bash subshell and return to the parent bash shell.

```
$ <Ctrl>-d
```

We check to see whether we have indeed left the subshell by requesting the PID of this shell.

```
$ echo $$<Enter>
340
```

This situation is no surprise. We are back in the parent bash shell. Now, we request the value of x to see whether the 400 has been inherited upward to the parent process.

```
$ echo $x<Enter>
4
```

No, the value of x in the parent process is still 4. Thus, variable values are inherited from parent to child but not vice versa.

> NOTE The `export` command (alone) and the `env` command show all inherited variables. Use `set` to show all shell variables.

To paraphrase Example 12.6, the value of x was set to 4 in the login shell and then exported to the terminal environment. Another bash subshell was then created. The inherited value of x was, as predicted, 4 here, too. Then, we changed the value of x from 4 to 400 in the bash subshell to see whether it would affect the value of x in the parent login shell. Then, we exited to the login shell and checked the value of x. We discovered that despite the fact that we changed x from 4 to 400 in a subshell, the value of x remained unchanged in the login shell (it was still 4). In other words, then, changing the value of a variable in a subshell does not affect the parent process.

Assume that you are still in the bash subshell and have just changed the value of x from 4 to 400. If you open another subshell within this subshell, will the value of x be 4 or 400? The answer is 400. The child process inherits the parent process value in this case. After a variable has been exported, it does not have to be exported again. If you continued to open subshells within these subshells, the value of x would remain 400 until you saw fit to change it.

If you exit from the string of subshells back to the login shell and then open subshells below the login shell, the value of x would return to and remain at 4. Changes made by a child process to an exported variable are available only to subsequent child processes. The variable value is not inherited back up to the login shell or down any other process.

## Return Codes from Commands

After a command has attempted or completed execution, it sends a *return code* (also known as an *exit code*) to its parent process. Note that a return code is a return message from a command, *not* from each individual process within the command. Also, please note that piped commands (discussed in Chapter 7, “Shell Basics”) send only one return code to their parent.

The return code is stored in the parent process environment as a value for the built-in question mark (?) variable, as shown in Example 12.7. Successful completion of a command returns a value of 0; unsuccessful completion returns a value ranging from 1 to 255.

How do you find the return code to a command? After sending the command for execution, type

```bash
$ echo $?
```

### Example 12.7 Using $ to Find a Command’s Return Code

```
$ date

Fri Mar 19 12:05:39 CST 1999

$ echo $?

0
```

> **NOTE** If you are contemplating using this method by default, be aware that after settings are made in the current shell (you are usually in the login shell), the only way of returning to the original default settings is to log out and log back in again.

## Process Monitoring: The ps Command

Users (occasionally) and system administrators (more frequently) have to check how their Linux processes are running. The ps (process status) command is commonly used to see how many processes are running, whether a specific process is running or has gotten hung up, and how many resources the various processes are using. In addition, the command checks priorities, who is doing what, and so on. A frequent use of the ps command is to monitor background jobs and other processes that do not regularly communicate with your terminal. The syntax is as follows:

```bash
$ ps (-options)
```

Earlier in this chapter, we briefly introduced you to the ps command when we illustrated parent-child process relationships. At that time, the ps command, with its a, u, x, and f options, showed us which processes were running, who they belonged to, and which processes were children of other processes.

The default ps listing, illustrated in Example 12.8, displays only minimum information about the processes started from your terminal. These processes are described in Table 12.4. On a system that has more than one terminal, the TTY field indicates which terminal initiated the process.

**Table 12.4 Response to the ps Command**

| FIELD | DESCRIPTION |
| :--- | :--- |
| PID | Process identification number assigned by the kernel |
| TTY | Terminal where the process originated |
| STAT | Current status of the process (for example, S = Asleep, R = Runnable) |
| TIME | Cumulative execution time for the process (min : sec) |
| COMMAND | Name of the process being executed |

**Example 12.8 Monitoring Processes with ps**

```
$ ps<Enter>  
PID TTY STAT TIME COMMAND  
340 1 S 0:00 -bash  
356 1 S 0:00 bash  
363 1 S 0:00 1s -R /  
364 1 S 0:00 ps
```

The ps command options are fully detailed in the man pages and in other information sources. A few options are explained in Table 12.5.

**Table 12.5 Some ps Command Options**

| OPTIONS | DESCRIPTION |
| :--- | :--- |
| e | Environment of the process |
| f | Processes and subprocesses spawned from the parent processes |
| 1 | Long listing (along with basic ps flags, including PLAGS, UID, PPID, PRI, NI, SIZE, RSS, WCCHAN) |
| j | Jobs format (along with basic ps flags, including UID, PPID, PGID, SID, TPGID) |
| a | Other users' processes, too |
| u | User's name and start time |
| x | Processes without an associated terminal |

## Invoking Foreground and Background Processes

Typically—and so far in this book—you invoke processes interactively from the command line. You can also invoke processes from the foreground and background states, however.

Processes that are started and require interaction from the terminal are called *foreground processes*. They are invoked in the foreground when you are fairly sure that they will finish in a short time or when you have to interact with them before and during execution. The processes themselves take over the terminal while they run. As we have seen before, the syntax for a foreground process is

```
$ command [-] options arguments<&Enter>
```

Processes that run independently from the initiating terminal are called *background processes*. You run processes in the background when, for example, you want to use your terminal for other tasks. But they are most useful for executing commands (or scripts or batch files containing numerous commands) that will take a long time to run, regardless of whether or not you are using your terminal. The syntax for a background process, then, is

```
$ command [-] options arguments / > backfile &<Enter>
```

> **NOTE** A process can be run in the background only if it does not require keyboard input and only if you observe the invocation syntax—the ampersand (&) at the end of the command line.

## Terminating Processes

You might want to terminate a foreground or background process for several reasons:

- You no longer need the program or process, and there is no other way to stop it.
- You are not getting the results you expected.
- You are not getting any results and your system seems “frozen.”
