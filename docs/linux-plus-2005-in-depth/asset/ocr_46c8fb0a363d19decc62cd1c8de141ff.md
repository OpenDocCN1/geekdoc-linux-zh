```
[root@server1 root]$ sort <newhosts >newhosts
[root@server1 root]$ cat newhosts
[root@server1 root]$ _
```

The newhosts file has no contents when displayed in the preceding output. Because the BASH shell saw that output redirection was indicated on the command line, it cleared the contents of the file newhosts, then sorted the blank file and saved the output (nothing in our example) into the file newhosts. Because of this feature of shell redirection, Linux administrators commonly use the command >>fileName at the command prompt to clear the contents of a file.

> **NOTE**
> 
> The contents of log files are typically cleared periodically using the command >>path/to/logfile.

Table 8-1 summarizes the different types of redirection shown in this section.

**Table 8-1** Common redirection examples
| **Command** | **Description** |
|---|---|
| command 1>file<br>command >file | The Standard Output of the command is sent to a file instead of to the terminal screen. |
| command 2>file | The Standard Error of the command is sent to a file instead of to the terminal screen. |
| command 1>fileA 2>fileB<br>command >fileA 2>fileB | The Standard Output of the command is sent to fileA instead of to the terminal screen, and the Standard Error of the command is sent to fileB instead of to the terminal screen. |
| command 1>file 2>&1<br>command >file 2>&1<br>command 1>&2 2>file<br>command >&2 2>file | Both the Standard Output and the Standard Error are sent to the same file instead of to the terminal screen. |
| command 1>>file<br>command >>file | The Standard Output of the command is appended to a file instead of being sent to the terminal screen. |
| command 2>>file | The Standard Error of the command is appended to a file instead of being sent to the terminal screen. |
| command 0<file<br>command <file | The Standard Input of a command is taken from a file. |