
`who` 命令列出当前登录用户的名称、终端行号和登录时间。

The of of purpose is to find who is on the system. The `who` command lists the, terminal the, and of times of the in. If you want to communicate with is on the computer. the command, you can find out who is. You can also use `who` to see when certain users are logged into the computer to keep track of their time.

# TROUBLESHOOTING

- commands I put in my crontab file don't work.
- When I try to use the command, I don't have permission to use it. You haven't added your login ID to the `/etc/cron.d/at.file`
- I tried to use the `at now` to run a command immediately. No matter how fast you type, `at now` responds with the message ERROR: Too late. The best alternative is to use the `batch` command to run the command for you. Can, however, use `at now +5 min` to run the command in five minutes. After you press `<Return>`, type quickly to enter your command before the five minutes expire.

# Reporting On and Monitoring the Multitasking Environment

You know that Linux is a multiuser, multitasking operating system. Because so many people can do so many things with the system at the same time, users find it useful to determine who's using the system and what processes are running, as well as to monitor processes.

![](img/c03a7f0ab2607b89c7035fa9e718_0.png)

# Chapter 19 Managing Multiple Processes

Knowing that others can keep track of the commands you enter is important. Most users can access your files without your permission, but they can see the names of commands you enter. Also (as the system administrator) or someone else with the root password can erase all the files on the system. Although you don't have to be paranoid about privacy on a Linux system, you should know that the system can be monitored by anyone who wants to take the time to do it. The you can gain about what is on the system is more useful than just curiosity: By seeing what jobs are running, you can appropriately schedule your tasks and see whether a process of yours is still active and whether it's behaving properly.

# Finding Out Who's on the System

The purpose of `who` command is to find who is logged into the system. The `who` command lists names, terminal lines, and login times of users now logged in. If you want to communicate with someone on the computer using the `write` command, you can find out who is on. You can also use `who` to see when certain users are logged into the computer to keep track of their time.

To specify a sequence of values for the first four fields, use commas to separate the values. Suppose you have a program, `checkpoints`, that accesses a service that provides stock quotes and puts the quotes in a file. To get those quotes at 9 a.m., 11 a.m., 2 p.m., and 4 p.m. on Monday, Tuesday, and Thursday of every week—and definitely on the 10th of March and entry:

`* * 09,11,14,16 10 03,09 01,02,04 chkquotes`

Put the command lines into a file by using `vi` or any other editor that allows you to save files as text files. Assume that you put your commands in a file named `cronjobs`. To use `crontab` to put the file where cron can find it, enter this command:

`crontab cronjobs`

To sort a file `/user/www/sales/weekly` and mail the output to a user named at 7:30 a.m. each Monday, using the following entry in a file:
`30 07 * * 1 sort /usr/www/sales/weekly | mail -s Sales* email`

This command specifies the minute as 30, the hour as 07, any day of the month with the asterisk, any month of the year with another asterisk, and the day-of-week as 01 (which represents Monday).

Notice the pipe between the `sort` and `mail` commands in the preceding example. The command field can contain pipes, semicolons, arrows, or anything else you enter on a shell command line. At the specified date and time, cron runs the entire command field with a standard shell (`bash`).

## 第 19 章 管理多个进程

输入 `finger username`（如果用户在另一台计算机上，则输入 `finger username@domain`）。
例如，要查看名为 `tackett` 的用户的更多信息，你可以输入此命令：

```bash
```
