

## 图 16-18
使用 SQL 命令查看数据

```
mysql> SELECT * FROM active;
+-----------+----------+---------------+
| first | last | phone | lastpurchase |
+-----------+----------+---------------+
| Robb | Tracy | 801-756-5555 | 2010-07-04 |
+-----------+----------+---------------+
1 row in set (0.00 sec)
mysql>
```

FROM active WHERE last='Tracy';，然后运行 DELETE FROM active WHERE last='Tracy';
你也可以使用 UPDATE 命令修改现有数据。语法如下：
UPDATE table_name SET column = new_value WHERE condition

> 提示 你还可以使用 JOIN 命令合并来自两个不同表的字段。

> 考试提示 你可以使用 GROUP BY 语句按一个或多个列合并 SELECT 语句的结果。它常与 SUM() 语句一起使用。例如，假设 active 表包含两个额外的列，分别命名为 quantity 和 custid，并使用这些信息来记录个人订单。在这种情况下，每个客户在表中可能有多个记录；每个订单对应一个记录。执行 SELECT custid, SUM(quantity) AS "Total" FROM active GROUP BY custid; 将为每个唯一的客户 ID 聚合出单个结果，在新列“Total”中显示每个客户购买的总数量。

## 章节回顾

在本章中，我们探讨了几种可以在 Linux 上实现的网络服务。首先，我们研究了如何使用 CUPS 配置打印。CUPS 服务由 cupsd 守护进程提供。CUPS 可以在本地网络上宣告其打印机的可用性。其他 Linux 系统可以监听这些宣告，连接到 CUPS 服务，并向其打印机发送打印作业。CUPS 系统由以下组件组成：

- CUPS 调度器
- CUPS 过滤器
- CUPS 后端
- PPD 文件
- 基于 Web 的配置实用程序
- 打印队列 (/var/spool/cups)

CUPS 服务使用 /etc/cups/cupsd.conf 文件进行配置。配置 CUPS 时需要完成的任务之一是配置 CUPS 管理员。为此，请在 shell 提示符下输入 **lppasswd -g sys -a user_name**。完成此操作后，你可以使用基于 Web 的配置实用程序创建打印机。你需要打开 web 浏览器并导航至 http://localhost:631 来完成此操作。

创建打印机后，你可以选择通过图形界面 Linux 应用程序中的“文件 | 打印”选项来发送打印作业。你也可以使用 lp 命令从 shell 提示符发送打印作业。你可以使用以下命令行实用程序来管理你的 CUPS 系统：

- `lpstat -t` 显示系统中 CUPS 打印机的信息
- `cancel` 取消打印作业
- `lpoptions -d` 设置系统的默认打印机
- `cupsaccept`/`cupsreject` 启用或禁用 CUPS 打印队列
- `cupsenable`/`cupsdisable` 启用或禁用 CUPS 打印机

你还可以使用行打印机守护进程（lpd）来管理 Linux 打印。你可以使用 lpd 命令执行以下操作：

- `lpr -P printer_name filename` 打印文档
- `lpc status` 查看打印机状态
- `lpc print` 查看待处理的打印作业
- `lprm job_number` 从队列中删除待处理的打印作业

这些命令也适用于 CUPS 打印机和打印队列。

我还回顾了一个你可以用来排查打印问题的标准化流程。我们还查看了一些常见的打印问题及其解决方法。

随后，我们转向了 Linux 时间管理。我首先回顾了 Linux 上硬件时钟和系统时间之间的区别以及它们各自的用途。然后我们研究了如何使用 hwclock 命令来管理硬件时钟。

为了在联网的 Linux 系统之间同步时间，你可以在 shell 提示符下使用 netdate 命令。语法为 **netdate time_server**，其中 time_server 是网络上另一个运行在 UDP 端口 37 上的时间服务的 Linux 系统的 IP 地址或 DNS 名称。使用 netdate 同步系统时间后，你可能需要使用 **hwclock -s -sysclock** 命令将系统时间与硬件时钟同步。

netdate 命令在网络上同步时间方面表现相当不错。但是，按照定期计划保持时间同步的更好方法是使用网络时间协议（NTP）。NTP 比 netdate 以更整洁的方式管理时间。NTP 以温和的方式调整时间。如果时间提供者和时间消费者（你的本地系统）之间存在时间差异，它会逐渐以小的增量调整时间，直到最终时间同步。NTP 也得到大多数操作系统的支持。

