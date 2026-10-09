
/var/log 层级结构。除了提供日志记录功能外，**syslogd** 还允许一台机器充当网络的日志存储库，并允许任意程序处理特定的日志消息。

### rsyslog.conf

/etc/rsyslog.conf 文件存储 **rsyslogd** 的配置信息，而 /etc/rsyslog.d/50-default.conf 文件存储 **rsyslogd** 的默认规则。50-default.conf 文件中的每一行包含一个或多个*选择器*和一个*操作*，由空白字符分隔。选择器定义了消息的来源和类型；操作指定了 **rsyslogd** 如何处理该消息。以下是 **rsyslog.conf** 中的示例行（# 表示注释）：

```text
# First some standard logfiles. Log by facility.
    kern.*        -/var/log/kern.log
    lpr.*         -/var/log/lpr.log
    mail.*        -/var/log/mail.log
    #
    # Some "catch-all" logfiles.
    *.=debug;\   auth,authpriv.none;\
               news.none;mail.none          -/var/log/debug
    *.=info;*.=notice;*.=warning;\  auth,authpriv.none;\
               cron,daemon.none;\        mail,news.none -/var/log/messages
    #
    # Emergencies are sent to everybody logged in.
    *.emerg       *
```

### 选择器

选择器分为两部分：*设施*和*优先级*，中间用点号分隔。设施指示消息的来源。例如，**kern** 消息来自内核，而 **mail** 消息来自邮件子系统。以下是 **rsyslogd** 使用的设施名称列表以及生成这些消息的系统：

| 设施 | 描述 |
| :--- | :--- |
| auth | 授权和安全系统，包括登录 |
| authpriv | 与 *auth* 相同，但应记录到安全位置 |
| cron | cron |
| daemon | 没有自己类别的系统和网络守护进程 |
| kern | 内核 |
| lpr | 打印子系统 |
| mail | 邮件子系统 |
| news | 网络新闻子系统 |
| user | 默认设施；所有用户程序都使用此设施 |
| uucp | UNIX 到 UNIX 复制协议子系统 |
| local0 到 local7 | 保留供本地使用 |

优先级指示消息的严重程度。以下按优先级顺序列出了优先级名称及其代表的条件：

| 优先级 | 描述 |
| :--- | :--- |
| **debug** | 调试信息 |
| **info** | 无需干预的信息 |
| **notice** | 可能需要干预的条件 |
| **warning** | 警告 |
| **err** | 错误 |
| **crit** | 严重情况，如硬件故障 |
| **alert** | 需要立即关注的条件 |
| **emerg** | 紧急状态 |

仅由单一设施和优先级组成的选择器（例如 **kern.info**），会导致相应的操作应用于来自该设施且优先级为该级别或*更高*的所有消息。使用 `.` 指定单一优先级；例如，`kern.=info` 将该操作应用于具有 *info* 优先级的内核消息。感叹号指定不匹配某个优先级。因此 `kern.!info` 匹配优先级低于 *info* 的内核消息，而 `kern.!info` 也匹配优先级不是 *info* 的内核消息。

包含多个由分号分隔的选择器的行，如果在任何选择器匹配时即应用该操作。在包含多个选择器的行中，每个选择器都约束匹配条件，后续选择器通常会收紧约束。例如，选择器 `mail.info;mail.err` 匹配具有 `debug`、`info`、`notice` 或 `warning` 优先级的邮件子系统消息。

您可以将选择器的任一部分替换为星号以匹配任意内容。在选择器的任一部分中使用关键字 `none` 表示不可能匹配。选择器 `*.crit;kern.none` 匹配所有严重级别或更高优先级的消息，除了来自内核的消息外。

### 操作

操作指定了 **rsyslogd** 如何处理匹配选择器的消息。最简单的操作是普通文件，由绝对路径名指定；**rsyslogd** 会将消息追加到这些文件中。指定 `/dev/console` 可将消息发送到系统控制台。如果您希望获得消息的硬拷贝记录，请指定代表专用打印机的设备文件。在文件名前加上连字符 (-) 可防止 **rsyslogd** 在消息生成时立即将其写入文件（同步写入）。这样做可能会提高性能，但如果系统在消息生成后、写入文件前崩溃，您可能会丢失数据。

您可以通过指定一个或多个用逗号分隔的用户名将重要消息写入用户的终端。使用星号可将非常重要的消息写入每个已登录的终端。

