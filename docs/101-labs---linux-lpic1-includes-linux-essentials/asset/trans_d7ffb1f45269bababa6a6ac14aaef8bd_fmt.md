
## 实验 79

### 维护系统时间：NTP

**实验目标：**

学习如何维护系统时间，并使用 NTP 同步时钟。

**实验目的：**

在本实验中，你将了解经典的网络时间协议（NTP）及其用于同步系统时钟的设置。

**实验工具：**

Ubuntu 18.04（或其他你选择的发行版）

**实验拓扑：**

单台 Linux 机器，或虚拟机

**实验步骤：**

**任务 1：**

打开终端并运行：`sudo apt install ntp ntpdate`

现在使用以下命令查看主要的 NTP 配置文件：`cat /etc/ntp.conf`

NTP 通过树形拓扑同步时间——你的实验机器从一个特定于发行版的服务器池获取时间，该池由“pool”指定（例如，`ubuntu.pool.ntp.org`）。Ubuntu 自己的服务器从某些上游源获取时间，依此类推，直到全球实验室中的原子钟系统。

**任务 2：**

现在运行：

- `sudo systemctl stop ntp.service`
- `sudo ntpdate ntp.ubuntu.com`

（当然，你可以使用不同的时间服务器来代替 `ntp.ubuntu.com`。）

几秒后，你应该会看到输出，表明 `ntpdate` 已更新系统时间，并记录时间来源及偏移调整值。

`ntpdate` 可用于在每次启动时更新系统时间，有时是在 `ntpd`（NTP 守护进程）接管之前，或者用于在通常互联网访问受限或无互联网访问的服务器上手动同步时间。除此之外，建议使用 `ntpd` 而不是通过 `cron` 运行 `ntpdate`。

**备注**

`ntpq` 是一个主要用于调试的命令，可用于向 NTP 服务器查询各种信息。

## 实验 80

### 维护系统时间：Chrony

**实验目标：**

学习如何维护系统时间，并使用 Chrony 同步时钟。

**实验目的：**

在本实验中，你将了解 Chrony，这是 NTP 的一种较新的实现，及其用于同步系统时钟的设置。

**实验工具：**

Ubuntu 18.04（或其他你选择的发行版）

**实验拓扑：**

单台 Linux 机器，或虚拟机

**实验步骤：**

**任务 1：**

打开终端并运行：

- `sudo apt install chrony`
- `sudo systemctl start chrony`

现在使用以下命令查看主要的 Chrony 配置文件：`cat /etc/chrony/chrony.conf`

你应该能认出它与实验 79 中 NTP 配置文件的一些相似之处。

**任务 2：**

现在运行 `sudo chronyc`。你将进入交互式提示符。你现在可以实验 `chronyc` 工具：

- `tracking`
- `activity`
- `ntpdata`

在此提示符处运行 `help` 以查看你可以做的事情的列表，或运行 `quit` 退出。

与 `ntpdate` 相比，chrony FAQ 页面指出：“如果你的计算机每次只连接互联网几分钟，网络连接经常拥塞，你经常关闭或暂停计算机，时钟不是很稳定（例如温度变化快或它是虚拟机），或者你想在没有硬件参考时钟的隔离网络上使用 NTP，`chrony` 可能更适合你。”

**备注：**

`hwclock` 可用于检查硬件时间，它不一定与系统时间相同（特别是当硬件时钟使用不同时区时）。运行 `sudo hwclock` 后接着运行 `date`——它们一致吗？

Chrony FAQ 页面的网址是：

https://chrony.tuxfamily.org/faq.html#_how_does_code_chrony_code_compare_to_code_ntpd_code

## 实验 81

### 系统日志：Rsyslog

**实验目标：**

学习如何配置 `rsyslog` 日志守护进程。

**实验目的：**

在本实验中，你将了解 `rsyslog` 的基本配置及其不同的日志记录选项。

**实验工具：**

Ubuntu 18.04（或其他你选择的发行版）

**实验拓扑：**

单台 Linux 机器，或虚拟机

**实验步骤：**

**任务 1：**

打开两个终端窗口/选项卡。

在第一个中运行：`tail -f /var/log/syslog`

在第二个中运行：`logger "Hello World"`

