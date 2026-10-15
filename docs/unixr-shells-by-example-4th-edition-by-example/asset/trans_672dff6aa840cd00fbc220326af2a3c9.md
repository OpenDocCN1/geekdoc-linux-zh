

## EXPLANATION

- 1 crontab -l 命令的输出被重定向到名为 instructions 的文件。在此示例中，因为 crontab 文件中没有列出任何命令，instructions 文件将只包含由 crontab 命令生成的一些注释。
- 2 instructions 文件使用 vi 进行编辑。此文件可能包含或不包含任何起始行。这取决于你的 UNIX/Linux 版本以及 root 是否之前为 cron 输入过指令。
- 3 在文件的底部添加了一条新指令。此指令告诉 cron 每天每天的 1:25 a.m. 运行 /root/checkpercent 脚本。有关在此文件中指定时间的详细信息（时间由该行开头的数字和星号表示）可在 crontab 手册页中找到。
- 4 crontab 命令用于将 instructions 文件提交给 cron。
- 5 crontab -l 命令导致 cron 显示当前用户，即本例中为 root 用户的当前指令集。这验证了 cron 已接受来自上一命令的文件。

## The cron Boot Script.

在查看 cron 启动脚本的内容之前，让我们先看看启动脚本的总体布局。以下示例显示了 Red Hat 系统上运行级别 5 的部分启动脚本列表。虽然大多数其他 UNIX 版本的启动脚本布局类似，但有些，如 Mac OS X 中的 Darwin，则大不相同

下面是 Red Hat Linux 下运行级别 5 启动脚本所在目录的截断列表。

### EXAMPLE 16.12

```
1 # pwd
/etc/rc5.d
2 # ls
#
K20nfs   K45named   S55sshd   S90crond
... K35smb   S12syslog   S80sendmail1
# ls -l /etc/rc5.d/cron:
-rwxrwxrwx 1 root root 15 Oct 13 21:19 /etc/rc5.d/S90crond ->
../init.d/crond
4 # ls -l /etc/init.d/cron:
-rwxr-xr-x 1 root root 1316 Feb 19 2004 /etc/init.d/crond
```

## EXPLANATION

- 1 当前目录是 /etc/rc5.d，即运行级别 5 的启动脚本目录（Red Hat Linux）。
- 2 列表显示有些脚本名称以 S 开头，有些以 K 开头。

## EXPLANATION (CONTINUED)

- 3 此脚本启动 cron 守护进程，因为文件名以 S 开头。如果脚本名称以 K 开头，则脚本将停止 cron 守护进程。输出显示该文件实际上是一个链接——文件权限前面的字母 l 表示链接。-> 字符指向链接文件 crond，该文件位于 /etc/init.d 目录中。
- 4 运行级别目录中的每个脚本通常都是指向 /etc/init.d 目录中主副本的链接。
- 5 这是 cron 启动脚本主副本的列表。请注意，主副本的名称不以 S 或 K 开头，也不包含数字。启动目录中通常有多个指向主脚本的链接，只有链接名称会包含数字。此主脚本可用于启动或停止 cron 守护进程。我们将在下一节详细查看该脚本。

cron 启动脚本名为 crond，可以手动运行以启动或停止 cron 守护进程。在某些发行版中，它还可用于检查状态或重启 cron。其他发行版允许使用额外参数。传统上，启动脚本是通过在脚本名称前加上为其编写的 shell，然后是脚本名称来运行的。下面示例运行了 /etc/init.d 目录中的 crond 脚本的主副本。由于它们是链接的，你也可以通过运行 /etc/rc5.d/crond 脚本来实现同样的效果。

### EXAMPLE 16.13

```
1 # cd /etc/init.d
2 # ls crond
crond
3 # sh crond stop
Stopping crond: [OK]
4 # sh crond start
Starting crond: [OK]
5 # sh crond restart
Stopping crond: [OK]
Starting crond: [OK]
```

## EXPLANATION

- 1 cd 命令用于切换到 /etc/init.d 目录，该目录包含启动脚本的主副本。
- 2 ls 命令验证 cron 启动脚本是否存在。
- 3 crond 脚本使用 stop 参数运行以停止 cron 守护进程。由于当前用户是 root，因此脚本是通过在脚本名称前加上为其编写的 shell 来运行的。

