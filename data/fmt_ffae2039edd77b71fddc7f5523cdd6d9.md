
```
[root@localhost]# disable -r "Changer toner cartridge"
printer:
[root@localhost]# lpstat -t
scheduler is running
system default destination: printer1
device for printer1: parallel:/dev/lp0
printer1 accepting requests since Jan 01 00:00 -
printer1 disabled since Jan 01 00:00 -
Changing toner cartridge
[root@localhost]#
```

输出表明系统上只有一台名为 `printer1` 的打印机，它打印到连接到计算机第一个端口（`/dev/lp0`）的打印机，且其打印队列中没有打印作业。此外，`cups`（调度器）正在运行，并接受作业进入该打印机的打印队列。同时，`cups` 守护进程会将作业从打印机发送到已启用的打印机。

`CUPS` 是如今 Linux 计算机首选的打印系统；许多较旧的 Linux 计算机使用传统的行打印守护进程（`LPD`）打印系统。

在这一打印系统中，使用了以下命令：

- `lpr` 命令用于将文档打印到打印队列，类似于 `lpr` 命令。
- `lpc` 命令可查看打印机状态。
- `lpq` 命令可查看打印队列中的打印作业，类似于 `lpstat` 命令。
- `lprm` 命令可删除打印作业，类似于 `cancel` 命令。

对于使用 `LPD` 打印系统的用户，`CUPS` 包含了 `lpr`、`lpc`、`lpq` 和 `cancel` 命令的版本。以下输出显示了系统上所有打印机的状态、向 `printer1` 打印了两份 `/etc/inittab`、查看队列中的打印作业并删除了打印作业：

```
[root@localhost]# lpc status
printer:
 printer is on device 'parallel' speed -1
queuing is enabled
 printing is enabled
no entries
daemon present
[root@localhost]# lpr -2 -P printer1 /etc/inittab
[root@localhost]# lpq
printer1 is ready and printing
Rank Owner Job File(s) Total
Size active root 1 inittab 2048 bytes
[root@localhost]# lprm 1
[root@localhost]# lpq
printer1 is ready
no entries
[root@localhost]#
```

## 管理打印作业

你可以使用 `lp` 命令创建打印作业。要向 `printer1` 打印 `/etc/inittab` 文件的副本（如所示）：

```
[root@localhost]# lp -P printer1 /etc/inittab
[root@localhost]# lpstat -t
scheduler is running
system default destination: printer1
device for printer1: parallel:/dev/lp0
printer1 accepting requests since Jan 01 00:00
printer1 disabled since Jan 01 00:00 -
```

你可以使用 `accept`、`reject`、`enable` 或 `disable` 命令加上打印机名称来控制打印机状态。例如，要启用 `printer1` 的池化并禁用它，可以使用以下命令：

```
[root@localhost]# lpr -2 -P printer1 /etc/inittab
[root@localhost]# lpq
printer1 is ready and printing
Rank Owner Job File(s) Total
Size active root 1 inittab 2048 bytes
[root@localhost]# lprm 1
[root@localhost]# lpq
printer1 is ready
no entries
[root@localhost]#
```

# A-2: 讨论打印作业管理

### 练习

- 1. 在不使用 `-d` 选项的情况下使用 `lp` 命令会将 `pr` 打印到默认打印机。正确还是错误？
- 2. 哪个命令为系统设置默认打印机？
  - A. `export PRINTER=printerX`
  - B. `lp -d printername`
  - C. `lpoptions -d printername`
- 3. 对于运行 `CUPS` 的系统，你使用哪种命令来查看关于所有打印机和打印作业的所有信息？
- 4. `cancel` 命令用于做什么？

# 配置打印机

打印的核心组件是 `cups` 守护进程（`cupsd`），它接受打印作业并将其队列，将其发送到打印机。包含 `cupsd` 设置的文件为 `/etc/cups/cupsd.conf`，而包含系统中已安装的每个打印机信息的文件为 `/etc/cups/printers.conf`。

### 打印机配置工具，GUI 版本

与其手动编辑这些文件，不如使用打印机配置工具（Printer Configuration Tool）更加方便，如图 11-2 所示。

![](img/90ff486f13f13845c7a30a29d84ce954_493_0.png)

图 11-2：红帽打印机配置工具

要访问此工具，你可以在终端桌面环境中输入 `system-config-printer-gui`，或者选择主菜单中的“系统设置”->“打印”。这还有一个打印机配置工具的终端版本。在终端提示符处输入 `system-config-printer-t`。

图 11-2 所示的打印机配置工具显示系统中没有配置打印机。要添加打印机，请点击“新建”（New）并指定打印队列的名称和描述，如图 11-3 所示。

![](img/90ff486f13f13845c7a30a29d84ce954_493_1.png)

图 11-3：创建新的打印队列

由于打印过程涉及在将作业发送到打印机之前将其发送到打印队列，因此打印机配置工具用于配置队列而不是打印机；出于相同的原因，打印机名称通常被称为队列名称。

