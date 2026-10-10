
Because redirecting the Standard Output to a file for later use is more common than redirecting the Standard Error to a file, the BASH shell assumes Standard Output in the absence of a numeric file descriptor:

```bash
[root@server1 ~]# ls /etc/hosts /etc/h >goodoutput
ls: cannot access /etc/h: No such file or directory
[root@server1 ~]# cat goodoutput
/etc/hosts
[root@server1 ~]# _
```

In addition, you can redirect both Standard Output and Standard Error to separate files at the same time, as shown in the following output:

```bash
[root@server1 ~]# ls /etc/hosts /etc/h >goodoutput 2>badoutput
[root@server1 ~]# cat goodoutput
/etc/hosts
[root@server1 ~]# cat badoutput
ls: cannot access /etc/h: No such file or directory
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_329_0.png)

> The order of redirection on the command line does not matter; the command `ls /etc/hosts /etc/h >goodoutput 2>badoutput` is the same as `ls /etc/hosts /etc/h 2>badoutput >goodoutput`

It is important to use separate filenames to hold the contents of Standard Output and Standard Error; using the same filename for both results in a loss of data because the system attempts to write both contents to the file at the same time:

```bash
[root@server1 ~]# ls /etc/hosts /etc/h >goodoutput 2>goodoutput
[root@server1 ~]# cat goodoutput
access /etc/h: No such file or directory
[root@server1 ~]# _
```

To redirect both Standard Output and Standard Error to the same file without any loss of data, you must use special notation. To specify that Standard Output be sent to the file goodoutput and Standard Error be sent to the same place as Standard Output, you can do the following:

```bash
[root@server1 ~]# ls /etc/hosts /etc/h >goodoutput 2>&1
[root@server1 ~]# cat goodoutput
ls: cannot access /etc/h: No such file or directory
/etc/hosts
[root@server1 ~]# _
```

Alternatively, you can specify that the Standard Error be sent to the file badoutput and Standard Output be sent to the same place as Standard Error:

```bash
[root@server1 ~]# ls /etc/hosts /etc/h 2>badoutput >&2
[root@server1 ~]# cat badoutput
ls: cannot access /etc/h: No such file or directory
/etc/hosts
[root@server1 ~]# _
```

In all of the examples used earlier, the contents of the files used to store the output from commands were cleared prior to use by the BASH shell. Another example of this is shown in the following output when redirecting the Standard Output of the date command to the file dateoutput:

```
[root@server1 ~]# cat dateoutput
[root@server1 ~]# cat dateoutput
Fri Aug 20 07:54:00 EDT 2015
[root@server1 ~]# date>dateoutput
[root@server1 ~]# cat dateoutput
Fri Aug 20 07:54:00 EDT 2015
[root@server1 ~]# cat dateoutput
```

To prevent the file from being cleared by the BASH shell and append output to the existing output, you can specify two > metacharacters alongside the file descriptor, as shown in the following output:

```
[root@server1 ~]# date>dateoutput
[root@server1 ~]# cat dateoutput
Fri Aug 20 07:54:32 EDT 2015
[root@server1 ~]# date>>dateoutput
[root@server1 ~]# cat dateoutput
Fri Aug 20 07:54:32 EDT 2015
Fri Aug 20 07:54:48 EDT 2015
[root@server1 ~]# cat dateoutput
```

You can also redirect a file to the Standard Input of a command using the < metacharacter. Because there is only one file descriptor for input, there is no need to specify the number 0 before the < metacharacter to indicate Standard Input, as shown next:

```
[root@server1 ~]# cat</etc/issue
Fedora release 20 (Heisenbug)
Kernel \r on an \m (\1)