现在回到第一个选项卡。你的友好信息出现在系统日志中了吗？按 Ctrl+C 退出 `tail`。

> `logger` 是一个通用实用程序，用于向日志记录守护进程（包括 `rsyslog` 和我们在实验 83 中讨论的 `journal`）发送日志。

**任务 2：**

现在查看配置：

```bash
grep -v -e ^# -e ^$ /etc/rsyslog.conf /etc/rsyslog.d/*
```

这可能因发行版而异——一旦你找到正确的文件，你可能希望用文本编辑器打开它们。

最终，你要寻找像 `50-default.conf` 或类似的文件，它定义了哪些设施记录到哪些文件。在 Ubuntu 上，此文件应包含如下一行：

```
auth,authpriv.* /var/log/auth.log
```

在此文件顶部添加以下行：

```
*.* /var/log/allthelogs
```

然后重启守护进程：`systemctl restart rsyslog`

等待几分钟（或使用 `logger` 创建自己的日志），然后检查 `/var/log/allthelogs` 的内容。这应该是正在写入许多其他日志文件的所有日志的混合体。

**任务 3：**

通过删除你添加到 `rsyslog` 配置中的行来清理，并运行 `systemctl restart rsyslog`

**备注：**

除了大多数发行版因 Systemd 而迁移使用的 `journald` 外，还有其他日志守护进程，如 `syslog` 和 `syslog-ng`。虽然一些守护进程有自己的配置格式，但所有至少都支持经典的 `syslog` 配置格式（这应该就是你之前在 `rsyslog` 自己的配置中看到的内容）。学习该格式，你就已经学习了所有主要日志守护进程的配置。

## 实验 82

### 系统日志：Logrotate

**实验目标：**

学习如何配置 logrotate 以轮换系统日志。

**实验目的：**

logrotate 是一个常用的工具，用于轮换日志，即每隔 X 天/周归档一次，每隔 Y 周/月删除一次。在本实验中，你将学习如何配置它。

**实验工具：**

Ubuntu 18.04（或其他你选择的发行版）

**实验拓扑：**

单台 Linux 机器，或虚拟机

**实验步骤：**

**任务 1：**

打开终端并运行 `cat /etc/logrotate.conf`

这是主要的 logrotate 配置文件，包含默认指令。你可能会看到像这样的行：

```
weekly
rotate 4
create
```

结合这些行，它们将每周保存某个日志文件的归档，保留每个归档四周，并在轮换旧文件后创建一个新空日志文件。

此外，你很可能有一个名为 `/etc/logrotate.d` 的目录，其中存储了一些特定于包的配置。Ubuntu 有一个用于 apt，因此查看 `/etc/logrotate.d/apt`，或你选择的另一个文件。

你可能会在这里看到像 `rotate 12`（保留 12 周而不是 4 周，如果包含 `monthly` 则为 12 个月）、`compress` 用于压缩归档，或 `notifempty` 用于忽略空日志等指令。

有关更多详细信息，请参见 `man logrotate`。

**任务 2：**

现在，使用 `sudo`（或 `sudoedit`）打开文本编辑器，创建一个名为 `/etc/logrotate.d/mylog` 的文件，内容如下：

```
/var/log/mylog.log {
    hourly
    su root syslog
    rotate 2
    create
    compress
    missingok
}
```

然后：`sudo touch /var/log/mylog.log`

通常，你必须至少等待一小时才能看到任何轮换发生，但你可以通过 `-f` 开关强制这种情况发生。运行：

- `sudo logrotate -fv /etc/logrotate.d/mylog`
- `ls -al /var/log/mylog*`

你应该会看到原始文件的压缩归档，作为 `mylog.log.1.gz`，以及一个名为 `mylog.log` 的新日志。再运行第一个命令两次。第二次运行时将创建第二个归档文件，但在第三次运行时，你应该在底部看到一行“removing old log /var/log/mylog.log.3.gz”，这符合配置文件。

**任务 3：**

最后，清理：`sudo rm /etc/logrotate.d/mylog /var/log/mylog*`

**备注：**

通常，`logrotate` 通过每日 cron 作业运行。你能找到你的系统上配置此 cron 作业的位置吗？（提示：参见实验 75！）