你可以使用 Linux 上的 ntpd 守护进程与另一个 NTP 时间提供者同步时间。运行 ntpd 的系统可以同时作为时间消费者和时间提供者。NTP 协议在 IP 端口 123 上运行。时间消费者在端口 123 上向时间提供者发送时间同步请求。时间提供者向消费者发送其时间，消费者上的系统时间根据 NTP 算法进行调整。

你需要熟悉的关键 NTP 概念包括以下各项：

- 层级（Stratum）
- 步进和微调（Stepping and slewing）
- 疯狂时间（Insane time）
- 漂移（Drift）
- 抖动（Jitter）

一旦在你的系统上安装了 NTP，你就可以在文本编辑器中编辑 /etc/ntp.conf 文件以指定应从哪个系统获取时间。语法如下：

```
server time_server_IP_address_or_DNS_name
```

如果需要，你可以使用 NTP 池时间服务器。pool.ntp.org 域使用 DNS 轮询从自愿加入该池的时间提供者池中随机选择一个。

在你实际启动 ntpd 守护进程之前，你需要与你的 NTP 时间提供者进行一次快速的、一次性的同步，以避免疯狂时间问题。这通过在 shell 提示符下输入 ntpdate address_of_time_provider 来完成。这将执行初始同步，以便在启动守护进程之前使时间接近。如果你的系统和 NTP 时间提供者之间的时间差异很大，你可能实际上需要多次运行该命令。完成后，你可以使用发行版使用的适当 init 脚本目录中的 init 脚本启动 ntpd 守护进程。

NTP 守护进程启动后，你可以使用两个命令来跟踪 ntpd 守护进程的工作情况：

- `ntpq -p`
- `ntptrace`

在掌握了 NTP 之后，我们随后查看了 Linux MTA 管理。我从回顾电子邮件是如何工作的开始。我们查看了 MUA、MTA 和 MDA 的角色，以及 IMAP 和 POP3 守护进程。然后我们查看了几种常用的 Linux MTA：

- sendmail
- postfix
- qmail
- Exim

这些 MTA 可以通过 SMTP 接收从 MUA 发送的电子邮件消息。但是，它们不能通过 POP3 或 IMAP 将消息下载到电子邮件客户端。为此，你必须在你的系统上安装 imap 软件包。

然后我们查看了 mail 命令行实用程序，你可以使用它在 shell 提示符下读取存储在本地 MTA 中的电子邮件。要发送消息，你可以在 shell 提示符下输入 mail recipient_address。要查看邮件队列中未读消息的列表，你可以在 shell 提示符下输入 mailq。

你还可以配置在 Linux 系统上运行的 MTA 的别名。邮件别名将寻址给一个用户的邮件重定向到另一个用户的账户。你使用 /etc/aliases 文件来配置别名。此文件每行定义一个别名。你定义的别名必须指向一个现有的电子邮件地址。该文件的语法如下：

```
alias: list of real e-mail addresses
```

完成别名配置后，你必须在 shell 提示符下以 root 身份运行 newaliases 命令以启用它们。

你还可以使用用户主目录中的 ~/.forward 文件来配置转发。大多数 Linux MTA 会检查用户主目录中此文件是否存在，以配置消息转发。你可以在文本编辑器中打开/创建该文件，并输入你要转发电子邮件到的地址。

至此，我们将注意力转移到 SQL 数据管理。我从讨论数据库如何存储信息开始。Linux 上通常实现两种数据库服务：

- MySQL
- PostgreSQL

SQL 定义了可用于检索和更新数据库中数据的语句，例如 SELECT、UPDATE、DELETE、INSERT 和 WHERE。关系数据库使用字段、记录和表进行组织。字段是单个信息片段。记录是一组完整的字段，而表是记录的集合。每个表由一个名称标识，例如 Customers。每个表包含记录（每个记录为单行），记录包含一个或多个字段，字段进而包含实际的数据库数据。你可以使用以下命令来管理 SQL 数据库中的数据：

- SELECT
- UPDATE
- DELETE
- INSERT INTO
- CREATE TABLE
- ALTER TABLE
- DROP TABLE

然后我回顾了如何在 Linux 上实现 MySQL 数据库服务。安装完成后，你可以使用 SQL 客户端来管理 SQL 服务器中的数据。我回顾了如何使用 shell 提示符下的 mysql 命令来执行此操作。语法为 mysql -h host_name -u user_name -p。然后我讨论了如何在 mysql 客户端中使用以下命令：

- CREATE DATABASE
- USE
- SHOW TABLES
- CREATE TABLE

