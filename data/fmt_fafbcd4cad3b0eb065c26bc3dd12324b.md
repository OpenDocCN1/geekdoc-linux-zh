
- `mailto` = `root`

- `range` = `yesterday`

- `detail` = `low`

- `service` = `all`

这些选项对应于以下命令调用 `logwatch`：

```
# logwatch --mailto root --range yesterday --detail low --service all
```

`LogWatch` 使用了一组同样用 Perl 编写的过滤器，用于从 Red Hat 上的各种日志文件中提取信息。这些过滤器存储在三个独立的目录中：

- `/etc/log.d/scripts/shared` – 针对许多服务和/或日志文件的过滤器。
- `/etc/log.d/scripts/logfiles` – 专门针对特定日志文件的过滤器。
- `/etc/log.d/scripts/services` – 各种服务的实际过滤器程序。

`LogWatch` 可以报告的服务列表可以通过查阅 `/etc/log.conf/services` 中的文件列表来确定，该文件包含了定义 `LogWatch` 如何处理相应日志条目的配置文件。`LogWatch` 目前处理以下列表所示服务的日志条目：

| | kernel | samba |
| :--- | :--- | :--- |
| cron | modprobe | secure |
| ftpd-messages | mountd | sendmail |
| ftpd-xferlog | named | sshd |
| identd | pam | sshd2 |
| in.qpopper | pam_pwdb | syslog |
| init | proftpd-messages | | |

`LogWatch` 报告的信息类型随服务而异，取决于提供给 `--detail` 选项的参数。例如，为 `sendmail` 服务生成的日志信息对于所有 `--detail` 的取值来说都是相同的：

```
# logwatch --service sendmail --detail low --range today --print
############################ LogWatch 2.1.1 Begin ############################
```

```
sendmail Begin
641360 bytes transferred
81 messages sent
sendmail End
```

```
#################### LogWatch End ####################
# logwatch --service sendmail --detail high --range today --print

#################### LogWatch 2.1.1 Begin #######################
```

```
sendmail Begin
641360 bytes transferred
81 messages sent
sendmail End
```

```
#################### LogWatch End ####################
```

如你所见，`LogWatch` 对低细节（`low`）和高细节（`high`）报告的是相同的数据：`sendmail` 处理的字节总数和它发送的消息数。然而，内核（`kernel`）服务的情况则不同，如下：

![](img/8c5ce181a0f26bec693ad7f04bbfb6fe_925_0.png)

你可以使用 `mailstats` 命令获取有关邮件流量的更详细信息。为了使用它，请确保文件 `/var/log/sendmail.st` 存在。如果不存在，请以 `root` 用户执行 `touch /var/log/sendmail.st`。

```
# logwatch --service kernel --detail low --range today --print
###################### LogWatch 2.1.1 Begin #################
```

```
#################### LogWatch End ####################
# logwatch --service kernel --detail high --range today --print
###################### LogWatch 2.1.1 Begin #################
```

```
Kernel Begin
```

4 Time(s): Directory search (sector 0x17) failed

2 Time(s): end_request: I/0 error, dev 02:00 (floppy), sector 19

5 Time(s): end_request: I/0 error, dev 02:00 (floppy), sector 23

1 Time(s): end_request: I/0 error, dev 02:00 (floppy), sector 24

# 第 32 章：检测与防止入侵

```
1 Time(s): end_request: I/O error, dev 02:00 (floppy), sector 26
1 Time(s): end_request: I/O error, dev 02:00 (floppy), sector 364
1 Time(s): end_request: I/O error, dev 02:00 (floppy), sector 372
1 Time(s): end_request: I/O error, dev 02:00 (floppy), sector 373
1 Time(s): end_request: I/O error, dev 02:00 (floppy), sector 400
1 Time(s): end_request: I/O error, dev 02:00 (floppy), sector 404
1 Time(s): floppy0: CRC error: track 0, head 1, sector 5, size 2
1 Time(s): floppy0: CRC error: track 0, head 1, sector 9, size 2
1 Time(s): data CRC error: track 0, head 1, sector 17, size 2
4 Time(s): floppy0 data CRC error: track 0, head 1, sector 2, size 2
1 Time(s): floppy0 data CRC error: track 0, head 1, sector 6, size 2
1 Time(s): floppy0 data CRC error: track 0, head 1, sector 7, size 2
2 Time(s): floppy0 data CRC error: track 0, head 1, sector 9, size 2
1 Time(s): floppy0: sector not found: track 0, head 1, sector 2, size 2
1 Time(s): floppy0: sector not found: track 0, head 1, sector 3, size 2
1 Time(s): floppy0: sector not found: track 0, head 1, sector 5, size 2
10 Time(s): floppy0: sector not found: track 0, head 1, sector 6, size 2
1 Time(s): floppy0: sector not found: track 0, head 1, sector 7, size 2
Kernel End

```

########################### LogWatch ###########

`LogWatch` 在细节级别为高（`high`）时的输出表示磁盘驱动器开始故障。要从 `LogWatch` 中获得收益，请将 `/etc/logwatch.conf` 中的默认细节级别更改为高。

# 使用 ipchains 检测入侵

基于 `ipchains` 或 `iptables` 精心设计的安全策略是安全中最强大的层级之一。本节介绍了如何使用 `ipchains` 配置防火墙。单用 `ipchains` 无法检测入侵，但结合 `LogWatch`，可以确定是哪种黑客在尝试、频率如何以及在哪些端口。使用 `ipchains` 检测入侵的关键是使用其 `-l` 选项让内核记录匹配规则的数据包。虽然通常会记录所有包，但记录被拒绝的包是了解进入系统的流量的一种非常有用的方法。例如，假设你有如下规则：

```
# ipchains -l -A forward -i ppp0 -j DENY
```
