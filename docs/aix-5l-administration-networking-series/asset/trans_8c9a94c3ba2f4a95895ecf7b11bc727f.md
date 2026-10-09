

# 显示统计数据

随时都可以通过命令行对系统进行“把脉”，或者回顾账户统计历史。你还可以将标准输出重定向到文件，从而创建临时（ad hoc）报告。使用 **sa** 命令可以显示存储在 `/var/adm/pacct` 中的数据的通用摘要。**sa** 命令支持许多标志，可用于过滤和限制输出。其中两个最实用的标志是 **-m** 标志，它按用户进行摘要；以及 **-s** 标志，它按命令进行摘要。** -s** 标志还可以用于将摘要合并到现有的历史文件中。

```sh
# sa -m

root     766    0.75cpu   77743653tio    11532k*sec
daemon     8    0.02cpu    663334tio    848k*sec
adm        75    0.07cpu    1242340tio    747k*sec
cps        36    0.29cpu    3810811tio    7740k*sec
nobody      15    0.14cpu    4890509tio    26791k*sec
```

```sh
# sa -s | head -7

900   17008.96re    1.28cpu    98167avio     6k
6       0.39re     0.39cpu   10289152avio    3k   egrep
6      2060.74re    0.23cpu    471744avio     5k   xterm
3       0.15re     0.13cpu    1566208avio    33k   da_rslt
17     2850.94re    0.13cpu    51509avio     3k   ksh
47      2944.44re    0.07cpu    44984avio     3k   other
30       0.07re     0.03cpu    13452avio     3k   awk
```

可以使用 BSD 的 `ac` 和 `last` 命令来显示连接历史记录。`ac` 命令可以按天或按 `/var/adm/wtmp` 文件涵盖的时间区间来汇总连接时长。`last` 命令可用于显示所有用户或单个用户的登录时间。

```sh
# /usr/sbin/acct/ac -p | awk '{print $1 " " $2}'
duan e 0.46
deroest 264.16
don n 487.54
n oyd 9961.55
```

```sh
# /usr/sbin/acct/ac -d
Sep 01 total 269.68
Sep 02 total 613.75
Sep 03 total 914.32
```

```sh
# last -4
cps pts/92 xtreme.sar.washi Fri Sep 17 10:41 still logged in
don pts/82 tiab1.bnn.washin Fri Sep 17 10:07 still logged in
kenn pts/75 192.168.90.125 Fri Sep 17 10:00 - 10:22 (00:21)
davldw pts/56 redy.aal.washing Fri Sep 17 08:23 still logged in
```

可以使用 BSD 的 `lastcomm` 命令生成详尽的命令使用情况信息。与 `ac` 一样，该命令也支持大量标志来过滤输出。请注意，调用该命令时也会消耗大量的系统资源！

```sh
# lastcomm | sed 's/  */ /g'
acctwtmp S root --- 0.02 secs Fri Sep 17 23:44
httpd F nobody --- 0.05 secs Fri Sep 17 13:50
tftpd S root --- 0.69 secs Fri Sep 17 11:28
tftpd F nobody --- 0.01 secs Fri Sep 17 11:28
nfssrv S root --- 0.01 secs Fri Sep 17 23:44
ksh F root pts/0 --- 0.01 secs Fri Sep 17 23:44
whoami S root pts/0 --- 0.03 secs Fri Sep 17 23:44
termdef S root pts/0 --- 0.03 secs Fri Sep 17 23:44
sh S adm pts/1 0.28 secs Fri Sep 17 22:02
```

# 摘要报告

`runacct` 和 `monacct` 命令会定期生成一组标准报告。这些命令应由 adm crontab 运行。摘要和报告记录在以下目录中：

| 目录 | 描述 |
| :--- | :--- |
| `/var/adm/acct/nite` | runacct 使用的每日文件 |
| `/var/adm/acct/sum` | runacct 创建的每日摘要 |
| `/var/adm/acct/fiscal` | monacct 创建的每月摘要 |

报告和数据文件包括：

