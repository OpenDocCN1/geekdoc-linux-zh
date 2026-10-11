
最后三个数字分别表示系统在过去一分钟（`2.91`）、过去五分钟（`1.59`）和过去十五分钟（`0.39`）的平均负载。

这些数字中的每一个表示有多少进程正在等待 CPU 资源或等待输入输出操作完成。这意味着如果这些进程拥有相应的资源，它们就准备好运行了。

# 系统日志与系统消息

一旦内核和进程开始执行并相互通信，就会产生大量信息。其中大部分被发送到文件中——所谓的日志文件（log files），或简单的日志（logs）。

如果没有日志，在服务器上搜索发生的事件会让系统管理员头疼，因此拥有一种标准化且集中的方式来跟踪任何系统事件至关重要。此外，在故障排除和安全方面，日志是决定性的，也是理解系统统计和进行趋势预测的可靠数据源。

# 使用 syslog 守护进程记录

传统上，系统消息由标准日志设施 `syslog` 或其任何变体——`syslog-ng` 或 `rsyslog` 管理。日志守护进程收集其他服务的并并存储在文件中，通常位于 `/var/log` 下。然而，某些服务会处理自己的日志（例如——Apache HTTP Web 服务器）。同样，Linux 内核使用内存中的环形缓冲区来存储其日志消息。

## /var/log 中的日志文件

因为日志是随时间变化的数据，它们通常在 `/var/log` 中。

如果你探索 `/var/log`，你会发现日志的名称在某种程度上是相当自而易懂的。示例包括：

### /var/log/auth.log

它存储关于身份验证的信息。

### /var/log/kern.log

它存储内核信息。

### /var/log/syslog

它存储系统信息。

### /var/log/messages

它存储系统和应用程序数据。

> 注意 日志文件的确切名称和内容可能随 Linux 发行版有所不同。

## 访问日志文件

探索日志文件时，记得使用 root 用户（如果你没有读取权限）并使用分页器，这样显示较少；

```
### less /var/log/messages

Jun 4 18:22:48 debian logging-bdlog: [origin software="rsyslogd" swVersion="8.24.0" x-pid="285" x-info="http://www.rsyslog.com"] rsyslog was HUPed

Jun 29 16:57:10 debian kernel: [ 0.000000] Linux version 4.9.0-amd64 (debian-kernel@lists.debian.org) (gcc version 6.3.0 20170516 (Debian 6.3.0-18-deb91)) #1 SMP

Debian 4.9.130-2 (2018-10-27)

Jun 29 16:57:10 debian kernel: [ 0.000000]Command line: BOOT_IMAGE=/boot/vmlinuz-4.9.0-amd64 root=/dev/sda ro quiet
```

或者，你可以使用 `tail` 配合 `-f` 来读取文件的最新消息，并在其更新时动态显示这些行：

```
### tail -f /var/log/messages

Jul 9 18:22:48 debian logging-bdlog: [origin software="rsyslogd" swVersion="8.24.0" x-pid="285" x-info="http://www.rsyslog.com"] rsyslog was HUPed

Jun 29 16:57:10 debian kernel: [ 0.000000] Linux version 4.9.0-amd64 (debian-kernel@lists.debian.org) (gcc version 6.3.0 20170516 (Debian 6.3.0-18-deb91)) #1 SMP

Debian 4.9.130-2 (2018-10-27)

Jun 29 16:57:10 debian kernel: [ 0.000000]Command line: BOOT_IMAGE=/boot/vmlinuz-4.9.0-amd64 root=/dev/sda ro quiet
```

```
[ 0.000000] Kernel command line: BOOT_IMAGE=/boot/vmlinuz-4.9.0-9-amd64

root=UUID=5216e1a4-4ae0-441f-b8f5-8061c0034c4 ro quiet

[ 0.144986] AppArmor: AppArmor disabled by boot time parameter

(...)
```

随着内核环形缓冲区随时间推移提供新消息，旧的消息将会逐渐消失。

## 注意

## 系统日志：systemd-journald

截至 2015 年，systemd 已取代了 SysV Init，成为大多数主流 Linux 发行版中事实上的系统和服务管理器。结果是，日志守护进程——journal——已成为标准的日志组件，在许多方面取代了 syslog。数据不再以明文形式存储，而是以二进制格式存储。因此，需要使用 `journalctl` 工具来读取日志。此外，journal 兼容 syslog 并可以与 syslog 集成。

`journalctl` 是读取和查询 systemd 日志的工具。如果不带选项调用，它将打印整个日志：

```
### journalctl

-- Logs begin at Tue 2019-06-04 17:49:40 CEST, and at Tue 2019-06-04 18:13:10 CEST. -

Jun 04 17:49:40 debian systemd-journal[339]: Runtime journal (/run/log/journal/) is 8.0M, max 159.6M, 159.6M free.

Jun 04 17:49:40 debian kernel: microcode updated to revision 0xccc, date = 2019-04-01

Jun 04 17:49:40 debian kernel: Linux version 4.9.0-8-amd64 (debian-kernel@lists.debian.org)

(gcc version 6.3.0-20170516 (Debian 6.3.0-18+deb9u1)) 1 SMP

Jun 04 17:49:40 debian kernel: Command line: BOOT_IMAGE=/boot/vmlinuz-4.9.0-8-amd64

root=/dev/sda ro quiet

(...)
```

如果带有 `-k` 或 `--dmesg` 切换调用，将等同于使用 `dmesg` 命令：

```
### journalctl -k

[ 0.000000] Linux version 4.9.0-8-amd64 (debian-kernel@lists.debian.org) (gcc version

6.3.0 20170516 (Debian 6.3.0-18+deb9u1) ) 1 SMP

[ 0.000000] Command line: BOOT_IMAGE=/boot/vmlinuz-4.9.0-9-amd64 root=UUID=5216e1a4-4ae0-441f-b8f5-8061c0034c4 ro quiet

(...)
```

# Linux 基础 (版本 1.6) | 主题 4: Linux 操作系统

`journalctl` 的其他有趣选项包括：

- `-b`, `--boot`

它显示启动信息。

- `-u`

它显示关于指定单元（unit）的消息。大致来说，单元可以定义为 systemd 处理的任何资源。例如，`journalctl -u apache2.service` 用于读取关于 apache2 Web 服务器的消息。

- `-f`

它显示最近的日志消息，并在新条目追加到日志时持续打印——类似于 `tail -f`。

## 引导性练习

1. 查看以下 `top` 的输出列表并回答以下问题：

```
carol@debian:~$ top

top - 13:39:16 31 min, 1 user, load average: 0.12, 0.15, 0.10

Tasks: 73 total, 2 running, 71 sleeping, 0 stopped, 0 zombie

%(Cpu): 1.1 us, 0.4 sy, 98.6 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st

KiB Mem: 1020232 total, 698700 free, 170664 used, 150968 buff/cache
```
