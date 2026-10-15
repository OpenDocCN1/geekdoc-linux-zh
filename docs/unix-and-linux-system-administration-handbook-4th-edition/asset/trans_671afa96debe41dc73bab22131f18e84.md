

如果 amavisd 将扫描后的邮件和结果交还给最初接收该邮件的 MTA，则可以在线路上进行过滤，并在 MTA 的初始 SMTP 会话期间拒绝邮件。如果 amavisd 反而将邮件排队到内部邮件枢纽，则过滤为离线处理，违规邮件可以被丢弃或退回。

有关 SNMP 的更多信息，请参阅第 21 章。

amavisd 非常注重不丢失邮件，不让邮件未经检查就溜走，尊重各个收件人的意愿，并遵循各种电子邮件相关 RFC 中规定的标准。尽管是用 Perl 编写的，amavisd 的性能相当不错。它只扫描每封邮件一次，无论与之关联的收件人有多少。日志可以非常详细，发行版中的工具可以通过 SNMP 监控过滤。amavisd 不需要以 root 身份运行，并且拥有良好的安全记录。

## amavisd 安装

从 jims.is/software/amavisd 下载最新版本的软件，或获取 Linux 软件包并跳过分发层级顶部的 INSTALL 文件中详细说明的步骤。项目主页提供了指向预编译软件包的链接。amavisd 预计以用户和组 vscan 或 amavis 运行，因此最简单的方法可能是创建该用户和组，然后以 vscan 身份登录以获取软件并安装它。在你正确安装并运行 amavisd 后，将该账户的登录 shell 更改为 /bin/false 或其他受限 shell。

文件 amavisd.conf-default 包含每个可能的配置参数及其默认值。amavisd.conf-sample 是一个更典型的带注释的示例配置文件。最后，amavisd.conf 是一个最小的起点（但仍超过 750 行！），其中包含一些必须更改的变量的注释。配置语言是 Perl。

## 基本 amavisd 配置

以下是主机名为 mail.example.com 的基本 amavisd 配置，其中 MTA 和 amavisd 在同一台机器上运行，并使用 TCP 和 SMTP 协议相互通信。

```
use strict;

$myhostname = 'mail.example.com';
@local_domains_maps = ({'example.com'});
@mynetworks = qw[127.0.0.0/8 192.168.0.0/16];

$forward_method = 'smtp:[127.0.0.1]:10025';
$enable_db = 1;
$enable_global_cache = 1;
$max_servers = 5;
$DO_SYSLOG = 1;
$SYSLOG_LEVEL = 'mail.info';
$bypass_decode_parts = 1;
```

```
$final_virus_destiny = D_REJECT;
$final_banned_destiny = D_REJECT;
$final_bad_header_destiny = D_PASS;
$log_recip_temp = undef;

@av_scanners = (
    ["ClamAV-clamd",
        \&ask_daemon, ["CONSTSCAN /n", "/var/run/clamav/clamd"],
        qr/\bOK$/m, qr/\bFOUND$/m,
        qr/^.*?: (?!Infected Archive)(.*) FOUND$/m ],
);
1;
```

示例配置的 av_scanners 数组中列出了 40 多个反垃圾邮件和反病毒程序；此摘录仅显示 ClamAV。文件末尾的 1; 是一种 Perl 习惯用法，可确保文件本身在读取它的任何 Perl 上下文中都求值为 true。

## amavisd-new 工具

**amavisd-new** 发行版包含两个方便的工具：**amavisd-nanny** 和 **amavisd-agent**。nanny 监控 **amavisd** 的健康状况，agent 可实时访问大量类似 SNMP 的计数器和仪表。两者都需要 Berkeley DB 库。

**amavisd-nanny** 显示所有 **amavisd** 进程的状态、它们正在处理的邮件、正在做什么以及已持续多久。使用 **-h** 标志运行它会显示使用信息，并列出 **amavisd** 可能处于的状态。最有趣的是 S 表示垃圾邮件扫描，V 表示病毒扫描，以及点号（句点）表示空闲。每秒打印一个状态字符，每十秒打印一个冒号字符以便更易计数。你应该偶尔运行 **amavisd-nanny** 只是为了看看系统运行情况。以下是一个示例：

```
$ sudo amavisd-nanny
process-id    task-id    elapsed in    elapsed-bar (dots indicate idle)
              or state   idle or busy
PID 01422:              0:09:51       ........................
PID 26784: 26784+18    0:00:01       ==
PID 01422:              0:09:53       ........................
PID 26784:              0:00:03
```

**amavisd-agent** 是一个类似 SNMP 的代理，可从所有正在运行的守护进程收集统计信息，并可显示处理的邮件数量、每封的处理时间、包含病毒的百分比、最常见的病毒等。以下是一个大幅截断的示例：

```
$ sudo amavisd-agent
entropy              STR ipwvEI0sVA
sysContact           STR
sysDescr             STR amavisd-new-2.6.1 (20080629)
sysLocation          STR
sysObjectID          OID 1.3.6.1.4.1.15312.2.1
```