# 打印机和日志文件管理 11-1

一旦你点击“下一步”（Forward），系统会提示选择打印队列类型。有几种不同的打印机类型可以配置。如果打印机通过串口、并行口或 USB 线连接到本地计算机，你应该像图 11-4 所示那样选择“本地连接”（Locally-connected）。

![](img/90ff486f13f13845c7a30a29d84ce954_494_0.png)

图 11-4：选择队列类型

如果打印机连接到远程 Linux 计算机（`CUPS` 或 `LPD`）、远程 Windows 服务器、远程网络服务器，或使用惠尔 Jetdirect 技术的网络打印机，请选择“网络”（Networked），如图 11-5 所示。

![](img/90ff486f13f13845c7a30a29d84ce954_494_1)

图 11-5：创建队列

一旦选择了打印机类型，你必须提供有关打印机的特定信息。对于本地打印机，你必须选择连接到 `/dev/lp0` 的端口。对于远程打印机，可能需要指定远程服务器的名称、IP 地址或打印机端口。随后，你将被提示选择打印机型号，如图 11-6 所示。

# 11-12 CompTIA Linux+ 2004

![](img/90ff486f13f13845c7a30a29d84ce954_495_0)

图 11-6：选择打印机

# 打印机和日志文件管理 11-3

一旦打印机创建完成，配置工具会提示你打印测试页，如图 11-7 所示。

![](img/90ff486f13f13845c7a30a29d84ce954_495_1)

图 11-7：打印测试页

你可以通过选择图 11-8 所示的“编辑”（Edit）按钮来修改任何打印机设置，或者从“测试”（Test）菜单中选择测试页。在添加或修改打印机设置后，必须选择“应用”（Apply）以生效。

# 共享打印机

注意图 11-8 所示，打印 1 是默认打印机且未共享。要共享打印机，请从“操作”（Action）菜单中选择共享，选择“此队列对其他计算机可用”，并指定哪些计算机可以打印到该打印机，如图 11-9 所示。

![](img/90ff486f13f13845c7a30a29d84ce954_496_0)

图 11-9：共享打印机

# 配置共享属性

如果你在“通用”（General）选项卡上，你可以配置 `CUPS` 自动搜索其他共享 `CUPS` 打印机，并允许远程计算机使用 `LPD` 协议打印到该打印机，如图 11-10 所示。

![](img/90ff486f13f13845c7a30a29d84ce954_496_1)

图 11-10：配置共享属性

# A-3: 创建本地打印机

| 操作方法 | 目的 |
| --- | --- |
| 按 `CTRL + ALT + F7` | 切换到图形终端 |
| 输入 `root` | |
| 输入 `password` | |
| 选择主菜单、系统设置、打印。 | 定义新打印机。 |
| 点击“下一步” | 在名称框中 |
| 输入 `lp` | 在描述框中 |
| 点击“本地连接” | 在类型框中 |
| 点击“自定义” | 在设备框中 |
| 点击“下一步” | 在队列类型中 |
| 选择“仅文本” | 在操作菜单中 |
| 点击“下一步” | 在设置屏幕中 |
| 点击“应用” | 重启 `cups` 守护进程 |
| 关闭 | 打印机配置文件 |

# 系统日志守护进程

大多数事件的记录由系统日志守护进程（`syslogd`）处理。该守护进程在系统启动时加载。它创建一个套接字（`/dev/log`）供其他系统进程写入。然后读取写入该套接字的任何信息，并将信息保存到 `/etc/syslog.conf` 文件中相应的日志文件条目。以下输出显示了一个示例 `/etc/syslog.conf` 文件：

```
[root@localhost]# cat /etc/syslog.conf
# 将所有内核消息记录到控制台。
# 记录太多内容会让屏幕变得混乱。
*.*
/dev/console
# 记录除邮件之外级别为 info 或更更高的任何内容。
# 不要记录私有的身份验证消息！
*.info;mail.none;authpriv.none;cron.none
/var/log/messages
# authpriv 文件受限制访问。
authpriv.*
/var/log/secure
# 将所有邮件记录在一个地方。
*.mail
/var/log/maillog
# 记录 cron 任务
cron.*
/var/log/cron
# 所有人都会接收紧急消息
*.emerg
# 将级别为 crit 和更高的新闻错误保存到特殊文件中。
uucp,news.crit
/var/log/spooler
# 将启动消息也保存到 boot.log
local.7.*
/var/log/boot.log
#
# INN
# news=-crit /var/log/news/news.crit
news=-err /var/log/news/news.err
news.notice /var/log/news/news.notice
[root@localhost]#
```

在 `/etc/syslog.conf` 文件中，任何以 `#` 字符开头的行都是注释。所有其他条目均具有以下格式：

`facility.priority /var/log/logfile`

`facility`（设施）是指要监听的系统区域，而 `priority`（优先级）指的是信息的严重程度。

