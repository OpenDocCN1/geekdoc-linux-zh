

现在你已经熟悉了最常用的运行级别脚本，请完成练习 14.2 以学习更多。

## 练习 14.2

## 运行级别脚本

大多数 Linux 系统使用表 14.2 中未列出的额外脚本。要了解系统上安装的脚本，请检查 /etc/rc.d/init.d 目录并识别表 14.2 中未找到的任何脚本。检查这些脚本的内容以了解它们的作用。大多数脚本都包含解释其功能的注释。

大多数脚本接受控制其运行的参数。最常用的参数有：

- start，导致脚本启动关联的服务
- stop，导致脚本停止关联的服务
- restart，导致脚本重启关联的服务
- reload，导致脚本重新读取配置文件
- status，导致脚本报告关联服务的状态

linuxconf 程序使用这些脚本来启动和停止服务。你也可以手动调用它们来控制服务。例如，你可以通过执行命令关闭 Web 服务器（httpd 服务）：

```
/etc/rc.d/init.d/httpd stop
```

或者，你可以通过执行命令重启服务器：

```
/etc/rc.d/init/httpd restart
```

使用 /etc/rc.d/init.d 中的脚本而不是通过其他方式控制服务是非常重要的。例如，可以通过执行命令 /usr/sbin/httpd 来启动 Web 服务器。但是，如果你这样做，Linux 在你关闭服务器时将无法清理锁文件和进程标识文件。更糟糕的是，除非使用运行级别脚本，否则可能会无意中启动多个服务器实例。

## /etc/rc.d/rc?.d 中的符号链接

/etc/rc.d/rc?.d 中的符号链接名称如 K05keytable 和 S40atd。以 K 开头的链接在被 /etc/rc.d/rc 执行时会接收 stop 参数；以 S 开头的链接则接收 start 参数。通常情况下，与运行级别相关的目录会为每个已安装的服务包含一个 K 脚本或一个 S 脚本。

脚本名称中的两个数字数字被称为“优先级”，它指示了给定目录中脚本运行的顺序；例如，脚本 K10ufs 会在脚本 K15gm 之前运行。表 14.3 根据脚本执行时的运行级别总结了这些运行级别脚本。

## 表 14.3 按运行级别总结的常用运行级别脚本

| Script | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| K01linuxconf | | X | X | | | | |
| K05keytable | | X | X | | | | |
| K10ufs | | X | X | | | | |
| K15gpm | | X | X | | X | X | |
| K15httpd | | X | X | | X | X |
| K15sound | | X | X | X | | | X |
| K20nfs | | X | X | X | | | X |
| K20rstatd | | X | X | X | X | X | X |
| K20usersd | | X | X | X | X | X | X |
| K20rwhod | | X | X | X | X | X | X |
| K30sendmail | | X | X | | X | X | | |
| K35smb | | | | X | X | | |
| K45named | | X | X | X | | | X |
| K45sshd | | X | X | X | | | X |

## 表 14.3 按运行级别总结的常用运行级别脚本（续））

| Script | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| K50inet | | X | | | | X | |
| routed | | X | X | X | X | X | |
| K60atd | | X | X | X | | | X |
| K60crond | | X | X | | | | X |
| K61pd | | X | X | | | | X |
| K80random | | X | | | | | X |
| K85netfs | | X | X | | | | X |
| K89portmap | | X | X | X | | | X |
| K90killall | | X | | | | | X |
| K90mysql | | X | X | | | | X |
| K90network | | X | X | | | | X |
| K92apm | | X | X | X | X | X | |
| K96pcmcia | | X | | X | X | X | |
| K99syslog | | X | X | | | | X |
| S0halt | | X | | | | | |
| S000 | | X | | | | | | |
| S00reboot | | | | | | | X |
| S05apmd | | | X | | | | |
| S10network | | | X | X | X | | |
| S11portmap | | | | X | X | | |
| S15netfs | | | | X | X | | |

## 表 14.3 按运行级别总结的常用运行级别脚本（续）

