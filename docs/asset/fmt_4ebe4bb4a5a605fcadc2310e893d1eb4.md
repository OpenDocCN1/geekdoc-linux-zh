
上面的 `read()` 调用使用了阻塞 I/O。在实际应用中，我们希望接受连接并使用 `select()` 或 `poll()` 进行多路复用。在本示例中，我们试图保持代码简单。

## dbcommand() 调用

以下调用是 RTA 执行实际工作的地方。我们将从客户端读取的 SQL 命令传递给 RTA 库进行进行验证、执行并填充 `outbuf`。我们根据 `dbcommand()` 的结果判断是将结果发回客户端还是关闭连接。正常情况下，PostgreSQL 客户端会有序关闭，`dbcommand()` 返回 `RTA_CLOSE`。

```c
dbret = dbcommand(inbuf, &incnt, outbuf, &outcnt);
switch (dbret) {
    case RTA_SUCCESS:
        write(connfd, outbuf, OUTSZ - outcnt);
        incnt = 0;
        break;
    case RTA_NOCMD:
        break;
    case RTA_CLOSE:
        close(connfd);
        connfd = -1;
    break;
    default:
        break;
}
```

## 写回调

这是 UI/客户端程序设置 alarm 列后调用的子程序。此类更新的典型 SQL 命令是 `UPDATE ztable SET alarm = 0`。在学习使用回调时，你可能想在回调中添加打印语句来显示表、输入的 SQL 和行号。

```c
/* zgedetect(), a write callback to print a message when
alarm structure member is set from zero to one
from零。我们还将 alarm 归一化为 0 或 1。 */
```

```c
int zgeddetect(char *tbl, char *col, char *sql, void *pr,
  int rowid, void *poldrow)
{
  /* 我们通过查看 zalarm 的旧值是否与新值不同来检测边缘变化。 */
  int oldalarm,
  int newalarm;

  /* 将非零值归一化为 1 */
  if (((struct ZData*) pr)->zalarm != 0) {
    ((struct ZData*) pr)->zalarm = 1;
  }

  oldalarm = ((struct ZData*) poldrow)->zalarm;
  newalarm = ((struct ZData*) pr)->zalarm;
  if (oldalarm != newalarm) {
    zdata[rowid].count++; /* 计数器 */
  }

  printf("Transition from %d to %d in row %d\n",
      oldalarm, newalarm, rowid);

  return(0); /* always succeeds */
}
```

通过比较 `zalarm` 的旧值和新值来检测转换。行的旧值和新值都作为参数传递给例程。在本示例中我们总是返回成功。

注意：如果写回调返回非零值，受影响的行将恢复到旧值，客户端程序将收到发送的 SQL 命令的错误结果。

## 安装 RTA

你可以在这本书的附带光盘上以及 RTA 项目网站（http://www.linuxappliancesesign.com）上找到 RTA 软件包。检查网站获取最新版本。RTA 中的 SQL 解析器是使用 `yacc` 和 `lex` 编写，因此如果你从源代码编译 RTA，你的开发系统需要安装这两个者。

RTA 的默认安装会将 `.a` 和 `.so` 库存于 `/usr/local/lib` 目录。如果你不想使用 `/usr/local/lib`，可以在安装前编辑 `Makefile`。你已经下载了 RTA 软件包，解压文件并构建库。下面的示例代码展示了如何操作。

```bash
# -xzf rta-X.Y.Z.tgz
# cd rta-X.Y.Z
# cd src
# make librtadb.so.2
# make install
```

## 构建与链接

现在在 `rta-X.Y.Z` 下创建一个测试目录，并将 `myapp.c` 复制其中。接下来，使用此命令构建应用程序：

```bash
# gcc myapp.c -o myapp -L/usr/local/lib -lrtadb
```

为了编译并运行应用程序，我们需要告诉系统在运行时查找 RTA 库的位置。你可以编辑 `/etc/ld.so.conf` 并运行 `ldconfig`，或者导出 `LD_LIBRARY_PATH` 环境变量。如果编译成功，你可以使用以下命令运行应用程序：

```bash
# export LD_LIBRARY_PATH=/usr/local/lib
# ./myapp
```

大搞定！你的示例应用程序应该已经运行，并准备好响应 PostgreSQL 请求。

## 测试

在本节中，我们假设你已经从 Linux 发行版或本书附带的 CD 中安装了 PostgreSQL，并且 `psql` 命令位于你的路径（`path`）中。如果一切顺利，你现在应该有一个运行中的伪装成 PostgreSQL 数据库服务器的应用程序。然而，我们的示例应用程序并不是数据库，而是将其内部表提供给各种 PostgreSQL 客户端使用。我们将首先使用的客户端是命令行工具 `psql`。

假设一切正常，打开另一个终端窗口并启动 `psql`，按如下方式指定数据库服务器的主机和端口。（记住，我们已经告诉应用程序监听 8888 端口。）

```bash
# psql -h localhost -p 8888
```

> PostgreSQL 应该返回类似的内容：

Welcome to psql 8.1.5, the PostgreSQL interactive terminal.

```
\copyright for distribution terms
\h for help with SQL commands
\? for help on internal slash commands
\g or terminate with semicolon to execute query
\q to quit
```

让我们给 `psql` 发一个简单的 SQL 命令：

```sql
# SELECT * FROM ztable;
| zname | zalarm | zcount |
|---|---|---|
| 0 | 0 | |
| 0 | 0 | |
| 0 | 0 | |
| 0 | 0 | |
(5 rows)
```

如果你的 SQL 命令没有显示上述表，你需要调试 RTA 的安装。最常见的问题是客户端与 RTA 之间的 PostgreSQL 协议不匹配。`psql` 客户端可能会给出警告，但它对使用新客户端连接旧服务器其实相当宽容。如果你使用的是最新的 `psql` 客户端，可能会出现这种情况。

检查 RTA 网站以查看你的 RTA 版本是否与 PostgreSQL 版本兼容。如果不兼容，请更新 RTA 或 PostgreSQL。本书的附带 CD 包含了已知兼容的 RTA 和 PostgreSQL 库版本。你也可以执行 `netstat -natp` 来验证应用程序是否真的在监听 8888 端口。

在进入 SQL 教程之前，让我们尝试几个命令看看应用程序的响应。

```sql
# UPDATE ztable SET zalarm = 1;
UPDATE 5
#
```

这应该会在启动 `myapp` 的控制台上打印出一条转换消息。（注意，`psql` 返回的是更改的行数，由于我们没有指定更改某一行，所以所有五行都被更新了）。

现在第二次执行相同的命令。

```sql
# UPDATE ztable SET zalarm = 1;
UPDATE 5
#
```

控制台上此时不应打印任何消息，因为这次没有发生转换。

将警报置回零应该会导致一次转换，现在的转换次数应该是 2。

```sql
# UPDATE ztable SET zalarm = 0;
UPDATE 5
# SELECT * FROM ztable;
| zname | zalarm | zcount |
|---|---|---|
| 0 | 2 | |
| 0 | 2 | |
| 0 | 2 | |
| 0 | 2 | |
```

当你首次启动 `./myapp` 时，保存的表配置文件 `/tmp/zsave.sql` 并不存在。通过对标记为 `RTA_DISKSAVE` 的列进行更新来创建它。

```sql
# UPDATE ztable SET zname = "row name";
UPDATE 5
#
```

你可以通过执行 `cat /tmp/zsave.sql` 来验证上述操作。你应该能看到以下：