- `nite/accterr` ←— runacct cron/tac 作业的错误日志（ASCII）
- `nite/active` ←— runacct 的进度报告（ASCII）
- `nite/active` [mndd] ←— runacct 的上一次进度报告（ASCII）
- `nite/cms` ←— prdaily 使用的命令总摘要（ASCII）
- `nite/ctmp` ←— 连接会话记录（ASCII）
- `nite/dacct` ←— 每个用户的每日使用记录（tacct）
- `nite/dayacct` ←— 全天会计记录总计（tacct）
- `nite/daycms` ←— prdaily 使用的每日命令摘要（ASCII）
- `nite/lastdate` ←— 限制 runacct 每天只运行一次（ASCII）
- `nite/linuse` ←— 会话记录（ASCII）
- `nite/oxtmp` ←— 上一次系统的 wxtmp 数据（tacct）
- `nite/reboots` ←— 会计期间的会话报告（ASCII）
- `nite/statefile` ←— runacct 的过程入口点（ASCII）
- `nite/wtmperror` ←— runacct 的 wxtmp/lix 错误消息（ASCII）

- `sum/cms` ←— 每月清除前的命令摘要（tacct）
- `sum/cmsprev` ←— 更新前的命令摘要（tacct）
- `sum/daycms` ←— 每日命令摘要（tacct）
- `sum/logilog` ←— 每个已使用 ID 的最后一条记录（ASCII）
- `sum/xrpt` [mndd] ←— prdaily 命令的输出（ASCII）
- `sum/tacct` ←— 清除前的总期间会计数据（tacct）

- `fiscal/cms` [mm] ←— 会计命令摘要（tacct）
- `fiscal/fiscrpt` [mm] ←— 会计总报告（ASCII）
- `fiscal/tacct` [mm] ←— 会计总会计摘要（tacct）

# 性能工具

以下是随 Accounting Services 附带的一些有助于评估性能的工具，以及它们使用方法的简短示例。

`vstat` 命令报告有关内核线程、内存、磁盘 I/O、陷阱和处理器活动的信息。AIX 5L 等新版本的命令行选项增加了面向 I/O 的输出，每行包含三个新字段和一个时间戳。要查看两个具有新 AIX 5L 参数的五秒钟系统切片摘要，请输入

```sh
# vstat -It 5 2
```

`timex` 命令将显示命令的已耗时、用户时间和系统执行时间。命令行选项允许生成类似 `sar` 命令数据项的系统活动总报告。要显示由 `ps -ef` 命令产生的系统活动，请输入

```sh
# timex -s ps -ef > /dev/null
```

`iostat` 命令报告处理器统计信息以及所有系统输入和输出设备统计信息。随 AIX 5L 提供的新命令行选项增加了新的适配器和系统吞吐量标题字段及报告。在此命令收集数据之前，必须将 `sys0` 的 `iostat` 属性设置为 `true`。使用 `lsattr` 和 `chdev` 命令来列出和更改此属性。

```sh
# lsattr -El sys0 -a iostat      # Check the iostat attribute
# chdev -l sys0 -a iostat=true   # Change the iostat attribute
```

使用以下命令行在复制一个大文件到跨越这三个测试驱动器的目标文件系统 `/fatest` 时，从这三个测试驱动器收集 I/O 性能数据。

```sh
# echo "/bin/cp . /largefile /fatest\n/usr/sbin/umount /fatest" > a.out
# iostat -d hdisk2 hdisk3 hdisk4 5 > /tmp/iostat.out &
# timed.sh a.out
# jobs          # To see what background jobs to stop
# kill %1       # To kill the background iostat command
```

卸载文件系统可确保测试数据已完全写入目标驱动器，并且 `timex` 命令将为您提供一个参考标尺。请不要在此示例中使用、测试或卸载生产文件系统。

`sar` 命令特别擅长从对称多处理器系统收集 CPU 统计信息。它调用 `sadc` 命令，并访问已由会计系统和 adm crontab 激活的许多数据收集文件。实际上，`/usr/lib/sa/sa/sa2` 是一个为 `sar` 配置的包装脚本，设置为由 adm crontab 每天运行一次（参见本章中“Cronat 条目”部分）。要创建一个临时报告，该报告可作为 ASCII 输入文件用于电子表格，以说明第四号 CPU 当天的性能（该报告将追踪全天内 `%usr`、`%sys`、`%wio` 和 `%idle` 的变化），请输入

```sh
# sar -P 4 > /tmp/cpu4_data.txt
```

# 定期清理

开启系统计就像打开水闸一样。在活跃的多服务器系统上，会计可能会生成大量数据，这些数据必须作为常规清理活动的一部分进行过滤和归档。adm cron 表中指定的默认会计程序会定期关闭并重命名会计文件，以协助管理数据。系统管理员负责实施归档旧数据文件并清理它们的程序。应该保存哪些信息以便后世参考？你可以采取保守的方法，保存所有报告和数据文件；或者你可以不计后果，创建 cron 表脚本每天删除旧报告和数据文件。适度的做法可能建议

