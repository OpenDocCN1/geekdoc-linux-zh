A few sample lines from a messages log file are shown here. Notice that the host name for all these messages is brighton, the name of someone's computer. Also notice that several different programs have generated the log messages shown here, including the Linux kernel, the httpd daemon (the Web server), the sound system, and other programs.

```
Oct 26 06:42:29 brighton kernel:
Installing knfsd (copyright (C) 1996 ok
Oct 26 06:42:29 brighton nfs: rpc.nfsd startup succeeded
Oct 26 06:42:29 brighton keytable: Loading keymap:
Oct 26 06:42:30 brighton keytable: Loading /usr/lib/kbd/keymaps/1386/qwe
Oct 26 06:42:30 brighton keytable: Loading systemfont:
Oct 26 06:42:30 brighton rc: Starting keytable succeeded
Oct 26 06:42:30 brighton gpm: gpm startup succeeded
Oct 26 06:44:57 brighton rpc.statd[451]:
gethostname error for brighto
Oct 26 06:45:01 brighton httpd: Cannot determine local host name.
Oct 26 06:45:01 brighton httpd:
Use the ServerName directive to set it
Oct 26 06:45:01 brighton httpd: httpd startup failed
Oct 26 06:45:01 brighton sound: Starting sound configuration:
Oct 26 06:45:01 brighton sound: sound
Oct 26 06:45:01 brighton rc: Starting sound succeeded
Oct 26 06:45:02 brighton PAM_pwdb[582]:
(su) session opened for user xfs
Oct 26 06:45:03 brighton PAM_pwdb[582]:
(su) session closed for user xfs
Oct 26 06:45:03 brighton xfs: xfs startup succeeded
Oct 26 06:45:05 brighton rc: Starting local succeeded
Oct 26 06:45:08 brighton PAM_pwdb[629]: check pass; user unknown
Oct 26 06:45:09 brighton login[629]:
FAILED LOGIN 1 FROM (null) FOR root, User not known to the
underlying authentication module
```

Right now you don't have to understand everything in the preceding log file lines. But you should become familiar with the format of a log line.

If you see a program in a log line that you don't recognize, you can use the whatis command to learn about it. This command looks at a database of program descriptions and prints a one-line description of the program you ask about. Sometimes the result is not too helpful, but it can give you a starting place and also refer you to a man page that may provide more information.

![](bbox=[0.12, 0.93, 0.22, 0.99])

The whatis command uses an internal database to find an answer to your query. That database should be prepared automatically, but if it is not available, you can create it by running the command makewhatis.