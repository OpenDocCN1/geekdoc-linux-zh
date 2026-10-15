
Of course, no one wants to keep typing --preserve-root each time they run rm, so you should add this line to the .bashrc file in your home directory:

```
alias rm='rm --preserve-root'
```

That alias automatically adds --preserve-root to all calls to rm in future Bash sessions.

## Printing the Last Lines of a File with tail

If you want to watch a log file as it is written to, or want to monitor a user's actions as they are occurring, you need to be able to track log files as they change. In these situations you need the tail command, which prints the last few lines of a file and updates as new lines are added. This command tells tail to print the last few lines of /var/log/httpd/access_log, the Apache hit log:

```
tail /var/log/httpd/access_log
```

To get tail to remain running and update as the file changes, add the -f parameter (follow):

```
tail -f /var/log/httpd/access_log
```

You can tie the lifespan of a tail follow to the existence of a process by specifying the --pid parameter. When you do this, tail continues to follow the file you asked for until it sees that the process identified by PID is no longer running, at which point it stops tailing.

If you specify multiple files on the command line, tail follows both, printing file headers whenever the input source changes. Press Ctrl+C to terminate tail when in follow mode.

## Printing Resource Usage with top

The top command is unusual in this list because the few parameters it takes are rarely, if ever, used. Instead, it has a number of commands you can use while it is running to customize the information it shows you. To get the most from these instructions, open two terminal windows. In the first, run the program yes and leave it running; in the second run sudo top.

- PR—Priority
- NI—Niceness
- Virt—Virtual image size in kilobytes
- Res—Resident size in kilobytes
- Shr—Shared memory size in kilobytes
- S—Status
- %CPU—CPU usage
- %Mem—Memory usage
- Time+—CPU time
- Command—The command being run

Several of them are unimportant unless you have a specific problem. The ones we are interested in are PID, User, Niceness, %CPU, %MEM, Time+, and Command. The Niceness of a process is how much time the CPU allocates to it compared to everything else on the system: 19 is the lowest, and −19 is the highest.

With the columns explained, you should be able to find the process ID of the errant yes command launched earlier; it is usually the first number below PID. Now type k, enter that process ID, and press Enter. You are prompted for a signal number (the manner in which you want the process killed), with 15 provided as the default. Signal 15 (also known as SIGTERM, for "terminate") is a polite way of asking a process to shut down, and all processes that are not wildly out of control should respond to it. Give top a few seconds to update itself, and hopefully the yes command should be gone. If not, you need to be more forceful: type k again, enter the PID, and press Enter. When prompted for a signal to send, enter 9 and press Enter to send SIGKILL, or "terminate whether you like it or not."

You can choose the fields to display by pressing f. A new screen appears that lists all possible fields, along with the letter you need to press to toggle their visibility. Selected fields are marked with an asterisk and have their letter, for example:

```
* A: PID      = Process Id
```

If you press the a key, the screen changes to this:

```
a: PID      = Process Id
```

When you have made your selections, press Enter to return to the normal top view with your normal column selection.

You can also press F to select the field you want to use for sorting. This works in the same way as the field selection screen, except that you can select only one field at a time.

Again, press Enter to get back to top after you have made your selection, and it will be updated with the new sorting.

If you press B, text bolding is enabled. By default, this bolds some of the header bar as well as any programs that are currently running (as opposed to sleeping), but if you press x you can also enable bolding of the sorted column. You can use y to toggle bolding of running processes.

The last command to try is r, which allows you to renice—or adjust the nice value—of a process. You need to enter the PID of the process, press Enter, and enter a new nice value. Keep in mind that 19 is the lowest and −20 is the highest; anything less than 0 is considered “high” and should be used sparingly.

## Printing the Location of a Command with which

The purpose of which is to tell you the exact command that would be executed if you typed it. For example, which mkdir returns /bin/mkdir, telling you that running the command mkdir runs /bin/mkdir.

## Combining Commands Together

So far, we have only been using commands individually, and for the large part that is what you will be doing in practice. However, some of the real power of these commands lies in the ability to join them together to get exactly what you want. There are some extra little commands that we have not looked at that are often used as glue because they do one very simple thing that enables a more complex process to work.

All the commands we have looked at have printed their information to the screen, but this is often flexible. There are two ways to control where output should go: piping and output redirection. A pipe is a connector between one command’s output and another’s input. Instead of sending its output to your terminal, a command sends that output directly to another command for input. Output redirection works in a similar way to pipes but is usually used for files. We will look at pipes first and then output redirection.

Two of the commands we have looked at so far are ps and grep: the process lister and the string matcher. We can combine the two to find out which users are playing Nethack right now:

```
ps aux | grep nethack
```

That creates a list of all the processes running right now and sends that list to the grep command, which filters out all lines that do not contain the word nethack. Ubuntu allows you to pipe as many commands as you can sanely string together. For example, we could add in the wc command, which counts the numbers of lines, words, and characters in its input, to count precisely how many times Nethack is being run:

```
ps aux | grep nethack | wc -l
```
