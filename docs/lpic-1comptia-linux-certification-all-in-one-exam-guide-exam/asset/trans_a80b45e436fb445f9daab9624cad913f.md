

## 快速回顾

大多数 Linux 发行版使用 CUPS 来提供本地和网络打印功能。
CUPS 服务由 `cupsd` 守护进程提供。
CUPS 可以宣布其打印机在本地网络上的可用性。
其他 Linux 系统可以监听这些广播，连接到 CUPS 服务，并向其打印机发送打印任务。
CUPS 系统由 CUPS 调度器、CUPS 过滤器、CUPS 后端、PPD 文件、基于 Web 的配置实用程序以及打印队列（`/var/spool/cups`）组成。
CUPS 服务通过 `/etc/cups/cupsd.conf` 文件进行配置。
若要允许其他 Linux 系统通过您的 CUPS 打印机进行打印，您必须取消 `/etc/cups/cupsd.conf` 文件中 BrowseAddress 指令的注释。
在 shell 提示符下使用 `lpusers -g sys -a user_name` 命令创建一个 CUPS 管理员用户。
您使用基于 Web 的配置实用程序来配置您的打印机。可以通过 http://localhost:631 访问该实用程序。
创建好 CUPS 打印机后，您可以通过在图形 Linux 应用程序中选择“文件” | “打印”来发送打印任务。
您可以在 shell 提示符下使用 `lp` 命令发送打印任务。
您可以使用以下命令行实用程序来管理您的 CUPS 系统：
- `lprstat -t`
- `cancel`
- `lpoptions -d`
- `cupsaccept` / `cupsreject`
- `cupsenable` / `cupsdisable`

您还可以使用行打印机守护进程（lpd）来管理 Linux 打印。
您可以使用 lpd 命令执行以下操作：
- `lpr -P printer_name filename`
- `lpc status`
- `lpq`
- `lprm job_number`

您应该使用标准化的流程来排查打印问题。
您应该记录打印任务的流程，以帮助排查打印问题。
常见的打印问题包括：
- 打印机缺纸了吗？
- 打印机通电了吗？
- 如果是网络打印机，它连接到网络了吗？
- 网络正常吗？
- 您可以从用户工作站 ping 打印机吗？
- 用户在发送打印任务时选择了正确的打印机吗？
- 是否为打印机配置了正确的打印机驱动程序？

您可以使用 `hwclock` 命令管理硬件时钟。
要在网络连接的 Linux 系统之间同步时间，您可以在 shell 提示符下使用 `ntdate` 命令。
语法为 `ntdate time_server`，其中 `time_server` 是网络上另一台正在 UDP 端口 37 上运行时间服务的 Linux 系统的 IP 地址或 DNS 名称。
使用 `ntdate` 同步系统时间后，您可能希望使用 `hwclock --systohc` 命令将系统时间与硬件时钟同步。
定期保持时间同步的一种更好方法是使用网络时间协议（NTP）。
NTP 以比 `ntdate` 更干净的方式管理时间。
如果时间提供者和时间消费者（您的本地系统）之间存在时间差异，它会通过小增量逐步调整时间，直到最终实现同步。
NTP 得到大多数操作系统的广泛支持。
运行 `ntpd` 的系统可以同时充当时间消费者和时间提供者。
NTP 协议在 IP 端口 123 上运行。时间消费者在端口 123 上向时间提供者发送时间同步请求。
时间提供者向消费者发送其时间，并根据 NTP 算法调整消费者的系统时间。
您需要熟悉以下几个关键的 NTP 概念：
- 层级（Stratum）
- 步进和微调（Stepping and slewing）
- 异常时间（Insane time）
- 漂移（Drift）
- 抖动（Jitter）

您可以在文本编辑器中编辑 `/etc/ntp.conf` 文件，以指定应从哪个系统获取时间。
`pool.ntp.org` 域使用 DNS 轮询从自愿加入池中的时间提供者池中随机选择一个。
在实际上启动 `ntpd` 守护进程之前，您需要通过在 shell 提示符下输入 `ntpdate address_of_time_provider` 与您的 NTP 时间提供者进行快速的一次性同步，以避免异常时间问题。
您可以使用发行版使用的相应 init 脚本目录中的 init 脚本来启动 `ntpd` 守护进程。

