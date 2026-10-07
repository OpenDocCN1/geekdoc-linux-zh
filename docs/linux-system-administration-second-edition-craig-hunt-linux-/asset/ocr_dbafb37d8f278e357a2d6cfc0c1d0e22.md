# **Redirection**

*Redirection* is the practice of changing where the stream comes from or is written to. One common use is to route the system log to a vacant console and update it as messages are added. You do this by listing the tail command followed by an output redirection character ( > ) and then the device where the output is to be sent. If you wanted the output of the command to go to the console device designated by /dev/tty9 rather than to stdout, you would enter this:

```
# tail -f /var/log/messages > /dev/tty9
```

When you execute this command, the output of the tail command will be redirected to console 9, causing the system log (/var/log/messages) to be displayed there and, since the -f argument is present, appending new output as it is written to the system log.

Sometimes you want to take input from somewhere other than stdin. This is also redirection, and you can use the same principle illustrated above. Simply follow the command that requires input with the input redirection character ( < ) and the file that contains the data to be input. Let's say that a file contains a list of names to be sorted in a particular order. By changing the stdin for the sort command, we can make it take the names from the file, reorder them, and write them to stdout. The command would look like this:

```
# sort < namelist
```

You can use the two redirection operators in the same command sequence when you need to take stdin from one file and send stdout to another. A common use of this is to sort the lines in a file and output the sorted lines into a new file. With redirection it would look like this:

```
# sort < namelist > sortedlist
```

Another common use of redirection is to send both stdout and stderr to a file in order to save the data for examination. This is a very useful tool for tracking down a problem. This can be done for any two I/O streams and not just stdout and stderr. You need to know that standard input is considered the first stream and numbered 0; standard output numbered 1, and standard error is numbered 2, since the numeric representation is used in redirection. Using stdout and stderr, the command would look like this:

```
# backup > backup.log 2>&1
```

**Note** The 2>&1 means to route stderr (2) wherever stdin (1) goes. The ampersand (&) often relates to memory location or addresses. Redirection as above causes backup.log to write over any file previously known as backup.log. If you want to append the output from a command to backup.log instead of writing over it, you'd use the >> symbol. This is especially good for log keeping. The command would look like this:

```
# backup >> backup.log 2>&1
```

# **Wildcards**

Bash, like most other Unix shells, allows the use of special characters called *wildcards* to reference more than one file at a time. DOS and Windows, of course, also offer wildcards, but the difference is that in Linux, these special characters are expanded by the Bash shell and not by the program itself. That is, if you launch a program that has special characters in its argument string, the program does not need to know how to handle them; they are translated by the Bash shell before being passed to