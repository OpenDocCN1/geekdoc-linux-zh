
查看 `/usr/share/logwatch/default.conf/logwatch.conf` 其他需要更改的设置（例如默认级别或每份报告的时间范围）。然后按照提到的在 `/etc/logwatch/conf/logwatch.conf` 中添加你的配置。

当服务被启用时（只需安装 logwatch 软件包即可启用），你每晚都会在 root 用户的邮箱中看到一条消息。当你以 root 身份登录时，可以使用旧命令查看 root 用户的邮箱：

```bash
# mail
Heirloom Mail version 12.5 7/5/10. Type ? for help.

"/var/spool/mail/root": 2 messages 2

>N 1 logwatch@abc.ex Sun Feb 15 04:02 45/6664 "Logwatch for abc"
2 logwatch@abc.ex Mon Feb 16 04:02 45/6664 "Logwatch for abc"
```

在 `mail` 中，你每天都应该看到来自 logwatch 的邮件（此处为每天凌晨 4:02）。输入你想查看的消息编号，并使用空格键翻页或按回车键逐行查看。完成后输入 `x` 退出。

你看到的信息类型包括内核错误、已安装的软件包、身份验证失败以及运行出现故障的服务。系统会报告磁盘使用情况，以便你可以查看存储空间是否正在填满。只需扫一眼这条 logwatch 消息，你就应该大致知道是否正在遭受攻击或是否发生了某些重复的失败。

## 使用 sar 检查系统资源

系统活动报告器 (`sar`) 是为早期 UNIX 系统创建的最古老的系统监控设施之一——比 Linux 早了几十年。`sar` 命令本身可以以间隔（每秒或每两秒）连续显示系统活动并显示在屏幕上。它还可以显示之前收集的活动数据。

`sar` 命令使用 sysstat 软件包。通过安装 sysstat 并启用 sysstat 服务，你的系统开始收集活动数据，可以使用 `sar` 命令的某些选项来检查这些数据。数据收集由一个定期启动的 crontab 文件 (`/etc/cron.d/sysstat`) 完成。查看该文件发现包含：

```bash
# cat /etc/cron.d/sysstat
# 每 10 分钟运行一次系统活动统计工具
*/10 * * * * root /usr/lib64/sa/sal 1 1
# 0 * * * root /usr/lib64/sa/sal 600 6 *
# 在 23:53 生成进程计费的每日摘要
53 23 * * * root /usr/lib64/sa/sa2 -A
```

第一行每 10 分钟运行一次 `sa1` 命令。该命令收集一次系统活动范围（等待 1 秒后一次），并将其复制到 `/var/log/sa/sar` 文件，其中 `??` 被替换为当前日期。`sa -A` 命令收集当天到此为止（晚上 11:23）的所有数据，并将其放在 `/var/log/sa/sar??` 文件中，其中 `??` 被替换为当前日期。

要读取 `sar??` 和 `sar` 文件中的数据，可以使用以下命令：

```bash
# sar -u | less
Linux 3.10.0-123.el7.x86_64 (rhel7-0) 4/16/2017 _x86_64 (4 CPU)
12:00:01 AM %user %system %iowait %idle
12:10:01 AM all 6.48 0.00 0.82 0.59 0.00 92.12
12:20:01 AM all 6.50 0.00 0.78 0.82 0.00 91.99
```

`-u` 显示 CPU 使用率。默认情况下，输出从当天开始，显示系统不同部分消耗的时间。输出将持续到当前时间。要查看活动，请运行 `sar -d`。同样，输出从午夜开始：

```bash
# sar -d | less
Linux 3.10.0-123.el7.x86_64 (rhel7-0) 4/16/2017 _x86_64 (4 CPU)
12:00:01 AM dev tps rd_sec/s wr_sec/s avq-sz cu-sz
12:00:01 AM dev0 0.00 0.00 0.00 0.00 0.00
12:00:01 AM dev-8 1.39 0.24 18.49 13.34 0.04
12:00:01 AM dev-3 0.29 0.00 0.24 18.49 7.24
```

