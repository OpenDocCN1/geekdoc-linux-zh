```
```
$ kill KILL_PID<Enter>
```
```

> **NOTE** The number assigned to a signal by Linux/UNIX has no bearing on its strength or priority. In other words, a higher or lower number does not indicate potency.

> **WARNING** Sometimes when a process is killed—especially if it has been terminated with a *kill -9*—a child process might be terminated. But the parent process, although notified of the child’s termination, does not acknowledge the termination. The now-dead child process becomes what is called a *zombie* and will appear as *default* under the **COMMAND** column when you issue a *ps* command. You might or might not be able to *kill* a zombie; it will continue to be listed in the **COMMAND** column because it holds onto a process slot (that is, a record in the process table) until its parent process acknowledges its termination. A few zombies do not present a major problem, but if the *ps* table begins to fill up with them, your ability to execute legitimate processes declines. Zombies can be eliminated by a system reboot or occasionally by a *cleanup* initiated by the *init* process.

# Running Long Processes: The nohup Command

The nohup (no hang-up) command tells a background command or process to ignore kill signals 1 (hang-up) and 3 (quit). This command enables the background process to continue executing after the owner logs out of the system. The nohup command itself takes over control of the command. The syntax is as follows:

```
```
$ nohup command -option argument > filename <Enter>
```
```

Because the nohup command is designed to shepherd a process *after* the user/owner has logged out, output from the command cannot go to the terminal screen. Therefore, the user/owner should redirect the output to a destination of his or her choice. If the user/owner does not redirect output, nohup automatically redirects the output to the *nohup.out* file in the directory in which the nohup command was originally invoked. See Example 12.11 for both types of redirection.