# 68 | Master of Linux Commands

Here, I want to talk briefly about that we will use again in time, about | sign in and piping (pipe). As seen in the example above, with the pipe transaction a output command is given as input command. When we examine the example, reading the contents of test file is given as input to tr command and tr command in accordance with the parameters used in the file content with its trade. Piping process is made by "|\ Yes, let us keep to our examples.

We talked about that we can read the contents of the text file with cat command to the terminal. Now, for example, with the passwd file content with cat /etc/passwd command

```
root@kemal:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
demon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/usr/sbin/nologin
sys:x:3:3:dev:/usr/sbin/nologin
sync:x:4:6534:sync:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
```

The file content shown as it is. If we want to see the content with the rows, we must use cat -n /etc/passwd command.

```
root@kemal:~$ cat -n /etc/passwd
1 root:x:0:0:root:/root:/bin/bash
2 demon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
3 bin:x:2:2:bin:/usr/sbin/nologin
4 sysys:x:3:3:dev:/usr/sbin/nologin
5 sync:x:4:6534:sync:/bin/sync
6 games:x:5:60:games:/usr/games:/usr/sbin/nologin
7 lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
8 mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
9 news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
10 uuc:x:10:10:uuc:/bin:/usr/sbin/nologin
11 proxy:x:12:13:proxy:/bin:/usr/sbin/nologin
12 www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
13 backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
14 list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
15 irc:x:39:39:irc:/var/run/irc:/usr/sbin/nologin
```