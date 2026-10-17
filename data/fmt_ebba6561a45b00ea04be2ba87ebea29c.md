
`*.emerg *`

示例配置包含以下规则：

- `uucp.crit /var/log/spooler`
- `local7.* /var/log/boot`
- `*.emerg *`

关于此文件中指定规则的几条说明将有助于选择器的用法：

1. 禁用内核消息到控制台的日志（包含在注释中），但通常会发送到系统控制台。
2. `info` 级别或以上的所有内容都记录到 `/var/log/messages`，但 `mail` 和 `cron` 消息通过对优先级使用 `none` 被排除。
3. 来自 `authpriv`、`cron` 和 `mail` 的信息通过指定操作的三个路由分离到三个单独文件中。
4. 任何 `emerg` 消息都会发送所有登录用户。
5. `uucp` 和 `news` 子系统生成的关键消息指向 `/var/log/spooler` 文件。
6. 系统启动过程的消息由启动脚本重定向到 `/var/log/boot`，它们使用 `init` 命令和默认 `notice` 日志级别。

## 11.9.2 内核消息日志

现在我们已经对 `syslogd` 系统的工作原理有了简单了解，就可以利用它来跟踪集群中的系统活动了。在继续配置 `syslog` 远程日志之前，我们需要注意一个被我们忽略的细节：内核日志守护进程 `klogd`。

内核会在 `/proc/kmsg` 文件中产生错误消息，该文件是内核消息缓冲器的接口。`klogd` 进程的任务是检测并读取任何消息，通过适当 `/boot/System.map-<version>` 文件将数值地址转换为符号值，对其进行正确的格式化，最后将输出定向到文件、系统控制台和 `syslog`。

内核错误消息（或称为 `oops` 的可恢复故障）最可能在向内核添加新功能时发生，这些功能可能是通过补丁或来自 Linux 当前操作系统发行版以外的软件添加。你可能需要添加驱动模块、启用实验性内核，或者根据用户需求对内核部分进行补丁。所有这些活动都会打破现状并增加内核消息的产生可能性。在这种情况下，能够捕捉内核软件生成的任何消息和调试信息是一个好主意。如果你正在与 ISV（独立软件供应商）或需要软件反馈的软件开发者合作，这一点尤为重要。

配置并启用 `klogd` 将让你能够记录内核生成的消息，并选择生成多少信息以及信息的去向（本地系统控制台、日志文件或两者兼有）。如果目标之一是串口控制台，且你拥有串口端口切换器（例如 Cyclades 制造的，它们可以通过 NFS 将串口控制台输出日志到通道），那么可能没有必要同时将输出定向到本地系统的日志文件。但内核崩溃（`crash`）、`panic` 和 `oops` 的行为各不相同。

要启用 `klogd`，你必须修改 `/etc/sysconfig/syslog` 文件的内容，其中包含两个定义内核子系统守护进程启动选项的变量——一个用于 `syslog`，一个用于 `klogd`：

```bash
# syslog 选项
# -m 0 禁用 'MARK' 消息
# -r 启用来自远程机器的日志
# -x 禁用对通过 -r 接收的消息进行 DNS 查询
# 详细信息请参 syslog(8)
SYSLOG_OPTIONS="-m 0"
# klogd 选项
# -2 打印两次内核 oops 消息；一次用于 klog
# -t 用于解码，一次用于 'ksymoops' 处理
# -x 完全禁用 klogd 对 oops 消息的所有处理
# 详细信息请参阅 klogd(8)
KLOGD_OPTIONS="-x"
```

如你从 `KLOG_OPTIONS` 的变量定义所示，默认禁用了内核-ops 消息的处理。如果你更改了变量定义，必须执行：

```bash
# service syslog restart
```

以便将新选项传递给守护进程。此操作将停止并重启 `syslog` 和 `klogd` 进程。

## 11.9.3 启用远程日志

如之前提到的，要启用将日志发送到远程系统，你可以将 `/etc/syslog.conf` 中规则的“动作”部分替换为 `@system` 格式的令牌——例如使用 `@ns1` 将特定规则相关的消息发送到 `ns1`。远程日志功能使用 UDP 端口 514（参见 `/etc/services` 中的定义）。

但将消息发送到空中仅是所需操作的一半。毕竟，这是一种客户端-服务器软件架构。你必须配置远程 `syslog` 以监听并接受网络消息。这很容易，通过在 `/etc/sysconfig/syslog` 文件（如前所述）的 `SYSLOG_OPTIONS` 变量定义中添加 `-r` 选项即可。更改完成后，重启 `syslog` 守护进程（以及默认的 `klogd` 守护进程）：

```bash
# service syslog restart
```

图 11–9 显示了 `syslog` 子系统及其组件的示意图。

![](img/6e858fce5db2ec904615b8b7ba46f1ef_352_0.png)

在为集群日志客户端系统提供远程日志服务方面，你必须做出若干设计选择：

