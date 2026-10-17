
PostgreSQL 应该返回类似的内容：

Welcome to psql 8.1.5, the PostgreSQL interactive terminal.

```text
Type: \copyright for distribution terms

\h for help with SQL commands

\? for help on internal slash commands

\g or terminate with semicolon to execute query

\q to quit
```

让我们给 `psql` 发一个简单的 SQL 命令：

（此处缺少 SQL 命令示例）

如果你的 SQL 命令没有显示上面的表，你将需要调试 RTA 的安装。最常见的问题是客户端和 RTA 之间的 PostgreSQL 协议不匹配。`psql` 客户端可能会给出警告，但它对使用新客户端连接旧服务器是相当宽容的。如果你使用的是最新的 `psql` 客户端，可能会出现这种情况。

检查 RTA 网站以查看你的 RTA 版本是否与你的 PostgreSQL 版本兼容。如果不匹配，请更新 RTA 或 PostgreSQL。本书附带 CD 包含了已知兼容的 RTA 和 PostgreSQL 库版本。你也可以通过 `netstat -natp` 验证应用程序是否正在监听 8888 端口。

在进入 SQL 教程之前，让我们尝试几个命令看看应用程序是如何响应的。

```bash
# UPDATE ztable SET zalarm = 1;
UPDATE 5
#
```

这应该会在你启动 `myapp` 的控制台上打印出一条转换消息。（注意，`psql` 返回了更改的行数，因为我们没有指定更改哪一行，所以所有五行都已更新）。
现在再次执行执行相同的命令。

```bash
# UPDATE ztable SET zalarm = 1;
UPDATE 5
#
```

控制台上不应打印任何消息，因为这次没有发生转换。

将警报器置回零应该会导致一次转换，现在转换的计数应该是 2。

```bash
# UPDATE ztable SET zalarm = 0;
UPDATE 5
# SELECT * FROM ztable;
| zname | zalarm | zcount |
|---|---|---|
| 0 | | 2 |
| 0 | | 2 |
| 0 | | 2 |
| 0 | | 2 |
(5 rows)
```

当你第一次启动 `./myapp` 时，保存的表配置文件 `/tmp/zsave.sql` 并不存在。通过对标记为 `RTA_DSKSAVE` 的列进行更新来创建它。

```bash
# UPDATE ztable SET zname = "row name";
UPDATE 5
#
```

你可以通过执行 `cat /tmp/zsave.sql` 来验证上述内容。你应该看到以下内容：

```text
UPDATE ztable SET zname = "row name" LIMIT 1 OFFSET 0
UPDATE ztable SET zname = "row name" LIMIT 1 OFFSET 1
UPDATE ztable SET zname = "row name" LIMIT 1 OFFSET 2
UPDATE ztable SET zname = "row name" LIMIT 1 OFFSET 3
UPDATE ztable SET zname = "row name" LIMIT 1 OFFSET 4
```

为了结束关于 RTA 的这一节，让我们生成一些错误并查看对应的错误消息。

```bash
# UPDATE ztable SET zcount = 0;
ERROR: Can not update read-only column 'zcount'
# UPDATE ztable SET zname = "abcdefuvwxyzuvwxyz";
ERROR: String too long for 'zname'
#
```
