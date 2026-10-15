
`00 4 1 * * ~/maintenance.pl`

### 本地日志文件分析

11. `/etc/rsyslog.conf` 文件中有一个注释条目满足问题的要求。只需激活它，即可在内核出现严重问题时通知您（以及所有人）：

```
kern.*    /dev/console
```

当然，这意味着还有其他可接受的方式来满足问题的要求。

12. 与安装过程最相关的 `/var/log` 中的日志文件以 `anaconda` 开头。

## 实验答案

### 实验 1

修改登录消息的一种方法如下（我还能想到至少一种其他方法，与 `/etc/cron.d` 目录相关）：

1. 以 `root` 用户身份登录。
2. 运行 `crontab -e` 命令。
3. 添加适当的环境变量，至少包括以下内容：
   `SHELL=/bin/bash`
4. 在适当的时间添加以下命令到文件中以覆盖 `/etc/motd`：

```
0 7 * * * /bin/echo 'Coffee time!' > /etc/motd

0 13 * * * /bin/echo 'Want some ice cream?' > /etc/motd

0 18 * * * /bin/echo 'Shouldn't you be doing something else?' > /etc/motd
```
5. 保存文件。只要 `cron` 守护进程处于活动状态（默认情况下是如此），在指定时间之一之后登录到控制台的下一个用户在成功登录时应看到该消息。如果您想立即测试结果，`date` 命令可以帮助您。例如，以下命令
`# date 06120659`
将日期设置为 6 月 12 日上午 6:59，就在 `cron` 守护进程应执行列表中第一个命令之前。（当然，您需要替换为今天的日期，并在从另一控制台登录此系统之前等待一分钟。）

### 实验 2

要设置一个 24 小时后开始的 `at` 作业，请从 `at` 命令开始。它会带您进入 `at>` 提示符。

当前安装的 RPM 包显示在 `rpm -qa` 命令的输出中。由于在 `at>` 提示符下没有给出 `PATH`，您应包含完整路径。因此，创建 `cur-` 列表的一种方法是

将当前已安装的 RPM 包记录到 `/root/rpms.txt` 文件中，从现在起五分钟后开始的一次性任务，可使用以下命令：

```
# at now + 5 min

at> /bin/rpm -qa > /root/rpms.txt

at> Ctrl+d

#
```

五分钟内，你应该能在 `root` 用户的主目录 `/root` 中看到 `rpms.txt` 文件。如果五分钟等待时间太长（如 RHCSA 考试期间），请先进行 Lab 3，之后再回来处理此问题。不要忘记设置另一个在 24 小时后运行的 `at` 任务。

## Lab 3

根据本书迄今为止讨论的硬件，远程 VNC 服务器的成功配置只能间接确认。然而，如果你有一台安装了 RHEL 的第二台物理系统，远程确认 VNC 服务器的可用性并不困难。例如，如果 VNC 服务器可在 `192.168.122.200` 系统上找到，在第二个终端上，你可以使用 `vncviewer 192.168.122.200:2` 命令连接到该 VNC 服务器。

## Lab 4

本实验没有秘密解决方案；其目的是让你查看关键日志文件的内容，看看其中应包含什么。

当你查看 `/var/log` 中的 `anaconda.*` 文件并将其与其他文件进行比较时，你可能会获得一些诊断安装问题的见解。在今后的章节中，你将检查与特定服务相关的一些日志文件；其中许多位于 `/var/log/samba/` 和 `/var/log/httpd/` 等子目录中。

失败的登录应该在 `/var/log/secure` 文件中很容易显现。你可能能在 `utmpdump btmp` 命令的输出中获得提示。

当你查看 `/var/log/cron` 文件时，你会看到标准 `cron` 作业的运行时间。默认情况下，该文件的大部分内容应由 `/etc/crontab` 配置文件中的标准每小时作业 `run-parts /etc/cron.hourly` 填充。如果已重新启动，你可能会看到 `anacron` 服务，并且应该能够搜索同名作业。

虽然 `/var/log/dmesg` 包含当前启动的内核，但如果未升级内核，它可能与 `/var/log/anaconda/syslog` 关联的内核相同。在 `/var/log/dmesg` 的末尾，你可以找到格式化为 EXT4 的文件系统，以及当前挂载的交换分区。例如，以下列出了基于 KVM 的虚拟驱动器的分区：

```
EXT4-FS (vda1): mounted filesystem with ordered data mode.

SELinux: initialized (dev vda1, type ext4), uses xattr
```

```
EXT4-FS (vda5): mounted filesystem with ordered data mode.

SELinux: initialized (dev vda5, type ext4), uses xattr

Adding 1023992k swap on /dev/vda3. Priority:-1 extents:1 across:979956k
```
