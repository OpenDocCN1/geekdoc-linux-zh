
通过查看窗口标题，您可以轻松识别出您正在 DB2 命令窗口中工作，该标题始终包含图中标记高亮的“DB2 CLP”字样。在 DB2 命令窗口中，所有命令都必须以 `db2` 为前缀。例如，在上图中，发出两条语句：

```
db2 connect to sample
db2 select * from staff
```

对于 Linux，DB2 命令窗口的等效物是 Linux shell（或终端），其中 DB2 环境已通过执行 `db2profile` 文件设置好。默认情况下会创建此文件，并将其添加到 DB2 实例所有者的 `.login` 文件中。默认情况下，DB2 实例所有者是 `db2inst1`。

### B.4.2.2 DB2 命令行处理器

DB2 命令行处理器（CLP）与 DB2 命令窗口相同，唯一的例外是提示符是 `db2=>` 而不是操作系统提示符。要在 Windows 上启动 DB2 命令行处理器，请使用 `Start -> Programs -> IBM DB2 -> DB2COPY1 (Default) -> Command Line Tools -> Command Line Processor`，或者从 DB2 命令窗口或 Linux shell 中输入 `db2` 并按 `Enter`。提示符将如图 B.6 所示更改为 `db2`。

![](img/c4119654311ebf24679359ca130a5ee6_217_0.png)

**图 B.6 - DB2 命令行处理器 (CLP)**

注意，图 B.6 还说明了在 CLP 中工作时，您不需要在命令前加上 `DB2` 前缀。要退出 CLP，请输入 `quit`。

### B.4.2.3 DB2 命令编辑器

DB2 命令编辑器是 DB2 命令窗口或 DB2 命令行处理器的 GUI 版本，如图 B.7 所示。该工具在 DB2 9.7 版本中已弃用。

![](img/c4119654311ebf24679359ca130a5ee6_218_0.png)

**图 B.7 - DB2 命令编辑器**

## B.5 DB2 环境

图 B.8 提供了 DB2 环境的快速概览。

![](img/c4119654311ebf24679359ca130a5ee6_219_0.png)

**图 B.8 - DB2 环境**

该图展示了一个已安装 DB2 Express-C 的服务器。浅绿色的小框（环境变量、数据库管理器配置文件、数据库配置文件、DB2 配置注册表）是可以配置 DB2 服务器的不同区域，它们将在下一节中详细解释。较大的深绿色框代表一个实例，在此示例中，该实例的名称为 `myinst`。

实例是可以创建数据库对象的环境。在同一台服务器上，您可以创建多个实例，每个实例都被独立对待。例如，您可以将一个实例用于开发，另一个用于测试，还有一个用于生产。表 B.1 展示了一些您在实例级别可以使用的有用命令。请注意，本节中显示的命令也可以通过 DB2 GUI 工具执行。

| 命令 | 描述 |
|---|---|
| `db2start` | 启动当前实例 |
| `db2stop` | 停止当前实例 |
| `db2icrt <instance_name>` | 创建新实例 |
| `db2idrop <instance_name>` | 删除实例 |
| `db2ilist` | 列出您系统中的实例 |
| `db2 get instance` | 列出当前活动实例 |

**表 B.1 - 有用的实例级 DB2 命令**

在一个实例内，您可以创建许多数据库。**数据库**是对象（如表、视图、索引等）的集合。例如，在图 B.8 中，数据库 **MYDB1** 已在实例 `myinst` 中创建。**表 B.2** 展示了一些您在数据库级别可以使用的命令。

| 命令/SQL 语句 | 描述 |
| :--- | :--- |
| `create database <database_name>` | 创建新数据库 |
| `drop database <database_name>` | 删除数据库 |
| `connect to <database_name>` | 连接到一个数据库 |
| `create table/create view/create index` | 分别用于创建表、视图和索引的 SQL 语句 |

**表 B.2 - 数据库级别的命令和 SQL 语句**

## B.6 DB2 配置

可以使用配置顾问 GUI 工具配置 DB2 参数。可以通过控制中心访问配置顾问：右键单击数据库并选择 *Configuration Advisor*（配置顾问）。根据您对系统资源和负载等问题的回答，配置顾问将提供一组建议值的 DB2 参数列表，这些参数可以最优运行。如果您想更深入了解 DB2 配置，请继续阅读。否则，使用配置顾问后，您就可以开始使用 DB2 了！

如图 B.8 所示，DB2 服务器可以在四个不同级别进行配置：

- **环境变量**是在操作系统级别设置的变量。需要关注的主要环境变量是 `DB2INSTANCE`。该变量指示您当前操作的实例，您的 DB2 命令将应用于该实例。

- **数据库管理器配置文件 (dbm cfg)** 包含影响实例及其包含的所有数据库的参数。*表 B.3* 展示了一些管理 dbm cfg 的有用命令。

| 命令 | 描述 |
| :--- | :--- |
| `get dbm cfg` | 检索有关 dbm cfg 的信息 |
| `update dbm cfg using <parameter_name> <value>` | 更新 dbm cfg 参数的值 |

**表 B.3 - 用于操作 dbm cfg 的命令**

- **数据库配置文件（db cfg）** 包含影响特定数据库的参数。*表 B.4* 列出了一些用于管理 db cfg 的常用命令。

| 命令 | 描述 |
|---|---|
| `get db cfg for <database_name>` | 检索指定数据库的 db cfg 信息 |
| `update db cfg for <database_name> using <parameter_name> <value>` | 更新 db cfg 参数的值 |

**表 B.4 - 用于操作 db cfg 的命令**

- **DB2 概要文件注册表变量** 包含可能因平台而异的参数，这些参数可以全局设置（影响所有实例）或在实例级别设置（影响特定实例）。*表 B.5* 列出了一些用于操作 DB2 概要文件注册表的常用命令。

| 命令 | 描述 |
|---|---|
| `db2set -all` | 列出所有已设置的 DB2 概要文件注册表变量 |
| `db2set <parameter>==<value>` | 将给定参数设置为指定值 |

**表 B.5 - 用于操作 DB2 概要文件注册表的命令**

## B.7 连接数据库

如果数据库是本地的，即位于执行数据库操作的同一系统上；在创建数据库时，连接设置会自动完成。只需发出 `connect to database_name` 语句即可连接到数据库。

如果数据库是远程的，设置数据库连接的最简单方法是使用配置助手（Configuration Assistant）GUI 工具，按以下步骤操作：

1. 从希望连接数据库的系统启动配置助手。启动此工具时，请在 Windows 命令提示符或 Linux shell 中使用命令 `db2ca`。*图 B.9* 展示了配置助手。

![](img/c4119654311ebf24679359ca130a5ee6_222_0.png)

图 B.9 - DB2 配置助手

2. 在配置助手中，点击 *Selected -> Add database using Wizard* 菜单。

3. 在 *Select how you want to set up a connection*（选择如何设置连接）窗口中，如果网络较小且没有太多集线器，可以使用 *Search the network*（搜索网络）。如果知道运行 DB2 的服务器名称，请选择 *Known systems*（已知系统）并一直向下钻取直到找到要连接的数据库。使用默认值继续向导操作。如果不知道系统名称，请选择 *Other systems (Search the network)*（其他系统（搜索网络））。请注意，如果网络很大，这可能需要较长时间。
