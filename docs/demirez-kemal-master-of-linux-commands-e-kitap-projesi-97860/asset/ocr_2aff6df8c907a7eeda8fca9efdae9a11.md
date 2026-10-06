# 70 | Master of Linux Commands

```
root@kemal:~/zyno# ls -l > list
root@kemal:~/zyno# cat list
top 16
-rw-r-r-- 1 root root 30 Eki 7 09:58 linuxcmd
-rw-r-r-- 1 root root 0 Eki 7 10:04 list
-rw-r-r-- 1 root root 42 Eki 6 01:34 test
-rw-r-r-- 1 root root 26 Eki 6 00:56 test-1
-rw-r-r-- 1 root root 8 Eki 6 01:23 test-2
root@kemal:~/zyno#
```

Now let's give an example about how we use echo command in another way and have additional information. First, let's look at the contents of the directory with the ls command that we were in, and then use the echo * command, let's check if the output is the same in both commands.

```
root@kemal:~/zyno# ls
linuxcmd list test test-1 test-2
root@kemal:~/zyno# echo *
linuxcmd list test test-1 test-2
root@kemal:~/zyno# _
```

As you can see the output of the two commands are the same. The reason is that, before starting the echo command shell, with * character and in /zyno directory all file index names to the command line get place, and give them as each to echo parameters. This means, with the fact that echo * command screen asterix (*) character was supposed to pop up, but it was not. So that means, asterix character is not sent as a parameter to echo.

```
root@kemal:~/zyno# echo "linux commands"
linux commands
root@kemal:~/zyno# echo *
linuxcmd list test test-1 test test-2
root@kemal:~/zyno# _
```

§