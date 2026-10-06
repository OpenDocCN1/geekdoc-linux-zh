

# 高级 Bash 脚本指南

| 设备 | DMA | IRQ | I/O 端口 |
| --- | --- | --- | --- |
| cascade | 4 | | |
| dma | | | 0080-008f |
| dmal | | | 0000-001f |
| dma2 | | | 00c0-00df |
| fpu | | | 00f0-00ff |
| ide0 | 14 | | 01f0-01f7 03f6-03f6 |

递归地显示磁盘文件使用情况。除非有指定，否则默认为当前工作目录。

```bash
bash du -ach
1.0k /wi.sh
1.0k /tst.sh
1.0k /random.file
6.0k
6.0k total
```

以表格格式显示文件系统使用情况。

| 文件系统 | 1k-块 | 已用 | 可用 使用率 | 挂载点 |
| --- | --- | --- | --- | --- |
| /dev/hda5 | 273262 | 92607 | 166547 | 36% | / |
| /dev/hda8 | 222525 | 123951 | 87085 | 59% | /home |
| /dev/hda7 | 1408796 | 1075744 | 261488 | 80% | /usr |

对给文件（设备或设备文件）或一组文件提供详细的统计信息。

```bash
bash stat test.cru
File: "test.cru"
Size: 49970 Allocated Blocks: 100 Filetype: Regular File
Mode: (0664/-rw-rw--) Uid: (501/bozo) Gid: (501/bozo)
Device: 3,8 Inode: 18185 Links: 1
Access: Sat Jun 2 16:40:24 2001
Modify: Sat Jun 2 16:40:24 2001
Change: Sat Jun 2 16:40:24 2001
```

如果目标文件不存在，stat 会返回错误消息。

```bash
bash stat nonexistent-file
nonexistent-file: No such file or directory
```

显示虚拟内存统计信息。

```bash
bash vmstat
procs memory swap io system cpu
r b w swpd free buff cache si so bo in cs us sy id
```

第 13 章。系统与管理命令

# 高级 Bash 脚本指南

显示当前的网络统计和信息，例如路由表和活动连接。此实用程序访问 /proc/net（第 28 章）。请参见示例 28–2。

**netstat -r** 等同于 route。

显示系统运行的时间以及相关的统计数据。

```bash
bash uptime
10:28pm up 1:57, 3 users, load average: 0.17, 0.34, 0.27
```

列出系统的主机名。此命令在 /etc/rc.d 设置脚本中（/etc/rc.d/rc.sysinit 或类似文件）设置主机名。它等同于 uname -n，是内部变量 HOSTNAME 的对应项。

```bash
bash hostname
localhost.localdomain

bash echo $HOSTNAME
localhost.localdomain
```

输出主机的 32 位十六进制标识符。

```bash
bash hostid
7f0100
```

该命令据称为特定系统获取“唯一的”序列号。某些产品注册程序使用此数字来标记特定的用户许可。遗憾的是，hostid 仅以十六进制返回网络地址，且字节对发生了转置。

典型的非网络化 Linux 机器的网络地址可以在 /etc/hosts 中找到。

```bash
$ cat /etc/hosts             localhost.localdomain localhost
127.0.0.1
```

转置 127.0.0.1 的字节时，我们得到 0.127.1.0.，这在十六进制中翻译为 007f0100，与上述 hostid 返回的结果完全相同。具有此相同 hostid 的 Linux 机器仅存几百万。

第 13 章。系统与管理命令

# 调用 sar–脚本指南

sar（系统活动报告）提供了系统统计的详详细概述。此命令于某些商用 UNIX 系统，但不是 Linux 发行版的一部分。它包含在 Sebastian Goddard 编写的 sysstat 包中。

```bash
$ sar
Linux 2.4.7-10 (localhost.localdomain)   12/31/2001

10:30:01 AM    CPU     %user    %nice    %system  %idle
10:40:00 AM    all     1.39    0.00     0.77    97.84
10:50:00 AM    all     76.83   0.00     1.45    21.72
11:00:00 AM    all     1.32    0.00     0.69    97.99
11:10:00 AM    all     1.17    0.00     0.30    98.53
11:20:00 AM    all     1.51    0.00     0.30    99.19
06:30:00 PM    all     100.00  0.00    100.01   0.09
Average:               1.39    0.00     0.66    97.95
```

# 系统日志

logger

将用户生成的消息添加到系统日志（/var/log/messages）。调用 logger 不需要 root 权限。

```bash
logger Experiencing instability in network connection at 23:10, 05/21.
# No, do a 'tail /var/log/messages'.
```

在脚本中嵌入 logger 可以向 /var/log/messages 写入调试信息。

```bash
logger Experiencing instability in network connection at 23:10, 05/21.
# No, do a 'tail /var/log/messages'.
```

