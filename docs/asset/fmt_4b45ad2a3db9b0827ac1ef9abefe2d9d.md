
要使用 `at` 命令，输入 `at` 命令并提供运行时间作为参数——你将看到一个 `at>` 提示符。输入要执行的命令然后按回车键。现在按 `Ctrl+D` 创建任务——出现“`<EOT>`”并且你返回到 shell 提示符。你可以通过向 `atrm` 命令指定任务编号来删除任务，并使用 `atq` 命令查看待处理任务列表。示例中的任务执行了一个 `write` 命令，在指定的时刻向系统用户发送消息：

```
user> at 4:25pm
warning: commands will be executed using /bin/sh
at> write mike
at> Hey Mike! It's time to go.
at> <EOT>
job 22 2005-10-11 16:25
user> 
```

```
Listening on Device /dev/pts/0

Message from mike@linux on <no tty> at 16:25...
Hey Mike! It's time to go.

EOF
```

![](img/0494b98ec9ddc4515587e9808d73902e_195_1.png)

Linux 还提供了一个名为“`cron` 守护进程”（`cron` daemon）的任务调度器，你可以设置按固定间隔运行作业。它每分钟唤醒一次，检查你的 `crontab` 配置文件，然后执行任何设置为在当前时间运行的作业。

一个 `crontab` 文件每行包含一条指令，每条指令包含字段——前五个字段指定作业运行的时间，第六个字段包含要执行的命令。五个时间字段按顺序依次为：分钟 (`0-59`)、小时 (`0-23`)、日期 (`1-31`)、月份 (`1-12`) 和星期 (`0-6`)——零代表星期日。字段之间必须用空格分隔，任何字段都可以包含一个 `*` 通配符来匹配该字段的任何值。例如：

![](img/0494b98ec9ddc4515587e9808d73902e_196_0.png)

| 字段 | 说明 |
| :--- | :--- |
| `*` | 每分钟 |
| `15 * * * *` | 每小时后 15 分钟 |
| `15 18 * * *` | 每天下午 6:15 |
| `15 18 * 3 *` | 每月第三天下午 6:15 |
| `15 18 * 2 3` | 每年 2 月 3 日下午 6:15 |
| `15 18 * * 6` | 每周六下午 6:15 |

要调度作业，你可以使用 `crontab -e` 命令编辑 `crontab` 文件以在文本编辑器中打开它。添加要运行的时间和命令，然后保存文件即可设置完成。下面的 `crontab` 每天下午 6:15 运行一次 `BitDefender` 系统扫描，然后更新主目录下日志文件中的摘要：

![](img/0494b98ec9ddc4515587e9808d73902e_196_1.png)

## 获取日期和时间

使用 `date` 命令在你的本地时区显示当前系统日期和时间。

| 命令 | 说明 |
| :--- | :--- |
| `date` | 显示当前日期和时间 |
| `cal` | 显示当前月的日历 |

可选地，可以通过添加格式指定符作为参数对 `date` 命令的输出进行多种格式化。例如，使用 `+%A` 显示当前的星期，或使用 `+%D` 以数字格式显示当前日期，或使用 `+%T` 以 `HH:MM:SS` 格式显示时间。格式指定符必须包含引号内，以避免干扰 `bash` shell。

`cal` 命令显示当前月的日历并高亮当前日期。或者，提供年份作为参数来显示一整年的日历。

为 `cal` 命令添加选项 `-3` 可以查看 3 个月的日历。

![](img/0494b98ec9ddc4515587e9808d73902e_197_0.png)

```
user> date
Mon Oct 10 12:28:59 BST 2005
user> date "+%A"
Monday
user> date "+%D"
10/10/05
user> date "+%T"
12:29:39
user> cal
October 2005
Su Mo Th Fr Sa Su
 1  2  3  4  5  6  7
 8  9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30 31
```

## 在 shell 中联网

本章演示了如何在 shell 中进行网络通信。它展示了如何传输文件、浏览互联网以及发送邮件。

- 跨网络连接
- 在网络上通信
- 通过网络传输文件
- 浏览互联网
- 发送邮件

就像街道上的每栋房子都有唯一的地址一样，网络上的每台计算机都有唯一的 `IP`（互联网协议）地址。

| 命令 | 说明 |
| :--- | :--- |
| `host` | 显示主机名和 `IP` 地址 |
| `ifconfig` | 显示本地 `IP` 地址 |
| `ping` | 发送包测试主机是否可用 |

你可以通过向 `host` 命令指定 `URL` 来发现计算机的 `IP` 地址。在某些情况下，对于大型网站，可能会显示多个 `IP` 地址，如下所示：

![](img/0494b98ec9ddc4515587e9808d73902e_199_0.png)

```
Shell - Konsole
Session Edit View Bookmarks Settings Help
user> host www.google.com
www.google.com is an alias for www.google.com
www.google.com has address 66.102.9.104
www.google.com has address 66.102.9.99
www.google.com has address 66.102.9.147
www.google.com is an alias for www.google.com
www.google.com is an alias for www.google.com
user> 
```

在 Linux 中，你可以通过假设 `root` 用户状态 (`su -l`) 并执行 `ifconfig` 命令显示所有接口来发现你计算机的 `IP` 地址。如果你的计算机有多个网络连接，每个连接将单独列出。向 `ifconfig` 提供设备名称以查看报告。

![](img/0494b98ec9ddc4515587e9808d73902e_200_0.png)

`ifconfig` 的输出很长，为了清晰起见在这里进行了截断。

```
Shell - Konsole
Session Edit View Bookmarks Settings Help
root> ifconfig ra0
ra0 Link encap:Ethernet
    inet addr:192.168.0.101
    Bcast:192.168.0.255
    Mask:255.255.255.0
root> _
```

通常，如果你的计算机通过以太网连接网络，被称为 `eth0`。如果你连接到无线网络，被称为 `ra0`——如上面的示例，`IP` 地址为 `192.168.0.101`。

跨网络测试最基本的测试是使用 `ping` 命令向其 `IP` 地址发送微数据包。这会持续发送测试包直到你停止，但也可以通过添加指定发送包数的 `-c` 选项来限制包的数量。在下面的示例中，成功发送到 `host` 命令发现的 Google `IP` 地址之一：

```
Shell - Konsole
Session Edit View Bookmarks Settings Help
user> ping -c 3 66.102.9.104
PING 66.102.9.104 (66.102.9.104)
64 bytes from 66.102.9.104: icmp_seq=1
64 bytes from 66.102.9.104: icmp_seq=2
64 bytes from 66.102.9.104: icmp_seq=3
---
66.102.9.104 ping statistics ---
3 packets transmitted, 3 received,
0% packet loss, time 2006ms
r min/avg/max/mdev = 34.8/40.1/44.2/3.936 ms
user> _
```

## 在网络上通信

“`telnet`”程序允许你登录你有账户的远程计算机。某些具有社区精神的系统允许匿名 `telnet` 访问，如下所示的雅雅社区网络：

```
Shell - Konsole
Session Edit View Bookmarks Settings Help
user> telnet
telnet> open scn.org
Trying 66.212.64.194...
Connected to scn.org.
Escape character is '^'
```

`Seattle Community Network Sun Solaris 1.1.1.B`
