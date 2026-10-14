

作业编号、正在打印的文件以及过滤前的文件大小。作业顺序为先进先出。作业编号在需要从队列中移除特定作业时非常重要。默认情况下，lpq 命令检查默认打印机（/etc/printcap 文件中名为 lp 的打印机）的打印 spool 队列。要检查特定打印机队列，请使用 -P printer 选项。

## Listing 10.2 lpq Output

```
laserjet is ready and printing

Rank Owner Job Files Total Size

Active dws 1 /home/dws/ts 1298 bytes

1st smg 300 resume.txt 4989 bytes

2nd ldh 38 salary.txt 159456 bytes
```

lprm 命令从队列中移除作业。用户可以删除他们提交的作业。作业的所有者由调用 lpr 命令的用户名和机器名决定。如果没有选项，lprm 将删除当前活动作业，前提是该作业由调用 lprm 的用户拥有。

- lprm—从队列中移除作业。
- -P printer—指定与打印机关联的队列，否则使用默认打印机。
- -—删除调用 lprm 的用户的全部作业；如果是超级用户，则会删除全部作业。
- User—如果指定了用户名，则删除该用户的全部作业（仅限超级用户）。
- job#—删除列出的作业编号。

lpc 命令使系统管理员能够控制打印机系统的操作。lpc 命令可以启用/禁用打印机或队列。可以使用此命令更改待打印作业的顺序。lpc 提供打印机、守护进程和队列的状态。lpc 只能管理本地 spool 的打印机。但请注意，lpc 并不能总是报告打印机/队列状态的有效信息。表 10.3 包含 lpc 的选项。

如果命令行中不包含任何选项，lpc 将以交互方式运行。用户将看到 lpc> 提示符，可接受表 10.3 中的任何命令。lpc 最常用的选项是 enable/disable 和 up/down 命令。enable/disable 命令仅影响作业向队列的 spool。已在打印机队列中的作业不受影响。up/down 命令影响队列和打印。有时打印系统会进入 lpc 无效的状态。如果 lpc 无法修复问题，则需要手动停止并启动 lpc 守护进程。

| Table 10.3 lpc Subcommands |  |
|---|---|
| Command | Action |
| abort | Terminates active spooling daemon and then disables printing. |
| clean | Removes all temporary files, data files, and control files that cannot be printed. |
| disable | Turns off the specified printer queues. |
| down | Turns off the specified printer queue, disables printing, and puts message in printer status file. |
| enable | Enables spooling on local queue. |
| exit/quit | Exits from lpc. |
| restart | Attempts to start a new printer daemon. |
| start | Enables printing and starts a spooling daemon. |
| status | Displays status of daemons and queues. |
| stop | Stops spooling daemon after current job completes. |
| topq | Places jobs in order listed at top of queue. |
| up | Enables everything and starts a new printer daemon. |
| help or ? | Prints out help information. |

lpc 命令使系统管理员能够控制打印机系统的操作。

![](img/415c89a1ede71e11e5040a0038b6916c_425_0.png)

## SysV PRINT SERVICES

SysV 版打印服务由四个主要组件组成。第一个组件是 lp 程序，它提供命令行用户界面将作业发送到打印机。第二个组件是 lpsched 守护进程。lpsched 是 spooler 守护进程，负责控制对本地打印机的访问，将作业从 spool 目录移动到打印机，并传输远程作业。第三个组件是 lpadmin 命令。lpadmin 通过定义打印机和设备来配置本地打印系统。管理命令构成了 SysV 打印系统的最后一个组件。

### lp

lp 命令是提交打印作业的命令行界面。可以使用 lp 命令输入多个选项来指定目标、副本数量和其他不胜枚举的选项。请查阅 lp 的手册页以了解完整信息。在 SysV 中，可以有打印机或类。类通常是一组具有相同一般特征的打印机（Postscript 打印机）。如果作业发送到类，则第一个可用的打印机将获得该作业。lp 将要打印的文件复制到 spool 目录，通常位于 /var/spool/lp/request/destination（destination 为打印机或类名）。

### lpsched

lpsched 是将打印作业从 spool 目录传输到打印机的守护进程。lpsched 在启动时由启动脚本调用，并在后台运行。lpsched 记录处理的所有作业以及可能发生的任何错误。日志文件位于 /usr/spool/lp/log，在遇到打印问题时应首先检查该文件。

### lpadmin

SysV 使用 lpadmin 命令配置打印机。lpadmin 配置 spooling 系统以描述打印机和类并设置默认打印机。lpadmin 可以添加和删除目标（打印机）、更改类的成员资格以及更改打印机接口程序。它创建的文件放在 /usr/spool/lp 中，不应手动编辑。