例如，设施为 `kern` 优先级为 `warning` 表示系统日志守护进程应该监听内核消息、警告信息以及更严重的问题。当发现这些消息时，系统日志守护进程会将这些消息放在 `/var/log/logfile` 中。该条目将：

```
kern.warning /var/log/logfile
```

# 打印机和日志文件管理 11-19

你也可以将信息发送到远程 Linux 或 UNIX 上的 syslog 守护进程。请使用 `@servername` 代替 `/var/log/logfile`。

要仅将来自内核的警告消息记录到 `/var/log/logfile`，你可以使用：

```
kern.*=warning
/var/log/logfile
```

或者，你可以使用通配符将内核的所有错误消息记录到 `/var/log/logfile`：

```
kern.*=error
/var/log/logfile
```

你可以指定多个设施和优先级。要将来自内核的所有错误和警告记录到 `/var/log/logfile`，你可以使用以下条目：

```
kern.*!=warn
/var/log/logfile
```

要记录来自内核和守护进程的所有消息，你可以使用以下条目：

```
kern,news.*
/var/log/logfile
```

要记录除内核外所有设施的警告，可以使用 `"none"` 关键字，如所示：`kern;none`

```
*=none!=warn
/var/log/logfile
```

下表列出了可用的各种设施及其描述。

| 设施 (Facility) | 描述 (Description) |
|---|---|
| auth or security | 指定来自登录系统的消息，例如登录程序和 `su` 命令 |
| authpriv | 指定在跨网络或到系统数据库验证用户时来自登录系统的消息 |
| cron | 指定来自 `cron` 和 `at` 守护进程的消息 |
| daemon | 指定来自系统守护进程的消息，例如 `FTP` 守护进程 |
| kern | 指定来自 Linux 内核的消息 |
| lpr | 指定来自打印系统 (`lpd`) 的消息 |
| mail | 指定来自电子邮件系统 (`sendmail`) 的消息 |
| mark | 内部使用；syslog 指定时间戳 |
| news | 指定来自互联网新闻（INN）守护进程和其他 USENET 守护进程的消息 |
| syslog | 指定来自 syslog 的消息 |
| user | 指定来自用户进程的消息 |
| uucp | 指定来自 `uucp`（UNIX 到 UNIX 拷贝）守护进程的消息 |
| local0-7 | 指定本地消息。默认情况下不使用，但可以为自定义进行定义 |

# 11-20 CompTIA Linux+ 认证，2004 目标

下表按升序列出了各种可用的优先级。

| 优先级 (Priority) | 描述 (Description) |
| --- | --- |
| debug | 表示来自特定设施的所有信息 |
| info | 表示系统操作结果的正常信息消息 |
| notice | 表示为了以后参考应该注意的信息，但并未表示问题 |
| Warning or warn | 表示可能是错误导致的消息，但对系统操作至关重要 |
| error or err | 表示所有其他未由其他优先级描述的错误消息 |
| crit | 表示关键系统错误，例如硬盘故障 |
| alert | 表示应该立即修正的错误，例如损坏的系统数据库 |
| emerg or panic | 表示严重的系统状况，通常会广播给所有用户 |

# 管理日志文件

虽然日志文件包含重要的系统信息，但随着时间的推移，它们可能会占用文件系统中过多的空间。因此，定期清理日志文件的内容是非常重要的。

在清理日志文件之前，权限和所有权也会被移除。

注意：不要删除日志文件，因为权限和所有权会被移除。

要清理日志文件，请使用 `>` 符号。以下命令显示了 `/var/log/messages` 在清理前后的大小：

```
[root@localhost]# ls -l /var/log/messages
-rw-r--r-- 1 root 0 Jul 14 52 /var/log/messages
[root@localhost]# > /var/log/messages
[root@localhost]# ls -l /var/log/messages
-rw-r--r-- 1 root 0 Jul 14 52 /var/log/messages
[root@localhost]#
```

## 使用 logrotate 管理打印机和日志文件

你也可以使用 `cron` 守护进程调度打印和清理日志文件。或者，你可以调度 `logrotate` 工具来备份和清理 `/etc/logrotate.conf` 文件中的条目并存储在 `/logrotate.d` 目录。`logrotate` 命令通常按周期重命名文件。名为 `test.log` 的日志文件在第一次循环中重命名为 `test.1`，并创建一个新的 `test.log`。在第二个循环中，`test.1` 重命名为 `test.2`，`test.log` 重命名为 `test.1`。如果 `logrotate` 配置为只保留两个旧文件（如 `test.1` 和 `test.2`），则 `test.2` 在下一个循环中被移除。

`logrotate.conf` 文件的示例输出所示：

```
[root@localhost]# cat /logrotate.conf

# 查看 "man logrotate" 详情

# 轮转日志

weekly

# 保留 4 周的日志

rotate 4

# 创建（空的）日志文件

create

# 如果你想压缩日志文件

compress

# 将轮转信息放入此目录

include /logrotate.d

# 不使用 lastlog 或 wtmp - 我们在这里轮转

/var/log/wtmp {
```
