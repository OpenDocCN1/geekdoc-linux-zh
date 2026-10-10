
| 围栏所有者 | `db2fenc` | `db2adm1` |

| DB2 管理服务器 | `db2as` | `db2grp` |

- 实例所有者的目录是创建 DB2 实例的地方。
- 围栏所有者用于在 DB2 数据库地址空间之外运行用户定义函数 (`UDF`) 和存储过程。
- DB2 管理服务器的用户 ID 用于在您的系统上运行 DB2 服务。

创建 DB2 所需组和用户 ID 的命令取决于操作系统，此示例为 AIX：

```
mkgroup id=999 db2iadm1
mkgroup id=998 db2fadm1
mkgroup id=997 db2grp
```

为每个组创建用户（AIX 示例）：

```
mkuser id=1004 pgrp=db2iadm1 groups=db2iadm1 home=/home/db2inst
db2inst passwd mypassword
mkuser id=1003 pgrp=db2fadm1 groups=db2fadm1 home=/home/db2fenc
db2fenc passwd mypassword
mkuser id=1002 pgrp=db2asgrp groups=db2asgrp home=/home/db2as
db2as passwd mypassword
```

> 注意：您必须拥有 root 权限创建用户和组，只要符合系统命名规则和 DB2 命名规则即可指定您的用户和组名称，请参考《DB2 UDB V8.1 快速入门》中的“命名规则”。

## 2. 创建 DB2 管理服务器 (DAS)

对于 AIX，执行此命令创建 DAS：

```
/usr/opt/db2_08001/instance/dascrt -u DASUser
```

## 3. 使用 `db2icrt` 创建实例

以具有 root 权限的用户登录并执行以下命令（AIX 示例）：

```
DB2DIR/instance/db2icrt -a AuthType -u FencedID InstName
```

# 第 2 章 入门

- `DB2DIR` 是 DB2 的安装目录，在 AIX 上它为 `/usr/opt/db2_08_01`
- `-a AuthType` 是实例的身份验证类型：`SERVER`、`CLIENT`、`SERVER_ENCRYPT`。此参数为可选，默认认为 `SERVER`。
- `-u FENCED` 代表运行围栏用户定义函数 (`UDFs`) 和围栏存储过程的用户名称。
- `INSTNAME` 是 DB2 实例的名称。实例名称必须与拥有该实例的用户名称相同。请指定你创建的实例所有者的名称。实例将在该实例所有者的家目录下创建。

## 4. 为实例设置通信

`DB2COMM` 注册表变量允许你为 DB2 实例设置通信协议。该变量可以设置为以下关键字的任意组合，并用逗号分隔：

- `APPC` 启动 `APPC` 支持
- `NETBIOS` 启动 `NETBIOS` 支持
- `NIPE` 启动 命名管道（`NAMED PIPE`）支持
- `TCIP` 启动 `TCP/IP` 支持

例如，要设置数据库管理器和 DAS 服务启动 TCP/IP 的连接管理器，请输入：

```
db2set DB2COMM=tcpip
db2set DB2DAS00 DB2COMM=tcpip
db2stop
```

数据库管理器配置文件有一个参数 `SVCNAME`，它被分配为实例的主连接端口名称，并定义在 `etc/services` 文件中。例如，如果服务文件中定义的名称为 `db2c_DB2`，则更新数据库管理器配置文件的命令如下：

```
update dbm cfg using svcename db2c_DB2
```

在 `/etc/services` 文件中对应的条目为：

```
db2c_DB2 5000/tcp
db2i_DB2 5001/tcp
```

## 5. 更新产品许可密钥

请参考 DB2 命令参考手册中的 `DB2LICM` 命令。

> 注意：请记住在 UNIX 环境中，所有命令都是大小写敏感的。有关手动安装的更多信息，请参考《安装和配置补充说明》。

# 启动 DB2 实例

现在 DB2 实例已经创建，必须对其进行初始化或启动。启动实例的过程类似于启动网络文件服务器；在实例启动之前，客户端将无法访问服务器上的数据库。

