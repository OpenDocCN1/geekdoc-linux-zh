
```
CATALOG TCPIP NODE rmt_server
REMOTE db2host
SERVER 60000
OSTYPE LINUX
WITH "A remote Linux TCP/IP node"
```

无论节点是如何编目录的，都可以随时通过执行 `UNCATALOG NODE` 命令来取消编目录。该命令的语法为：

```
UNCALOG NODE [NodeName]
```

其中：

- `NodeName`：标识分配给要取消编目录节点的别名。

```
UNCALOG NODE rmt_server
```

# DB2 数据库的编目录与取消目录

在访问存储在远程服务器上的数据库之前，你必须在客户端工作站上对数据库进行编目录。幸运的是，对数据库进行编目录是一个相对直接的过程，可以使用控制中心（`Control Center`）、配置助手（`Configuration Assistant`）或执行 `CATALOG DATABASE` 命令来完成。`CATALOG DATABASE` 命令的基本语法为：

```
CATALOG [DATABASE | DB] [DatabaseName]
<AS Alias>
<ON [Path]> | AT NODE [NodeName]>
```

```
<AUTHENTICATION [AuthenticationType]>
<WITH "[Description]">
```

其中：

- `DatabaseName`：标识分配给要编目录数据库的名称。
- `Alias`：标识在编目录时分配给数据库的别名。
- `Path`：标识与要编目录数据库相关的目录层次和文件物理存储的位置（驱动器或目录）。
- `NodeName`：标识要编目录数据库所在的节点。指定的节点名称应匹配节点目录文件中的条目（即应对应于已编目录的节点）。
- `AuthenticationType`：标识当用户尝试访问数据库时身份验证的位置和方式。该参数的有效值包括：`SERVER`, `CLIENT`, `SERVER_ENCRYPT`, `KERBEROS TARGET PRINCIPAL [PrincipalName]`（其中 `PrincipalName` 是目标服务器的完全限定 Kerberos 主体名称）、`DATA_ENCRYPT` 和 `GSSPLUGIN`。
- `Description`：用于描述为编目录数据库在数据库目录中创建的条目的注释。该描述必须包含在双引号括起来。

因此，如果你想对物理存储在目录 `/home/db2data` 且被命名为 `TEST_DB` 的数据库进行编目录，你可以执行类似下面的 `CATALOG DATABASE` 命令来完成：

```
CATALOG DATABASE test_db AS test
ON /home/db2data
AUTHENTICATION SERVER
```

正如编目录 DB2 数据库有多种方法，取消编目录也有多种方法：使用控制中心、使用配置助手，或执行 `UNCATALOG DATABASE` 命令。`UNCATALOG DATABASE` 命令的语法为：

```
UNCATALOG [DATABASE | DB] [DatabaseAlias]
```

其中：

- `DatabaseAlias`：标识分配给要取消编目录数据库的别名。

所以，如果你想取消编目录名称和别名均为 `TEST_DB` 的数据库，可以执行如下所示的 `UNCATALOG DATABASE` 命令：

```
UNCATALOG DATABASE test_db
```

## DB2 发现 (Discovery)

很容易看出手动配置客户端和服务器工作站之间的通信如何变成一个复杂的过程，尤其在复杂的网络环境中。正如我们刚刚看到的，建立客户端与服务器之间的通信只是开始；在客户端向 DB2 服务器发送请求进行处理之前，服务器以及存储在服务器上的数据库也必须在客户端工作站上进行编目录。

`DB2 Discovery` 允许你轻松编目录远程服务器和数据库（建立客户端与服务器之间的分布式连接），而无需了解任何详细的特定通信信息。`DB2 Discovery` 的工作原理：当从客户端工作站调用时，`DB2 Discovery` 在网络上广播发现请求，网络上每个配置为支持发现过程的 DB2 服务器通过返回服务器上发现的实例列表、每个实例支持的通信协议信息以及每个实例内发现的数据库列表来响应。控制中心和配置助手可以使用这些信息对发现过程返回的任何实例或数据库进行编目录。

# 第 2 章：服务器管理

为了处理发现请求，`DB2 Discovery` 可以使用方法之一：(1) 搜索 (`search`) 和 (2) 已知 (`known`)。当使用搜索发现方法时，会在整个网络搜索有效的 DB2 服务器和数据库，向客户端返回发现的所有服务器、实例和数据库列表，以及编目录和连接每个项目所需的通信信息。相比之下，当使用已知发现方法时，将在网络上使用特定的通信协议搜索特定的服务器。（因为客户端知道服务器的名称以及该服务器使用的通信协议，所以该服务器被认为是“已知的”）。再次，当找到指定的服务器时，会向客户端返回服务器上发现的所有实例和数据库列表，以及编目录和连接每个项目所需的信息。

