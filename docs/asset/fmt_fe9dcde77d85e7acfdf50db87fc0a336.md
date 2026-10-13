
许多时候，在系统日志文件中添加手动注释以标记活动的开始或结束是非常有价值的。当你运行脚本执行某些任务并希望在执行过程中的各个阶段记录状态或添加注释时，这尤为重要。这对于调试应用程序的启动以确定故障发生在何处非常有帮助。

`syslog.conf`文件中的`Modules`部分通过`syslog`模块支持使用`logger`命令向`messages`文件记录自定义消息。该命令可以由普通用户或 root 用户运行。以下示例显示了如何记录调用者重启了系统：

```bash
[user1@server1 ~] logger -i "System rebooted by $USER"
```

查看`messages`文件的最后一行，你将看到记录的消息，以及时间戳、主机名和 PID。你可以使用`tail`命令来实时观察该文件。

记录事件的默认优先级为`user.notice`。更多信息请参阅`logger`命令的手页。

## systemd 日志

除了 rsyslog 服务外，RHEL 还提供了一个基于 systemd 的日志服务，用于收集和存储日志数据。该服务通过`systemd-journal`守护实现。该服务的功能是收集、存储和显示来自各种来源的日志事件，例如内核、`rsyslog`和其他服务、初始内存磁盘以及启动阶段生成的警。它将这些消息以二进制格式存储在名为 journals 的文件中，这些文件位于`/run/log/journal`目录下。这些文件经过结构化和索引，以便更快、更方便地搜索，并可以使用`journalctl`命令进行查看和管理。如你所知，`/run`是系统启动时在内存中创建的虚拟文件系统，在系统运行期间维护，并在关闭时删除。因此，其中存储的数据是非持久的，但根据需要，你可以启用日志的持久化存储。

RHEL 同时运行`rsyslog`和`systemd-journal`。事实上，`systemd-journal`收集的数据可以转发到`rsyslog`，以便以文本格式进行进一步处理和持久化存储。

该服务的主要配置文件为`/etc/systemd/journal.conf`，它包含了许多影响服务整体功能的默认设置。可以根据需要修改这些设置。

### 获取和查看消息

RHEL 提供了`journalctl`来从日志中检索消息，并可以使用不同的选项以多种方式进行查看。一种常见的用法是不带任何选项运行命令，以查看自上次重启以来生成的所有消息。以下显示了日志中的几条目：

```
[user1server]$ sudo journalctl --since at 2019-10-15 09:25:41 EDT
Oct 15 09:25:41 server1.example.com kernel: Line BOOT: x86 xstate kernel-3.18.0-11.2.el[2] (mockbuild-x86-va-07.build.
Oct 15 09:25:41 server1.example.com kernel: x86/fpu Enabling XAVE feature 0001: floating point re
Oct 15 09:25:41 server1.example.com kernel: x86/fpu Enabling XAVE feature 0002: SSE registers
Oct 15 09:25:41 server1.example.com kernel: x86/fpu Enabling XAVE features on, context size is 832 bytes
```

注意`journalctl`的格式与你之前看到的记录在`/var/log/messages`文件中的事件相似。每行以时间戳开头，随后是系统主机名、带或带 PID 的进程名以及实际消息。

让我们带有不同的选项运行`journalctl`命令产生各种报告。

要为每个条目显示详细输出，请使用`-o verbose`选项：

```
[user1server]$ sudo journalctl --since at 2019-10-15 09:25:41 EDT, --until at 2019-10-15 12:19:09 EDT --o verbose
Oct 15 09:25:41 server1.example.com 91.429392 [id=ff25d648706b4d7a6c4as448f5326b6i:2;b=e7da5e82e6fc4cefb486bb87dd00165f] SOURCE_MONOTONIC_START=0
TRANSPORT=kernel
SYSLOG_FACILITY=kernel
MESSAGE=Linux version 4.18.0-108.80.11.2.el8.0.x86_64 (mockbuild-x86-va-07.build.eng.bos.redhat.com) (gcc) v4
BOOT_ID=e7da5e82e6fc4cefb486bb87dd00165f
MACHINE=5ff25d648706b4d7a6c4as448f5326b6i:2
HOSTNAME=server1.example.com
Oct 15 09:25:41 91.429392 [id=ff25d648706b4d7a6c4as448f5326b6i:2;b=e7da5e82e6fc4cefb486bb87dd00165f] SOURCE_MONOTONIC_START=0
```

要查看自上次系统重启后的所有事件，使用`-b`选项：

```
[user1server]$ sudo journalctl -b
```

你可以指定`-0`（默认，自上次重启以来）、`-1`（上一次重启）、`-2`（两次重启之前），以此类推来查看来自以前系统重启的消息。

要仅查看自上次系统重启以来由内核生成的警报：

```
[user@server1 ~]$ sudo journalctl -kb0
```

要将输出限制为特定数量的条目（下方示例中为 3），使用`-n`选项：

```
[user@server1 ~]$ sudo journalctl -n 3
Logs begins at 2019-10-15 09:25:41 EDT, end at 2019-10-15 12:29:36 EDT
Oct 15 12:29:36 server.example.com [41600]: user : TTY=tty; PRWD=/home/user; USER=root
Oct 15 12:29:36 server.example.com [41601]: pam_unix(sshd:session): Cannot create session;
Oct 15 12:29:36 server.example.com [41601]: pam_unix(sshd:session): opened for user
```

显示特定服务的所有警报，例如 cron：

```
[user@server1 ~]$ sudo journalctl -u /bin/chronyd
Logs begins at 2019-10-15 12:31:15 EDT
Oct 15 09:25:56 server.example.com chronyd[78441]: STARTUP: (1.5)
Oct 15 09:25:56 server.example.com chronyd[78441]: CRON: Pool will be used instead.
Oct 15 09:25:56 server.example.com chronyd[78441]: CRON: Frequency=33s, scaled by 1
Oct 15 09:26:10 server.example.com chronyd[78441]: System clock set back 7 seconds
```

获取特定服务的消息，例如与 chronyd 关联的 PID：

```
[user@server1 ~]$ sudo journalctl -u=78441
Logs begins at 2019-10-15 12:35:39 EDT
Oct 15 09:25:50 server.example.com sshd[79441]: Server listening on 0.0.0.0 port 22.
Oct 15 09:25:56 server.example.com sshd[79441]: Server listening on port 22.
Oct 15 09:27:40 server.example.com sshd[2150]: Accepted password for user from 192.168.0.21 port 49876
Oct 15 09:27:41 server.example.com sshd[2150]: pam_unix(sshd:session): opened for user
```