[root@server1 ~]# cat
```

In the preceding output, the bash shell located and sent the /etc/issue file to the cat command as Standard Input. Because the cat command normally takes the filename to be displayed as an argument on the command line (e.g., cat /etc/issue), there is no need to use Standard Input redirection with the cat command as used in the previous example; however, some commands on the Linux system only accept files when they are passed by the shell through Standard Input. The tr command is one such command that can be used to replace characters in a file sent via Standard Input. To translate all of the lowercase r characters in the /etc/issue file to uppercase R characters, you can run the following command:

The preceding command does not modify the /etc/issue file; it simply takes a copy of the /etc/issue file, manipulates it, and then sends the Standard Output to the terminal screen. To save a copy of the Standard Output for later use, you can use both Standard Input and Standard Output redirection together:

```
[root@server1 ~]# tr r R < /etc/issue > newissue
[root@server1 ~]# cat newissue
Fedora Release 20 (Heisenbug)
Kernel \r on an \m (\l)
[root@server1 ~]# _
```

As with redirecting Standard Output and Standard Error in the same command, you should use different filenames when redirecting Standard Input and Standard Output. However, this is because the BASH shell clears a file that already exists before performing the redirection. An example of this is shown in the following output:

```
[root@server1 ~]# sort < newissue > newissue
[root@server1 ~]# cat newissue
[root@server1 ~]# _
```

The newissue file has no contents when displayed in the preceding output. This is because the BASH shell saw that output redirection was indicated on the command line, it cleared the contents of the file newissue, then sorted the blank file and saved the output (nothing in our example) into the file newissue. Because of this feature of shell redirection, Linux administrators commonly use the command > filename at the command prompt to clear the contents of a file.

The contents of log files are typically cleared periodically using the command > /path/to/logfile.

![](img/c27875544958897d817484d558c208c8_331_0.png)

Table 7-1 summarizes the different types of redirection discussed in this section.

## Pipes

Note from Table 7-1 that redirection only occurs between a command and a file and vice versa. However, you can send the Standard Output of one command to another command as Standard Input. To do this, you use the pipe | shell metacharacter and specify commands on either side. The shell then sends the Standard Output of the command on the left to the command on the right, which then interprets the information as Standard Input. This process is depicted in Figure 7-2.

![](img/c27875544958897d817484d558c208c8_331_1.png)

Figure 7-2 Piping information from one command to another

| Command | Description |
| --- | --- |
| `command 1>file`<br>`command >file` | The *Standard Output* of the command is sent to a file instead of to the terminal screen. |
| `command 2>file` | The *Standard Error* of the command is sent to a file instead of to the terminal screen. |
| `command 1>fileA 2>fileB`<br>`command >fileA 2>fileB` | The *Standard Output* of the command is sent to fileA instead of to the terminal screen, and the *Standard Error* of the command is sent to fileB instead of to the terminal screen. |
| `command 1>file 2>&1`<br>`command >file 2>&1`<br>`command 1>&2 2>file`<br>`command >&2 2>file` | Both the *Standard Output* and the *Standard Error* are sent to the same file instead of to the terminal screen. |
| `command 1>>file`<br>`command >>file` | The *Standard Output* of the command is appended to a file instead of being sent to the terminal screen. |
| `command 2>>file` | The *Standard Error* of the command is appended to a file instead of being sent to the terminal screen. |
| `command 0<file`<br>`command <file` | The *Standard Input* of a command is taken from a file. |

Table 7-1 Common redirection examples

![](img/c27875544958897d817484d558c208c8_332_0.png)

A series of commands that includes the pipe `|` metacharacter is commonly referred to as a **pipe**.

![](img/c27875544958897d817484d558c208c8_332_1.png)

The pipe symbol can be created on most keyboards by pressing Shift+\|.

For example, the *Standard Output* of the `ls -l /etc` command is too large to fit on one terminal screen. To send the *Standard Output* of this command to the `less` command, which views *Standard Input* page-by-page, you could use the following command:

```
[root@server1 ~]# ls -l /etc | less
total 1836
drwxr-xr-x 3 root root 4096 Dec 11 2013 abrt
-rw-r--r- 1 root root 16 Sep 16 21:54 adjtime
drwxr-xr-x 2 root root 4096 Sep 17 19:44 akonadi
-rw-r-r-- 1 root root 1518 Jun 7 2013 aliases
drwxr-xr-x 2 root root 4096 Dec 11 2013 alsa
drwxr-xr-x 2 root root 4096 Sep 24 10:06 alternates
-rw-r-r-- 1 root root 541 Sep 25 2013 anacrontab
-rw-r-r-- 1 root root 55 Aug 1 2013 aacsound.conf
```
