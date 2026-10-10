
## MySQL 图形化工具

`MySQL` 拥有一个名为 `MySQLGUI` 的图形化时间较长的工具。该工具仍可从 `MySQL` 网站获取，但目前的开发重心已转向替代工具 `MySQL Control Center`（即 `MySQLCC`）。`MySQL Control Center` 是一个非常有用的全方位工具，值得安装。

我们强烈建议查看 `MySQLCC`；它为一个强大的、稳定的且易于使用的 `MySQL` 图形界面，提供了适用于 `Linux` 和 `Windows` 的预编译版本（如果你需要，甚至可以获得源代码）。它允许你通过 `GUI` 界面管理 `MySQL` 服务器并执行 `SQL`。

如果你的 `Linux` 发行版中没有提供 `MySQLCC`，你可以从 `MySQL` 网站下载副本并按照简单的安装说明操作。或者，你也可以从运行在 `Windows` 桌面上的 `MySQLCC` 直接管理运行在你的 `Linux` 服务器上的 `MySQL` 副本。它的外观和运行方式几乎完全相同。

### 初次运行

第一次运行 `MySQLCC` 时，你将看到一个空白的控制中心窗口，其中控制台管理器也是空的，如图 8-2 所示。将鼠标悬停在工具栏上的第一个图标上，会显示这是创建新连接的图标。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_363_0.png)

图 8-2

### 配置连接

当你点击此按钮时，会在额外的弹出窗口中要求你输入一些基本信息（见图 8-3）。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_364_0.png)

图 8-3

如果你想从 `Windows PC` 远程管理服务器，那么配置过程几乎相同，仅需要在 `Host Name` 字段中输入主机名或 IP 地址，如图 8-4 所示。

![](img/514272414a3a6a6c81e4d1e9d75bbc1_364_1.png)

图 8-4

你需要提供的所有信息包括识别连接的名称（你可以选择任何名称）、主机名、用户名和密码。所有其他值都由系统默认填充。然后点击 `Test` 按钮，它会告诉你哪个连接是正常的。

然后点击 `Add` 将此连接添加到列表中。名称 `gw1`（或你选择的任何名称——`gw1` 恰好是它运行的机器的名称）应该显示在 `MySQL` 服务器列表中，通过点击它，你应该能够展开更多信息，如图 8-5 所示。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_365_0.png)

图 8-5

### 管理数据与用户

如果你探索数据库部分，你可以看到表格，通过右键点击表格，可以编辑表格定义或表中的数据，如图 8-6 所示。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_366_0.png)

图 8-6

你还可以编辑用户及其权限、执行 `SQL`、查看与数据库的连接，以及进行许多其他操作。

## 从 C 访问 MySQL 数据

现在我们已经掌握了 `MySQL` 的基础知识，让我们探索如何从自己的应用程序访问它，而不是使用 `mysql` 或基础的 `mysql` 客户端。

`MySQL` 可以通过许多不同的语言访问。我们知道有：

- `C`
- `C++`
- `Java`
- `Perl`
- `Python`
- `REXX`
- `Tcl`
- `PHP`

`ODBC` 驱动也可用于从 `Access` 等 `Windows` 原生应用程序访问 `MySQL`；甚至有适用于 `Linux` 的 `ODBC` 驱动，尽管使用它的人寥寥无几。

在本章中，我们将限于 `C` 接口，因为它是本书的重点，而且相同的库方便了许多其他语言的连接。

### 连接例程

从 `C` 连接到 `MySQL` 数据库涉及的两个步骤：

- 初始化连接句柄
- 物理上建立连接

首先我们将使用 `mysql_init` 来初始化我们的连接句柄：

```c
*mysql_init (MYSQL *);
```

通常你向该程序传递 `NULL`，返回一个指向新分配连接句柄的指针。如果你传递一个现有结构，它将被重新初始化。如果出错，则返回 `NULL`。到目前，我们只是简单地分配并初始化了一个结构。我们仍然需要为 `mysql_real_connect` 提供连接参数：

```c
MYSQL *mysql_real_connect(MYSQL *connection,
const char *server_host,
const char *user_name,
const char *sql_password,
const char *db_name,
unsigned int *port_number,
const char *unix_socket_name,
unsigned int *flags);
```

连接指针必须标识一个已使用 `mysql_init` 初始化的结构。参数非常直白易懂；但需要注意的是，`server_host` 可以接受主机名或 IP 地址。如果仅连接到本地机器，我们可以通过指定 `localhost` 来优化连接。`user_name` 和 `sql_password` 正如其名所示。如果登录为 `NULL`，你将能够无密码访问服务器上的数据。`port_number` 和 `unix_socket_name` 的值由系统为你默认填充。