客户端是否可以启动发现请求、如果是如何启动、特定服务器是否会响应以及如果是如何响应，取决于 `DAS` 实例、`DB2` 数据库管理器（实例）以及该实例数据库配置参数的值。具体而言，这些参数控制：

- 客户端是否可以启动发现请求；
- 服务器是否可以被 `DB2 Discovery` 找到，如果是，是使用搜索发现方法还是已知发现方法；
- 是否可以通过发现请求找到实例；
- 是否可以通过发现请求找到数据库。

控制 `DB2 Discovery` 行为的 `DAS` 实例、`DB2` 数据库管理器和数据库配置参数详见表 2.6。

## 表 2.6 控制 DB2 Discovery 行为的配置参数

| 参数 | 值/默认值 | 描述 |
|---|---|---|
| 客户端实例 (`DB2` 数据库管理器配置文件) | | |
| `discover` | `SEARCH` | 标识客户端实例要使用的 DB2 发现操作。如果此参数设置为 `SEARCH`，客户端实例可以发布搜索或已知发现请求；如果此参数设置为 `KNOWN`，客户端实例仅可以发布已知发现请求；如果此参数设置为 `DISABLE`，客户端实例无法发布发现请求。 |
| `discover_inst` | `ENABLE`, `DISABLE` 默认值 `ENABLE` | 指定此实例是否可以被其他 DB2 Discovery 请求检测。 |
| 服务器 `DAS` 实例 (`DAS` 配置文件) | | |
| `discover` | `DISABLE`, `KNOWN`, `SEARCH` 默认值 `SEARCH` | 标识服务器启动时要使用的 DB2 发现操作。如果此参数设置为 `SEARCH`，服务器将响应搜索和已知发现请求。如果此参数设置为 `KNOWN`，服务器将仅响应已知发现请求；如果此参数设置为 `DISABLE`，服务器将不响应发现请求。 |
| 服务器实例 (`DB2` 数据库管理器配置文件) | | |
| `discover` | `DISABLE`, `KNOWN`, `SEARCH` 默认值 `SEARCH` | 标识服务器实例要使用的 DB2 发现操作。如果此参数设置为 `SEARCH`，服务器实例可以发布搜索或已知发现请求；如果此参数设置为 `KNOWN`，服务器实例仅可以发布已知发现请求；如果此参数设置为 `DISABLE`，服务器实例无法发布发现请求。 |
| 表 2.6 控制 DB2 Discovery 行为的配置参数（续） | | |
| 参数 | 值/默认值 | 描述 |
| --- | --- | --- |
| `discover_inst_inst` | `ENABLE` 或 `DISABLE` 默认值：`ENABLE` | 确定在服务器上发现的特定实例的信息是否会被包含在服务器对发现请求的响应中。如果此参数设置为 `ENABLE`，服务器将在对搜索和已知发现请求的响应中包含该实例的信息。如果此参数设置为 `DISABLE`，服务器将不会在对发现请求的响应中包含该实例的信息（也不会包含任何受该实例控制的数据库的信息）。此参数提供了一种从 DB2 Discovery 中隐藏实例及其所有数据库的方法。 |
| 数据库数据库（数据库配置文件）`discover_db` | `ENABLE` 或 `DISABLE` 默认值：`ENABLE` | 确定在服务器上发现的特定数据库的信息是否包含在服务器对发现请求的响应中。如果此参数设置为 `ENABLE`，服务器将在对搜索和已知发现请求的响应中包含该数据库的信息。另一方面，如果此参数设置为 `DISABLE`，服务器将不会在对发现请求的响应中包含该数据库的信息。此参数提供了一种从 DB2 Discovery 中隐藏单个数据库的方法。 |

如你所见，可以在服务器级、实例级和数据库级启用或禁用 `DB2 Discovery`，并控制客户端（以及服务器）如何发起发现请求。还可以配置服务器，使得在发出发现请求时，`DB2 Discovery` 无法看到一个或多个实例或数据库。图 2–16 显示了如何使用控制 `DB2 Discovery` 行为的配置参数来防止 `DB2 Discovery` 查看存储在服务器上的某些实例和数据库。