启动 DB2 实例的命令是 `DB2START`。此命令将在服务器上分配所有所需的 DB2 资源。这些资源包括内存和通信支持。

```
db2start
SQL1063N DB2START processing was successful.
```

在 Windows 上，你也可以使用以下命令启动实例：

```
net start instance_name
```

# 停止 DB2 实例

停止当前数据库管理器实例的命令是 `DB2STOP`。消息将到标准输出，指示 `DB2STOP` 命令的成功或失败。

```
DB2STOP
SQL1064N DB2STOP processing was successful.
```

在 Windows 上，你也可以使用命令停止实例：

```
net stop instance_name
```

# 实例管理

本节介绍了如何在本地和远程管理 DB2 实例。DB2 中的某些任务只能在实例级别执行，例如创建数据库、强制用户断开数据库、监控数据库或更新数据库管理器配置。其他任务需要数据库连接，例如发布 SQL 数据操纵语言（DML）语句、使用 `LOAD` 工具或使用 `BIND` 命令。

实例的远程和本地管理都可以使用控制中心（Control Center）完成。`ATTACH` 命令可以通过命令行用于本地和远程管理任务。

要附加到实例，可以使用 `ATTACH` 命令。`ATTACH` 命令的语法如下：

```
ATTACH [TO nodename] [USER username USING password]
```

如果执行不带参数的 `ATTACH` 命令，将返回你当前附加的节点名称。如果你在附加到另一个实例时尝试附加到另一个实例，当前实例将断断开，并尝试新的附加。换句话说，你一次只能附加到一个实例。

> 注意：当前激活的实例可以通过 `GET INSTANCE` 命令进行识别，该命令返回 `DB2INSTANCE` 环境变量的值。

数据库连接与实例附加是相互独立的。单个应用程序在保持一个实例附加的同时，可以同时维护多个数据库连接，但在任何时刻只能维护一个实例附加。数据库连接可以是隐式的或显式的。隐式数据库连接将连接到由 `DB2DBDFT` 注册表变量指定的数据库。显式数据库连接可以使用 `CONNECT TO DATABASE` 语句创建。

本地实例由 `DB2INSTANCE` 变量中包含的值决定。当附加到第二个实例时，你正在使用本地实例的目录服务。你无法在第二个实例中对数据库、节点或 DCS 目录（仅在安装了 DB2 Connect 时使用）进行目录更改，或列出、更新或重置目录。

# 本地实例管理

在服务器上安装 DB2 并创建实例后，用户可以通过两种方式之一访问此实例：

- 通过将 `DB2INSTANCE` 环境变量设置为实例名称。必须将 `DB2PATH` 环境变量设置为 DB2 可执行文件所在的位置。这被称为*隐式附加*。
- 通过对本地实例进行目录编目并发布 `ATTACH` 命令。这被称为*显式附加*。

# 实例附加

此场景研究了一个用户想要访问同一服务器上两个实例的情况。这两个实例是 `DBTEST` 和 `DB2`。她通过以下方式定义了本地节点：

```
/home/dbtest/sqlib/db2
```

Dana 还想访问 DB2 实例。她通过以下命令编目节点：

```
catalog local node
```

在此示例中：

- `LOCAL` 表示这是一个本地实例。
- `MYDB2` 是给节点的别名。
- `DB2` 是要访问的实例名称。

可以使用 `LIST NODE` 查看节点目录的内容：

### 节点目录

目录中有 2 个条目

第 1 个条目：

```
Node name      = MYDB2
Comment         = 
Protocol        = LOCAL
Instance name  = db2
```

要访问名为 `DB2` 的实例中的数据库，Dana 必须使用以下命令编目数据库：

```
catalog db2cert as mycert node mydb2
```

在此示例中：

- `DBCERT` 是实例中的数据库名称。
- `MYCERT` 是用户连接时使用的别名。
- `MYDB2` 是实例的本地别名。

如果 Dana 发布 `DIRECTORY` 命令，输出如下：

# 系统目录

目录中有 1 个条目

第 1 个数据库：