要将消息转发到远程系统上的 **rsyslogd**，请指定系统名称，前面加上 @。由于内核的重要消息通常出现在系统崩溃之前且可能未被保存到本地磁盘，因此将内核的重要消息转发到另一个系统是一个好主意。**rsyslog.conf** 中的以下一行将严重级别的内核消息发送到 `plum`：

```text
kern.crit       @plum
```

## MySQL

MySQL (My Structured Query Language，我的结构化查询语言) 是世界上最流行的开源数据库。它是 LAMP (Linux, Apache, MySQL, PHP/Perl/Python) 中的 M，LAMP 是一个开源企业软件堆栈。许多编程语言提供了访问 MySQL 的接口（例如，C、PHP、Perl）。

Michael Widenius 和 David Axmark 于 1994 年开始开发 MySQL。如今，MySQL 数据库归 Oracle 公司所有并获得其支持（该公司于 2010 年收购了前所有者 Sun Microsystems）。

> **本节解释了如何设置和使用 MySQL；它并不解释 SQL**

*提示* SQL (Structured Query Language，结构化查询语言) 是用于操作 SQL 数据库（包括 MySQL）的语言。本章解释如何在 Fedora/RHEL 环境中安装和设置 MySQL。虽然该说明中包含一些 SQL 语句，但它并不试图解释 SQL。请参阅 dev.mysql.com/doc 获取 SQL 文档。

### 更多信息

- 主页：www.mysql.com
- MySQL 文档：dev.mysql.com/doc
- 介绍：dev.mysql.com/tech-resources/articles/mysql_intro.html
- 备份数据库：www.webcheatsheet.com/SQL/mysql_backup_restore.php

### 术语

本节简要描述了一些在关系数据库工作时使用的基本术语。另请参阅第 632 页的图 16-6。

- **数据库**：由一个或多个表组成的结构化持久数据集。
- **表**：关系数据库中的一组行。
- **行**：表中列的有序集合。也称为*记录*。
- **列**：表中一种类型的值的集合，每行一个值。也称为*字段*。

### 语法和约定

MySQL 程序由一个或多个语句组成，每个语句以分号 (;) 结束。虽然语句中的关键字不区分大小写，但本书为了清晰起见将关键字以大写字母显示。数据库和表名称区分大小写。

以下示例显示了一个多行 MySQL 语句，其中包含主解释器提示符 (mysql>) 和次解释器提示符 (->)。该语句显示名为 *people* 的表中满足指定条件的行中三列的值。

```sql
mysql> SELECT person,password,executeparm
-> FROM people
-> WHERE password IS NULL AND executeparm=true;
```

### 先决条件

安装以下软件包：

- **mysql-client**
- **mysql-server**

安装 **mysql-server** 软件包时，**dpkg postinst** 脚本会显示一个伪图形窗口，要求您为名为 **root** 的 MySQL 用户提供密码。此用户不是系统 **root** 用户。请提供一个密码。

根据需要发出以下 initctl 命令（第 434 页）以重启 MySQL：

```bash
$ sudo restart mysql
mysql start/running, process 3433
```

### 备注

与 Oracle 不同，创建用户时，MySQL 不会自动创建数据库。在 MySQL 中，用户和数据库不像在 Oracle 中那样紧密结合。

MySQL 拥有一套独立于 Linux 用户的用户集合。在安装完成后，MySQL 管理员的名称为 **root**。由于 MySQL **root** 用户与 Linux **root** 用户不同，因此它可以拥有不同的密码。

### 快速入门：设置 MYSQL

MySQL 安装后有一个匿名用户以及您为名为 **root** 的 MySQL 用户提供的密码。为了更安全的设置，请移除匿名用户。**mysql_secure_installation** 工具会询问一系列问题，允许您移除匿名用户并执行其他维护任务。响应当前 **root** 密码的提示时，输入您分配给名为 **root** 的 MySQL **root** 用户的密码。当您要求 MySQL 移除测试数据库时，它会生成错误，因为 Ubuntu 在安装 MySQL 时不会安装此数据库。

```bash
$ /usr/bin/mysql_secure_installation
...
You already have a root password set, so you can safely answer 'n'.
Change the root password? [Y/n] n
... skipping.
...
Remove anonymous users? [Y/n] y
...
Disallow root login remotely? [y/N] y
...
Remove test database and access to it? [y/N] y
- Dropping test database...
ERROR 1008 (HY000) at line 1: Can't drop database 'test'; database doesn't exist
... Failed! Not critical, keep moving...
...
Reload privilege tables now? [y/N] y
...
```

