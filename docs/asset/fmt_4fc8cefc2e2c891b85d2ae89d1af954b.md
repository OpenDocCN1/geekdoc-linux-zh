
# 37. crond 和 atd

## 37.1. cron 时间规格

以下是 `/etc/cron-alarm.sh` 的时间规格示例：

```
# 时间规格 root /etc/cron-alarm.sh
30 20 * * root /etc/cron-alarm.sh
35 19 * * root /etc/cron-alarm.sh
58 18 * * root /etc/cron-alarm.sh
01 * * * root run-parts /etc/cron.hourly
02 4 * * root run-parts /etc/cron.daily
22 4 * * root run-parts /etc/cron.weekly
42 4 1 * root run-parts /etc/cron.monthly
```

注意，`#` 字符像通常一样用于注释。`cron` 还允许你指定运行命令时的环境变量。

### 37.2. at 命令

你的时间添加应该像我的一样添加，用来提醒我一天中最后几班地铁训练。

最后四个条目是供应商提供的。`run-parts` 命令是一个简单的脚本，用于运行列在 `/etc/cron.hourly`、`/etc/cron.daily` 等目录下的所有命令。因此，如果你有一个需要每天运行但不需要在特定时间运行的脚本，你不需要编辑 `crontab` 文件：只需将该脚本与其他脚本一起放在 `/etc/cron.daily`、`<interval>` 目录中即可。

我自己的 `/etc/cron.daily/` 目录包含：

| | | | | | | | | |
|---|---|---|---|---|---|---|---|---|
| drwxr-xr-x | 2 | root | | 1024 | Sep 2 13:22 | | | |
| drwxr-xr-x | 59 | root | | 644 | Aug 31 13:11 | | | |
| -drwxr-xr-x | 1 | root | | 140 | Aug 13 16:16 | backup | | |
| -drwxr-xr-x | 1 | root | | 051 | Jun 16 1999 | logrotate | | | |
| -drwxr-xr-x | 1 | root | | 390 | Sep 14 1999 | makethis.cron | | | |
| -drwxr-xr-x | 1 | root | | 459 | Mar 23 1999 | radius,cron.daily | | | |
| -drwxr-xr-x | 1 | root | | 099 | Jul 23 21:48 | alocate.cron | | | |
| -drwxr-xr-x | 1 | root | | 103 | Oct 25 1999 | tetex.cron | | | |
| -drwxr-xr-x | 1 | root | | 004 | Aug 03 1999 | tmpwatch | | | |

建议检查这些每一项，看看你的系统在你背后在些什么。`at` 将在未来的某个时间执行命令，且仅执行一次。我认为这是至关重要的，尽管在写这一章之前我从未自己用过。`at` 是守护进程的前端，`crond` 绝对会运行。尝试我们的文件示例，记住：

# 38. PostgreSQL 数据库服务器

## 38.1. 结构化查询语言 (SQL)

结构化查询语言（SQL）是一门用于访问数据库的编程语言。PostgreSQL（曾简称为 Postgres95）源自伯克利开发的 Postgres 的对象关系数据库系统。在经过十多年的开发后，PostgreSQL 是目前任何地方可获得的的最先进开源数据库，作为在任何平台上可运行的数据库，它提供了多版本并发控制（MVCC），支持几乎所有的 SQL 结构（包括事务、自定义类型和函数），并拥有广泛的语言绑定（包括 C、Java、Perl、Tcl 和 Python）。

PostgreSQL 也非常干练。大多数人问为什么它没有图形界面。考虑到它运行在许多不同的平台上，它作为一个纯后端引擎是合理的。图形界面是一种不同的软件项目，可能会支持不止一种类型的数据库服务器，并在可能的某一种图形界面下运行。

PostgreSQL 软件包包含下面两个节描述的文件：

## 38.2. postgres 包内容

PostgreSQL 软件包包含以下用户程序：

| createdb | dropdb | pg_dump | psql |
|---|---|---|---|
| createlang | droplang | pg_dumpall | vacuumdb |
| createuser | dropuser | pg_id |

以及以下服务器程序：

| initdb | pg_ctl | pg_upgrade | postgresql-dump |
|---|---|---|---|
| initlocation | pg_encoding | pg_version | postmaster |
| ipcclean | | | |

每个程序都有一个手册页（man page），你应该了解一下。

进一步的手册提供了实际 SQL 命令的参考。尝试 `man select`（后文详解）：

## 38.3. 安装并初始化 postgres

PostgreSQL 可以从你喜爱的发行版中预包获取。只需使用 `rpm` 或 `dpkg` 安装软件包，然后按照下面的说明操作。

如果 `postgres` 服务正在运行，请停止它，`.init.d` 脚本可能通过 `postgres` 或 `postgresql` (Debian) 命令调用：

```
/etc/rc.d/init.d/postgres stop
(/etc/rc.d/init.d/postgres stop)
```

编辑 `init.d` 脚本以支持 TCP 请求。会有像下面的行，你可以在其中添加 `-i` 选项。我的看起来像：

```
su -l postgres -c "usr/bin/pg_ctl -D $PGDATA \
```

## 38.4. 配置网络与权限

```bash
-p /usr/bin/postmaster -o -i -o start >/dev/null 2>&1
```

这也（带有 `-o -e` 选项）强制使用欧洲日期格式（28/4/1984 而不是 4/28/1984）。注意，除非你编辑了 `/var/lib/libpq/data/pg.hba.conf`（Deb Debian 上是 `/etc/postgresql/pg.hba.conf` 文件）并添加了如下行，否则主机无法连接：

```
host 192.168.4.7 255.255.255.255 trust
```

在任何情况下，你都应该检查此文件以确保只有信任的主机可以连接到数据库，如果你仅从本地机器连接，请完全删除 `-i` 选项。在有限的范围内，你可以在此文件中限制用户可以连接。

如果 `postgres` 监听的 UNIX 域套接字（即 `/tmp/.s.PG.5432`）的权限为 `0770` 而不是 `0777`，那就太好了。这样你可以将连接限制为属于 `postgres` 组的用户。你可以通过在 `postgres-7.0` 源码中搜索 C `chmod` 命令 `src/backend/libpqcomm.c` 来添加此功能。后续版本可能已经增加了设置此套接字权限的功能。

要运行 `postgres`，你需要一个同名的用户。如果你还没有该用户，请执行：

```bash
/usr/sbin/useradd postgres
```

并使用命令重启服务器：

```bash
/etc/rc.init.d/postgresql restart
```

`postgres` `init.d` 脚本在首次运行时初始化一个模板数据库，因此你可能需要启动它。

现在你可以创建自己的数据库了。以下示例创建了一个名为 `finance` 的数据库以及一个名为 `finance` 的 `postgres` 用户。这些创建操作是以用户 `postgres` 的身份执行的（这就是 `-U` 选项的作用）。你应该以 `root` 或用户 `postgres` 的身份不带 `-U postgres` 运行这些命令。

```bash
[root@cericon] # /usr/sbin/useradd finance
[root@cericon] # createuser -U postgres --aduser --createdb finance
CREATE USER
[root@cericon] # createdb -U finance finance
CREATE DATABASE
[root@cericon] #
```

## 38.5. 使用 psql 进行数据库查询

现在数据库已经存在，你可以开始运行 SQL 查询了。

```bash
[root@cericion-#] psql -U finance
Welcome to psql, the PostgreSQL interactive terminal.
```

输入输入：`\copyright` 查看分发条款

`\h` 获取 SQL 斜杠命令帮助

`\?` 获取内部斜杠命令帮助

`\q` 或输入分号结束以执行查询

`\q` 退出