电子邮件消息使用 MUA、MTA 和 MDA 以及 IMAP 或 POP3 守护进程创建和传输。
几种常用的 Linux MTA 包括：
- sendmail
- postfix
- qmail
- Exim

MTA 无法通过 POP3 或 IMAP 将消息下载到电子邮件客户端。
为此，您必须在系统上安装 `imap` 包。
您可以使用 `mail` 命令行实用程序在 shell 提示符下读取存储在当地 MTA 中的电子邮件。
要发送消息，您可以在 shell 提示符下输入 `mail recipient_address`。
要查看邮件队列中未读消息的列表，您可以在 shell 提示符下输入 `mailq`。

您可以配置运行在您的 Linux 系统上的 MTA 的别名。
邮件别名将发给一个用户的邮件重定向到另一个用户的账户。
您使用 `/etc/aliases` 文件来配置别名。
此文件每行定义一个别名。
您定义的别名必须指向一个现有的电子邮件地址。
完成别名配置后，您必须以 root 身份在 shell 提示符下运行 `newaliases` 命令以启用它们。

您还可以使用用户主目录中的 `.forward` 文件来配置转发。
大多数 Linux MTA 会检查用户主目录中是否存在此文件以配置消息转发。
您可以在文本编辑器中打开/创建该文件，并输入您想要转发邮件的电子邮件地址。

Linux 上常见的两种数据库服务是：
- MySQL
- PostgreSQL

SQL 定义了可用于检索和更新数据库中数据的语句，例如 SELECT、UPDATE、DELETE、INSERT 和 WHERE。
关系数据库使用字段、记录和表进行组织。
字段是单个信息片段。
记录是一组完整的字段，而表是记录的集合。
每个表都由名称标识，例如 Customers。
每个表包含记录（每个记录为单行），这些记录包含一个或多个字段，而这些字段又包含实际的数据库数据。

您可以使用以下命令管理 SQL 数据库中的数据：
- SELECT
- UPDATE
- DELETE
- INSERT INTO
- CREATE TABLE
- ALTER TABLE
- DROP TABLE

您可以使用 shell 提示符下的 `mysql` 命令连接到 MySQL 数据库。
语法为 `mysql -h host_name -u user_name -p`。
您可以在 `mysql` 客户端内使用以下命令：
- CREATE DATABASE
- USE
- SHOW TABLES
- CREATE TABLE
- DESCRIBE
- SELECT
- FROM
- WHERE
- DELETE
- UPDATE
- JOIN

## 问题

1. 以下哪个命令可以将 /home/tux/employees.txt 文件打印两份到名为 MIN2300W 的 CUPS 打印机？

A. lp -d MIN2300W -n 2 /home/tux/employees.txt
B. lp -p MIN2300W -c 2 /home/tux/employees.txt
C. lp /home/tux/employees.txt
D. lp -d MIN2300W /home/tux/employees.txt

2. 以下哪个命令将 Linux 系统上的默认打印机设置为名为 MIN2300W 的打印机？

A. lpoptions MIN2300W
B. lpstat -d MIN2300W
C. lp default = MIN2300W
D. lpoptions -d MIN2300W

3. 哪个 CUPS 组件处理来自 CUPS 客户端的 IPP 打印请求？

A. CUPS 调度器
B. PDLs
C. CUPS 后端
D. PPDs

4. 您的 Linux 系统 IP 地址为 192.168.1.20。您应该在浏览器中使用哪个 URL 来访问 CUPS 基于 Web 的管理实用程序？

A. http://192.168.1.20
B. https://192.168.1.20
C. http://192.168.1.20:631
D. http://192.168.1.20/cups

5. /etc/cups/cupsd.conf 文件中的哪个指令指定 cupsd 是否使用广播在网络上宣布其打印机？

A. BrowseAddress
B. BrowseAllow
C. Broadcast
D. Browsing

6. 哪个命令可以将 Linux 系统上的硬件时钟设置为系统时间？

A. hwclock -w
B. hwclock -s

