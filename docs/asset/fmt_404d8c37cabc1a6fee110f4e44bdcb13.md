
`92.1.125.124`        `db2server` # `db2server` 的主机地址

其中：

- `92.1.125.124` 是远程 DB2 服务器的 IP 地址
- `db2server` 是远程 DB2 服务器的主机名
- `#` 表示描述此条目的注释开始

提示：如果服务器与客户端不在同一域内，您必须提供完全限定域名，例如 `db2server.vnet.com`，其中 `vnet.com` 是域名。

### 3. 更新本地的 `/etc/services` 文件
如果您计划仅使用远程 DB2 服务器的端口在 DB2 客户端和 DB2 服务器之间建立通信，可以跳过此步骤。

使用文本编辑器，以 root 权限的用户为 DB2 客户端的 services 文件添加任意的服务名和与远程 DB2 服务器端口匹配的端口号，以支持 TCP/IP。例如：

```
db2inst1 50000/tcp # DB2 客户端服务名 & 匹配的 DB2 服务器端口
```

其中：

- `db2inst1` 是代表 DB2 客户端端口的任意本地名称。
- `50000` 是远程 DB2 服务器数据库配置文件中的 `svcename` 参数在其远程服务器 `/etc/services` 文件中映射的端口号。DB2 客户端使用的端口号必须与服务器上使用的端口匹配。
- `tcp` 是您正在使用的协议。
- `#` 表示描述此条目的注释开始。

提示：如果您计划支持使用网络信息服务 `NIS` 的基于 Unix 的 DB2 客户端，必须更新位于 NIS 主服务器上的 `/etc/services` 文件。

### 4. 注册 TCP/IP 节点
您必须在 DB2 客户端上添加条目来描述远程 DB2 服务器。此条目指定了 `node_name`、主机名或 IP 地址以及 DB2 客户端将使用的 `svcename` 或端口号。

注册 TCP/IP 节点，请执行以下步骤：

a. 以 `SYSADM` 权限的用户登录 DB2 服务器。例如，实例 `db2inst1`。

b. 输入以下命令注册 TCP/IP 节点：

```
catalog tcpip node node_name remote hostname or ip_address server svcename or port number
```

例如，要注册节点 `db2server` 的远程服务器，使用服务名 `db2inst1`，输入以下命令：

```
catalog tcpip node db2server remote db2server server db2inst1
```

要注册节点 `db2server` 的 IP 地址为 `92.1.125.124` 的远程服务器，使用端口号 `50000`，输入以下命令：

```
catalog tcpip node db2server remote 92.1.125.124 server 50000
```

### 5. 注册数据库
在客户端应用程序访问远程数据库之前，必须在 DB2 服务器和任何连接它的 DB2 客户端上注册该数据库。当您在 DB2 服务器上创建数据库时，它会自动在 DB2 服务器上注册，别名与数据库名相同。

注册数据库，请执行以下步骤：

a. 识别并记录所需的数据库参数。这些参数如表 7.2 所示。

| 参数 | 描述 | 示例值 | 您的值 |
| --- | --- | --- | --- |
| 数据库名 (`database_name`) | 远程 DB2 数据库的数据库别名 (`database_alias`)。当 DB2 安装程序创建 SAMPLE 数据库时，它会自动在 DB2 服务器上注册，别名与数据库名相同。 | SAMPLE | |
| 数据库别名[2] (`database_alias`) | 客户端上远程数据库的本地昵号。如果不提供，默认值与表中的 `database_name` 参数相同。该名称在 DB2 客户端上必须是唯一的。建议您使用与数据库名（远程数据库的数据库别名）相同的名称以避免混淆。这是您从 DB2 客户端连接到数据库时使用的名称。 | SAMPLE | |

| Node name (`node_name`) | 您正尝试连接的远程 remoteddb2server DB2 数据库的本地别名。计算机通常被称为节点。请使用您在上一步中编目录节点时使用的相同名称。 |

## 表格 7.2 客户端到服务器通信所需的数据库参数

b. 以具有 `SYSADM` 或 `SYSCTL` 权限的用户身份登录系统。在我们的示例中，您可以使用实例所有者 ID `ID db2inst1`。

**提示** 如果您使用此 `su` 命令登录系统，您**必须**带有 `--` 参数输入此命令；例如，`su -- db2inst1`。如果您不使用此参数，您将收收到一个错误，因为 DB2 将无法正确读取 DB2 配置文件（profile）。

c. 输入以下命令编目录数据库：
`db2 "catalog database database_name as database_alias at node node_name"`
`db2 terminate`

例如，为了对一个已使用数据库别名 `SAMPLE` 编目录的*远程*数据库，使其在节点 `db2server` 上拥有*本地*数据库别名 SAMPLE，请输入以下命令：

```
db2 "catalog database sample as sample at node db2server"

db2 terminate
```

### 6. 您已经完成了通信客户端的配置！
要将 DB2 客户端连接到 DB2 服务器，请执行以下步骤。

**注意** 在连接到远程数据库之前，您必须已经启动了远程 DB2 服务器上的数据库管理器。在我们的示例中，您创建的实例默认配置为自动启动（autost）。如果您已停止该实例，在完成这些步骤之前，您必须在远程 DB2 服务器上以 `db2inst1` 用户身份输入 `db2start` 命令。

a. 以 `db2inst1` 用户 ID 登录系统。

**提示** 如果您使用此 `su` 命令登录系统，您**必须**带有 `--` 参数输入此命令；例如，`su -- db2inst1`。如果您不使用此参数，您将收收到一个错误，因为 DB2 将无法正确读取 DB2 配置文件。

b. 输入以下命令连接到远程数据库：

`db2 connect to database_alias user userid using password`

其中：

- - `database_alias` 是 DB2 客户端为远程 DB2 数据库定义的别名。
- - `userid` 是在远程 DB2 服务器上定义的用户 ID。在我们的示例中，使用 `db2inst1` 用户。
- - `password` 是您指定的 `userid` 的密码。

如果您一直遵循我们的示例，并在 DB2 服务器和 DB2 客户端上创建了具有相同密码的用户 ID，则您不需要在此命令中指定 `userid` 和 `password` 参数。默认情况下，DB2 客户端将把当前用户的用户 ID 和密码传递给 DB2 服务器进行身份验证。由于它们是相同的，这对于本示例来说不是问题。

例如，以用户 `db2inst1` 的身份连接到数据库别名为 SAMPLE 的远程 DB2 数据库（该数据库在 DB2 客户端上已以本地数据库别名 SAMPLE 编目录），请输入以下命令：

```
db2 connect to sample
```

> 注意：在连接到远程 DB2 数据库时，不需要使用 `userid` 和 `password` 参数。当您安装 DB2 客户端时，您创建了一个与客户端上相同的用户 ID (`db2inst1`) 和密码的用户。这样做是为了简化示例。如果您使用一个在远程 DB2 服务器上未定义的用户登录 DB2 客户端，则您必须使用 `userid` 和 `password` 参数来指定一个有效用户。

您应该收到以下输出：

```
Database server = DB2/LINUX 6.1.0

SQL authorization ID = DB2INST1

Local database alias = SAMPLE
```

c. 输入以下命令选择 staff 表中属于部门 20 的所有员工列表：

```
db2 "select * from staff where dept = 20"
```
