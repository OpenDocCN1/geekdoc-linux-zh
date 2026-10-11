```
```
-rw-r--r--   1 root     root          703 Feb 17 00:35 aeplog.conf
drwxr-xr-x   4 root     root         4096 Jun 11 08:47 alchemist
-rw-r--r--   1 root     root          1419 Jan 26 10:14 aliases
-rw-r---r--   1 root     smpmmp       12288 Jun 17 13:17 aliases.db
drwxr-xr-x   2 root     root         4096 Jun 11 11:11 alternatives
drwxr-xr-x   3 amanda   disk         4096 Jun 11 10:16 amanda
-rw-r--r--   1 amanda   disk             0 Mar 22 12:28 amandates
-rw-r---r--   1 root     root          688 Mar  4 22:34 amd.conf
-rw-r--r--   1 root     root          331 May  5 08:07 ant.conf
-rw-r--r--   1 root     root          317 Feb 15 14:33 anacrontab
-rw-r--r--   5 root     root          331 May  5 08:07 ant.conf
-rw-r---r--   1 root     root         6200 Jun 16 16:42 asound.state
drwxr-xr-x   3 root     root         4096 Jun 11 10:37 atalk
-rw-r---r--   1 root     root          1 May  5 13:39 at.deny
-rw-r--r--   1 root     root          325 Apr 14 13:39 auto.master
-rw-r--r--   1 root     root          581 Apr 14 13:39 auto.misc
--More-
```
```

In the preceding example, the output of the `ls -1` command was redirected to the `more` command, which displays the first page of output on the terminal. You can then advance through the output page-by-page or line-by-line. This type of redirection is discussed in Chapter 8, "Working with the BASH Shell."

# ## Displaying the Contents of Binary Files

It is important to employ text file commands, such as `cat`, `tac`, `head`, `tail`, `more`, and `less`, only on files that contain text; otherwise, you might find yourself with random output on the terminal screen or even a dysfunctional terminal. To view the contents of binary files, you typically use the program that was used to create the file; however, some commands can be used to safely display the contents of most binary files. The **strings command** searches for text characters in a binary file and outputs them to the screen. In many cases, these text characters might indicate what the binary file is used for. For example, to find the text characters inside the `/bin/echo` binary executable program page-by-page, you could use the following command:

```
```
[root@server1 root]# strings /bin/echo | more
//lib/d-linux.so.2
<int<ke
[*.]
[*_]
Try '$s --help' for more information.
Usage: '$s [OPTION]... [STRING]...
```
```