- 哪些日志信息对我很重要？
- 日志服务器上需要多少磁盘空间？
- 我需要启用内核消息吗？
- 需要多少个远程日志服务器？
- 日志数据如何在服务器之间划分？
- 远程和本地消息日志的混合比例是什么？

一旦你决定了远程记录哪些消息，就可以编写客户端的 `/etc/syslog.conf` 文件，根据子系统和优先级发送适当的消息。一个客户端配置可能如下：

```bash
# 将内核消息记录到远程服务器，'klogd -c 4'
# 也会将此级别以上的消息显示到控制台。
k.err @ns1.cluster.local
# 在本地记录除邮件以外的 info 或更高级别的任何内容。
# 不要记录权限认证消息！
*.info;mail:none;authpriv:none;cron:none /var/log/messages
# authpriv 文件访问限制。
authpriv.* @ns2.cluster.local
# 在本地记录所有邮件。
mail.* /var/log/mail
# 记录 cron
cron.* /var/log/cron
# 所有人接收紧急消息
*.emerg @ns2.cluster.local
# 保存 crit 级别的本地
local.crit /var/log/messages
# 保存 info 级别的本地
local.* /var/log/messages
# 保存 debug 级别的本地
local.* /var/log/messages
```

此配置将内核错误推发送到 `local.crit`。这就是为 Linux 系统设置独立 `/var` 分区产生价值的时候。如果由于某种原因，某个失控客户端记录了大量消息，相关的日志文件会增大分区。有了独立的 `/var` 分区，整个文件系统就不会停止其他活动。你需要保留的日志信息量将取决于你工作环境的稳定性和安全性。管理日志文件版本的有用工具是 `/usr/sbin/logrotate`，它会在收集日志信息后自动轮转、压缩和删除。

`/etc/logrotate.conf` 文件包含了 `logrotate` 的配置信息，同样，`syslog` 功能也有一个 `include` 语句，指向一个包含独立日志信息配置文件的目录。

```bash
# 详情参阅 "logrotate"
# 每周轮转日志
weekly
# 保留 4 周的备份
rotate 4
# 在轮转旧文件后创建新的（空）日志
create
# 如果你想压缩日志文件，请取消注释
# compress
# RPM 包将日志轮转信息放入此# 目录
include /etc/logrotate.d
# 没有包处理 wtmp —— 我们在这里轮转
/var/log/wtmp
  monthly
    create 0664 root wtmp
    rotate 1
}
# 系统特定的日志也可以在此处配置。
```

`/etc/logrotate.d` 中的配置信息是由需要日志管理的各个软件包添加的。这里是查看日志管理配置文件示例的真实位置。`syslog` 日文件的配置信息包含在 `/etc/logrotate.d/syslog` 中：

```bash
/var/log/messages /var/log/secure /var/log/mailog \
/var/log/spooler /var/log/boot.log /var/log/cron \
{
  sharedscripts
    postrotate
      /bin/kill -HUP `cat /var/run/syslogd.pid` /dev/null 2> /dev/null || true
}
```

命名服务守护进程（`named`）的默认配置文件 `/etc/logrotate.d/named` 如下：

```bash
/var/log/named.log {
  missingok
  create 0644 named named
  postrotate
    /bin/kill -HUP `cat /var/run/named/named.pid` 2> /dev/null 2> /dev/null || true
}
```

这两个文件说明了 `logrotate` 的一些特性：在日志文件“轮转”之前之后执行脚本的能力、控制日志文件创建的方式，以及在单个配置中处理多个文件（或通配符）的能力。通常，`prerotate` 和 `postrotate` 命令脚本会针对配置中的每个文件或匹配通配符的文件执行。`sharedscript` 定义表明，如果存在这两个脚本，则它们应该只针对与配置相关的整个文件集执行一次。

在这些示例中，`postrotate` 脚本执行了一个命令，会导致守护进程关闭已打开的文件并重启。对于现代守护进程，这将导致打开的文件（如日志）关闭、重新读取守护进程配置并轮转日志文件。某些守护进程可能不会以这种文明的方式运行，有许多配置选项可以帮助处理特殊情况。（在这种情况下，步骤可能是完全停止守护进程，将日志文件重命名为新名称，然后重启守护进程。）在重启守护进程之前，可能需要为它创建默认日志文件。详情请参见 man 页。

默认情况下，轮转是每周进行一次，这在主配置文件 `/etc/logrotate.conf` 中指定，该文件控制工具由某些外部调度器运行时时的行为（见下文关于 `cron` 的信息）。在繁忙的集群中，这可能导致与频繁活动（如 DNS 查询或用户身份验证信息）相关的日志产生巨大的日志文件。你可能需要考虑退回到每日轮转。

## 日志系统活动

