> When you redirect output to a file using the output redirection operator, the shell overwrites the data in that file with the output of the command you specified. For example, the command $ date > now overwrites all the data in the file now with the output of the date command. For this reason, you should take extra care and make sure the file you specified does not contain important information.

# Appending to a File

Overwriting a file simply by redirecting output to it is often undesirable. Fortunately, the shell provides a second form of output redirection with the >> operator, which appends output to a file. The basic syntax is as follows:

```
and >> file
list >> file
```

In these forms, output is appended to the end of file. If the file does not exist it is created. For example, you can prevent the loss of data from the file mylog each time a date is added by using the following command:

```
{ date; uptime; who ; } >> mylog
```

If you view the contents of mylog, you find that it contains the output of both lists:

```
11:15am up 79 days, 14:48, 5 users, load average: 0.00, 0.00, 0.00
ranga tty1 Aug 28 14:12
ranga tty2 Aug 28 14:13
ranga tty0 Oct 27 19:42 (:0.0)
amma tty3 Oct 30 08:29 (localhost)
ranga tty4 Nov 14 11:13 (rishi.bosland.u)
Sat Nov 14 11:15:54 PST 1988
11:15am up 79 days, 14:48, 5 users, load average: 0.00, 0.00, 0.00
ranga tty1 Aug 28 14:12
ranga tty2 Aug 28 14:13
ranga tty0 Oct 27 19:42 (:0.0)
amma tty3 Oct 30 08:29 (localhost)
ranga tty4 Nov 14 11:13 (rishi.bosland.u)
```

# Redirecting Output to a File and the Screen

In certain instances, you need to direct the output of a script to a file and onto the terminal. An example of this is shell scripts that are required to produce a log file of their activities. For interactive scripts, the log file cannot just contain the script's output redirected to a file.