如果你运行 `sar` 报告，可以通过向命令中添加计数和时间间隔：

```bash
# sar -n DEV
Linux 3.10.0-123.el7.x86_64 (rhel7-0) 4/16/2017 _x86_64 (4 CPU)
12:19:36 PM IFACE rpcck/s tpxck/s rxkB/s tkkB/s rxcmp/s txcmp/s
12:19:41 PM lo 5.42 5.42 1.06 1.00 0.00
12:19:41 PM eth0 0.00 0.00 0.00 0.00 0.00
12:19:41 PM wlan0 1.00 1.00 0.12 0.00 0.00
12:19:41 PM pan0 0.00 0.00 0.00 0.00 0.00
12:19:41 PM tun0 0.00 0.00 0.00 0.00 0.00
```

| Average: IFACE | rpcck/s | tpxck/s | rxkB/s | tkkB/s | rxcmp/s | txcmp/s |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| lo | 7.21 | 7.21 | 1.42 | 1.40 | 0.00 | 0.00 |
| eth0 | 0.00 | 0.00 | 0.00 | 0.00 | 0.00 | 0.00 |
| wlan0 | 4.70 | 4.00 | 4.81 | 0.63 | 0.00 | 0.00 |
| pan0 | 0.00 | 0.00 | 0.00 | 0.00 | 0.00 | 0.00 |
| tun0 | 3.70 | 2.90 | 0.42 | 0.19 | 0.00 | 0.00 |

通过显示的 `-n Dev`，你可以看到系统上不同接口的活动情况。你可以看到传输了多少数据包以及传输和接收了多少 KB 数据。例如，每 5 秒采集一次数据样本并重复。有关如何收集和显示 sar 数据，请参考 `sar`、`sadc`、`sal` 和 `sa2` 页面。

## 检查系统空间

虽然 watch 可以提供系统磁盘消耗的每日快照，但 `df` 和 `du` 命令可以帮助你立即查看可用磁盘空间。以下章节显示了这些命令的示例：

### 第四部分：成为 Linux 服务器管理员

#### 使用 df 显示空间使用情况

你可以使用 `df` 命令显示文件系统的可用空间。要查看 Linux 计算机上所有挂载文件系统的可用空间，请输入不带选项的 `df`：

```bash
$ df
Filesystem      1k-blocks      Used  Available  Use%  Mounted on
/dev/sda3     30645460   2958356 26130408     11%       /
/dev/sda2        46668          8340     35919     19%     /boot
```

此示例显示了挂载在 `/root` 目录 (`/dev/sda1`) 和启动分区 (`/dev/sda2`) 的硬盘分区上的可用空间。磁盘空间以 1KB 块显示。为了以更符合人类习惯的格式产生输出，请使用 `-h` 选项：

```bash
$ df -h
Filesystem      Size  Avail  Use%  Mounted on
/dev/sda3       29G    2.9G    24G    11%       /
/dev/sda2       46M     8.2M    35M    19%     /boot
```

使用 `-h` 选项后，输出将以更友好的兆字节或字节列表显示。`df` 的选项允许你执行以下操作：

- 仅打印特定类型的文件系统 (`-t type`)。
- 排除特定类型的文件系统 (`-x type`)。例如，输入 `df -x tmpfs -x devtmpfs` 以排除临时文件系统类型（限制到代表根存储区域的 devtmpfs）。
- 包含空间的文件系统，例如 `/proc` 和 `/dev/pts` (`-a`)。
- 仅列出可用和使用的 inode (`-i`)。
- 以特定的块大小显示磁盘空间 (`--block-size=#`)。

### 第 13 章：理解服务器管理

```bash
$ du -h /home/jake
114k /home/jake/httpd
234k /home/jake/uucp/data
137M /home/jake/uucp
```