| Script | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| S20random | | X | | X | X | | |
| S30syslog | | | X | | | | |
| S40atd | | | | X | X | X | |
| S40crond | | | X | X | X | | |
| S45pcmcia | | | X | | | | |
| S50inet | | | | X | X | X | |
| S55named | | | | X | X | | | |
| S55sshd | | | | X | X | X | |
| S601pd | | | X | X | X | | |
| S60nfs | | | | X | X | | | |
| S75keytable | | | X | X | X | | |
| S85sound | | | X | X | X | | |
| S85gpm | | | X | | | | |
| S90mysql | | | | X | X | X | |
| S90xfs | | | X | | | | | |
| S90xfs | | | | X | | | |
| S91linuxconf | | | X | X | X | | |
| S99local | | | X | | | | |

当运行级别脚本结束时，它会报告完成状态。可能的值有：

- OK，表示脚本成功启动关联的服务
- Passed，表示脚本遇到错误但能够恢复并成功启动的服务
- Failed，表示脚本无法启动关联的服务

完成状态会在启动期间显示在控制台上。

/etc/rc.d/rc 的操作

所示，/etc/rc.d/rc 脚本设置运行级别并调用相应的运行级别脚本。以下是它执行的操作详细步骤：

1. 源 /etc/rc.d/init.d/functions 文件，包含一组函数。这些函数由 /etc/rc.d/init.d 目录使用。
2. 确定当前和之前的运行级别。
3. 检查是否设置了用户模式。
4. 将运行级别设置为指定的值。
5. 通知 linuxconf 当前运行级别。
6. 找到 n 为新运行级别的 /etc/rc.d/rc?.d 目录。
7. 执行每个运行服务的 kill 脚本。
8. 执行每个未运行服务的 start 脚本。

系统启动期间，init 进程调用 /etc/rc.d/rc 文件。第 15 章详细描述了这个过程。

将服务与运行级别关联

原则上，你可以通过在 /etc/rc.d/rc?.d 目录中创建和操作符号链接来将服务与运行级别关联。但由于这样做非常繁琐且容易出错，可以使用几种工具来辅助完成任务。这些工具包括：

- chkconfig，命令行工具
- ksys，基于 KDE 的工具
- nsys，文本模式工具
- tsys，图形界面工具

这些工具中最重要的是，其他工具在配置服务时可能不可用。chkconfig 允许：

- 列出已安装的服务
- 添加服务
- 将服务与运行级别关联

列出服务

要列出已安装的服务及其关联级别，执行命令 `chkconfig --list`。输出如下：

```
httpd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
amd 0:off 1:off 2:on 3:off 4:off 5:off 6:off
atd 0:off 1:off 2:off 3:on 4:on 5:off 6:off
named 0:off 1:off 2:off 3:on 4:on 5:on 6:off
keytable 0:off 1:off 2:on 3:on 4:on 5:off 6:off
gpm 0:off 1:off 2:on 3:off 4:off 5:off 6:off
netfs 0:off 1:off 2:off 3:on 4:on 5:off 6:off
network 0:off 1:off 2:on 3:on 4:on 5:off 6:off
random 0:off 1:off 2:on 3:on 4:on 5:off 6:off
pcmia 0:off 1:off 2:on 3:off 4:off 5:off 6:off
nfs 0:off 1:off 2:off 3:on 4:on 5:off 6:off
```

将服务与运行级别 3

```
linuxconf 0:off 1:off 2:on 3:on 4:on 5:on 6:off
lpd 0:off 1:off 2:on 3:on 4:on 5:on 6:off
inet 0:off 1:off 2:off 3:on 4:on 5:on 6:off
portmap 0:off 1:off 2:off 3:on 4:on 5:on 6:off
sound 0:off 1:off 2:off 3:on 4:on 5:on 6:off
routed 0:off 1:off 2:off 3:off 4:off 5:off 6:off
rstatad 0:off 1:off 2:off 3:off 4:off 5:off 6:off
usersd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
rwhod 0:off 1:off 2:off 3:off 4:off 5:off 6:off
smb 0:off 1:off 2:off 3:off 4:off 5:off 6:off
sendmail 0:off 1:off 2:on 3:off 4:off 5:on 6:off
syslog 0:off 1:off 2:on 3:on 4:on 5:on 6:off
crond 0:off 1:off 2:on 3:on 4:on 5:on 6:off
xfs 0:off 1:off 2:on 3:on 4:on 5:on 6:off
yypbind 0:off 1:off 2:off 3:off 4:off 5:off 6:off
shhd 0:off 1:off 2:off 3:on 4:on 5:on 6:off
mysql 0:off 1:off 2:on 3:on 4:on 5:on 6:off
```