`logrotate` 的活动由 `cron` 子系统调度，位于 `/etc/cron.daily` 目录，该目录在 `/etc/crontab` 文件中与小时、每周、每月目录一起指定。`/etc/cron.daily/logrotate` 文件仅在命令行上调用 `logrotate` 命令并带上其状态信息（文件上次轮转的时间）。`logrotate` 命令在命令行上保留其状态信息（文件上次轮转的时间）。这些信息存储在 `/var/lib/logrotate.status` 文件中，该文件包含类似下面的条目：

```bash
logrotate state -- version 2
"/var/log/messages" 2004-3-7
"/var/log/secure" 2004-3-7
"/var/log/boot.log" 2004-3-7
"/var/log/cron" 2004-3-7
```

图 11–10 显示了“logrotate”设施及相关组件的图。

## 11.9.5 使用 logwatch 报告

`/usr/sbin/logwatch` 工具允许通过扫描日志生成通用报告。它是高度可配置的，能够扫描当前活动的日志文件以及压缩存档。`logwatch` 的配置信息位于 `/etc/log.d` 目录，配置文件 `/etc/log.d/logwatch.conf` 是指向 `/etc/log.d/` 目录下某个文件的链接。报告的默认配置信息如下：

```bash
LogDir = /var/log
MailTo = root
Print = No
#Save = /tmp/logwatch
Range = yesterday
Detail = Low
Service = All
```

默认配置设置将搜索指定目录中的日志文件，生成并发送给 `root`，不会将报告打印到标准输出（stdout），仅搜索前一天的信息，并为所有定义的服务生成低分辨率报告。整个系统用 Perl 实现，并可以进行扩展以满足你的特定需求。

- 需要一个默认的 `cron` 配置。默认是将 `cron` 任务的输出邮寄给 `/etc/crontab` 中 `MailTo` 子句指定的用户。当然，这取决于是否激活了 `sendmail` 来处理邮件，否则邮件将静默等待发送。这种对本地操作（以及相关的 `sendmail` 守护进程）的依赖是许多 UNIX 和 Linux 子系统的一个问题。

## 日志服务器

**图 11–10** `logrotate` 设施的软件组件

`logwatch` 工具在不同版本的 Red Hat 和 Fedora 发行版上的运行情况各异。以下是使用 `logwatch` 的示例：

```bash
logwatch --service sshd --range all --archives --print

##################### LogWatch 4.3.2 (02/18/03) #################

Processing Initiated: Wed Mar 10 00:33:38 2004

Date Processed: all

Detail of Output: 0

Logfiles for Host: nsl

#####################################################

-- SSHD Begin ---

SSHD Started: 1 Time(s)

Users logging in through sshd:

  root logged in from hpxw4100.lucke.home (192.168.0.111)

  using password: 1 Time(s)

Unmatched Entries

RSA key generation succeeded

RSA key generation succeeded

DSA key generation succeeded

--- SSHD End ---

##################### LogWatch End #####################
```

## 日志系统活动

还有其他开源日志监控和分析工具可用。其中一个工具是 `wots` (http://www.vpc.univie.ac.at/~tc/tools/)，另一个是 `swatch` (http:///swatch.sourceforge.net)。

## 第 11 章 • 扩展与访问：远程访问服务、DHCP 和系统日志

下一步是在 KDC 上的 `/etc/syslog.conf` 文件中添加以下信息：

```bash
# 发送到远程服务器的 Kerberos 特定日志
Local0.* @logerver.cluster.local
```

不要忘记在 KDC 上重启 `syslog` 服务以激活更改：

```bash
# service syslog restart
```

现在，这将把 `Local0` 消息路由到远程日志服务器。在日志服务器上，我们需要通过向 `/etc/syslog.conf` 文件中添加配置规则，将 Kerberos 消息重定向到日志文件中：

```bash
# Kerberos 消息拥有自己的本地日志文件
Local0.* /var/log/Kerberos
```

再次，不要忘记在日志服务器上重启 `syslog` 服务：

```bash
# service logrotate restart
```

现在，我们需要在日志服务器上设置 `logrotate` 子系统来处理新文件。由于我们正在向 `syslog` 套件添加一个文件，我们只需要修改 `/etc/logrotate.d/syslog` 文件，将新的日志文件添加到标准处理流程中：

```bash
/var/log/messages /var/log/secure /var/log/maillog \
/var/log/spooler /var/log/boot.log /var/log/cron \
/var/log/Kerberos {
    sharedscripts
    postrotate
        /bin/kill -HUP `/var/run/syslogd.pid` 2 \
        /dev/null > /dev/null || true
}
```

在重启 Kerberos 守护进程之前，我们还可以测试远程客户端与日志服务器之间的消息：

```bash
# logger -i -t KERBEROS_TEST -p local0.err 'Message from KDC1'
```

如果消息通过远程日志服务器传输，我们可以使用新的日志目标后重启 Kerberos 守护进程：

```bash
# service krb5kdc restart
# service kadmin restart
```
