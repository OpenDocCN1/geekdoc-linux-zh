
`<instance_hostname>` 是注册备用 DB2 实例时使用的 IP 地址（在示例中为 9.26.96.91）。

### 16. 作为备用实例所有者 (`db2insts`)，如下所示更新备用数据库 (`haddrb`) 的备用服务器：

- `(S) % db2 update alternate server for database haddrb using hostname <instance_hostname> port 60000`

`<instance_hostname>` 是注册主 DB2 实例时使用的 IP 地址（在示例中为 9.26.96.90）。

### 17. 作为备用实例所有者 (e.g., `db2insts`)，如下所示在备用实例（例如，`hadr02`）上启动 HADR：

- `(S) % db2 start hadr on db hadrb as standby`

忽略信息：“Logindex build was not enabled before HADR started.”

请确保记住以下几点：

- a. 始终在编目录之前先在备用实例上启动 HADR。
- b. 在每个客户端上，确保主节点 (`hadr01`) 已编目录。示例如下：

```
(H) % db2 catalog tcpip node db2inst remote hadr1 server 60000
```

- c. 每个客户端必须至少连接一次主实例，以便获取备用服务器信息。此外，客户端必须通过 TCPIP 节点条目连接，而不是通过本地节点条目。如果您希望通过本地节点条目连接（例如客户端与数据库位于同一节点），则必须创建一个引用本地实例的 TCPIP 编条目（即环回条目）。
- d. 如果使用 Java 数据库连接 (`JDBC`) 类型 4 客户端，将无法从本地目录获取客户端重路由信息。应用程序必须设计为在文本文件中存储和恢复备用服务器信息。

### 18. 作为主实例所有者 (`db2inst`)，如下所示在主节点 (`hadr02`) 上启动 HADR：

```
(P) % db2 start hadr on db hadrb as primary
```

忽略信息：“Logindex build was not enabled before HADR started”。

### 19. 作为实例所有者 (`db2instp`)，确保 HADR 对处于 Peer 状态，如下：

```
(S) % db2 get snapshot for db on hadrb
```

您应该在主节点 (`hadr01`) 上看到类似下方的输出：

```
HADR Status Role = Primary

State = Peer

Synchronization mode = sync

Connection status = Connected, 11/08/2006 13:50:19.62630

Heartbeats missed = 0

Local host = hadr01

Local service = 18819

Remote host = hadr02

Remote service = db2inst

timeout(seconds) = 30

Primary log position(file, page, LSN) = S0000000.LOG, 0, 0000000000700000

Standby log position(file, page, LSN) = S0000000.LOG, 0, 0000000000700000
```

您应该在备用节点 (`hadr02`) 上看到类似下方的输出：

```
HADR Status Role = Standby

State = Peer

Synchronization mode = sync

Connection status = Connected, 11/08/2006 13:50:19.62630

Heartbeats missed = 0

Local host = hadr02

Local service = 18820

Remote host = hadr01

Remote service = 18819

Remote instance = db2instp

timeout(seconds) = 30

Primary log position(file, page, LSN) = S0000000.LOG, 0, 0000000000700000

Standby log position(file, page, LSN) = S0000000.LOG, 0, 0000000000700000
```

## 使用 TSA 注册 HADR 以自动管理

在这一步中，我们启用 TSA 自动监控和管理 HADR 对。
我们通过将 HADR 对作为资源组注册到 TSA 来实现。

在将 HADR 注册为 TSA 资源组后，请勿手动执行 DB2 “Takeover”（切换）命令。相反，使用以下命令手动重启 HADR：

```
# chrg -o online <resource_group_name>
```

其中 `<resource_group_name>` 是 TSA 给 HADR 资源组的名称，例如 `db2hadr_hadrb-rg`。

对于操作员故障转移，执行以下命令：

```
# rgeq -o move -n <node> <resource_group_name>
```
其中 `<node>` 是数据库 (`hadrb`) 具有“Primary”角色的节点 (`hadr01`)。`<resource_group_name>` 是 TSA 给资源组的名称，例如 `db2hadr_hadrb-rg`。

现在按照以下步骤操作：

- 1. 作为主节点 (`hadr01`)，为 HADR 对创建资源组：

```
(P) # rgh -a db2instp - hadrb
```
- 2. 执行此命令检查所有资源组的状态：

```
(P) # getstatus
```
如果您设置了 HA 地址（如第 29 页“Set up highly IP”所示），您应该看到类似下方的输出。如果您没有设置 HA 地址，下面的输出将不包含 IP 资源：

-- Resource Groups and Resources --

| 组名称 | 资源 |
|---|---|
| db2_dbinst_0-rg | db2_dbinst_0-rs |
| db2_dbinst_0-rg | db2_dbinst_0-rs_ip |

-- Resources --

| 资源名称 | 节点名称 | 状态 |
|---|---|---|
| db2_dbinst_0-rs | | |
| db2_dbinst_0-rs_ip | | |
| db2_dbinst_0-rs | hadr01 | Online |
| db2_dbinst_0-rs_ip | hadr01 | Online |
| db2_dbinsts_0-rs | hadr02 | Online |
| db2_dbinsts_0-rs_ip | hadr02 | Online |
（此处根据原文格式对齐）

**注意：** HADR 资源在线的节点（例如 `db2hadr_hadrdb-rs`）是数据库处于主模式的节点。

## 10.3.3 测试拓扑对故障的响应

在以下所有用例中，假设 `hadrb` 在 `hadr01` 上为主，且所有实例资源组均已上线。

接下来我们解释执行 `getstatus` 命令后看到的状态含义：

- 对于实例：
  - Online：表示实例正在运行。
  - Offline：表示实例已停止。
  - Unknown：表示实例状态未知。
- 对于 HADR 资源：
  - Online：表示 HADR 数据库在节点名称处处于主节点。
  - Offline：表示 HADR 数据库在节点名称处处于备用节点。
  - Unknown：表示 HADR 数据库不在 Peer 状态或 HADR 数据库已停止。

## 控制切换测试

以下是进行切换测试的步骤：

- 1. 以 root 身份将“`db2_hadr-hadrdb-rs`”资源从主节点 (`hadr01`) 移动到备用节点（例如，`hadr02`）；换句话说，如下执行控制故障转移（忽略“token”信息）：

```
# rgreq -o move -n hadr01 db2_hadr_hadrdb-rg
```

忽略“token”信息。

以 root 身份，如下检查主数据库 (`hadrdb`) 是否已成功切换到备用节点 (`hadr02`)：

```
(P) # status
```
