
## 配置自动客户端重定向数据库

客户端重定向允许客户端应用程序在 HADR 故障转移后，以最小中断继续对其正在访问的数据库的操作。

- 主数据库 - `LEAD` - `db2inst1` - `SAMPLE`

| | | |

| :--- | :--- | :--- |

| 主机名 | `LEAD` | 查看 IP 信息... |

| HADR 服务名称 | `DB2_HADR_1` | 查看服务文件... |

| HADR 端口号 | | `55001` |

- 备用数据库 - `POLONIUM` - `DB2_POL` (`db2inst1`) - `SAM_POL` (`SAMPLE`)

| | | |

| :--- | :--- | :--- |

| 主机名 | `polonium` | 查看 IP 信息... |

| HADR 服务名称 | `DB2_HADR_2` | 查看服务文件... |

| HADR 端口号 | | `55002` |

12. 检查点击“完成”时将发生的操作（图 3-12）：此对话框显示了所选 HADR 的概述。点击“显示命令”以获取命令行语句，了解场景中发生的情况。这些命令值得保存到文本文件中，供后续配置使用。

13. 步骤执行：图 3-13 显示了自动化脚本生成并运行的命令的动态摘要。如果遇到任何问题，向导将告知您必须修正的内容，您应该能够点击上一个对话框上的完成 (Finish) 以重试该过程。

![](img/a97b7826c3cf736045d80f48b5520a20_80_0.png)

图 3-13 开始处理脚本化 HADR 设置的步骤

图3-14 显示了完成的步骤，这是您预期的结果。HADR 设置已完成。点击关闭 (Close)。

![](img/a97b7826c3cf736045d80f48b5520a20_81_0.png)

图 3-14 *脚本化 HADR 设置的完成步骤*

14. *验证 HADR 设置：* 要确认 HADR 正在运行，您可以检查 DB2 控制中心（DB2 Control Center）。

首先，选择视图 (View) →刷新 (Refresh)，否则它会将远程数据库显示为“未知 (unknown)”。接下来，右键点击 HADR 数据库之一，选择高可用性灾难恢复 (High Availability Disaster Recovery) →管理 HADR (Manage HADR)。结果应类似于图 3-15。

如果您在第 11 步中将启动 HADR 的选项留空（见第 62 页的图 3-12），可以在此处点击“启动 HADR...”，这将显示您的数据库处于对等（Peer）状态，并具有相应的同步模式、连接状态以及每个数据库的日志信息。您可以使用 `GET SNAPSHOT` 命令或 `db2pd` 获取类似的信息。

> 注意：使用 DB2 版本 8 时，我们建议至少使用 FixPak 14 以修正管理 HADR 对话框中的 `SYNCMODE` 差异。

![](img/a97b7826c3cf736045d80f48b5520a20_82_0.png)

图 3-15 控制中心中：管理 HADR

### 3.2.3 命令行设置

DB2 为 HADR 提供了命令和 GUI 设置向导。在本节中，我们演示了如何使用命令设置 HADR。在我们的实验环境中，我们将 `LEAD` 服务器设置为为主服务器，将 `POLONIUM` 服务器设置为备用服务器，并在两个服务器上都建立了 `SAMPLE` 数据库。

要为命令行环境设置 HADR，请完成以下步骤：

- 1. 设置所需的数据库配置参数

如果尚未开启存档日志，请使用以下命令更新 `LOGRETAIN` 参数：

```
db2 update database configuration for sample using LOGRETAIN recovery
```

同样，使用以下命令更新 `LOGINDEXBUILD` 参数，以便对索引的创建、重新创建或重组操作进行记录：

```
db2 update database configuration for sample using LOGINDEXBUILD ON
```

- 2. 在主服务器上备份您的数据库，并使用以下命令将副本移动到备用服务器：

```
db2 backup database sample to /usr/db2/backup
```

- 3. 在备用系统上恢复数据库。

在示例中，我们使用以下命令恢复到 `POLONIUM` 服务器上的 `SAMPLE` 数据库：

```
db2 restore database sample from /usr/db2/backup taken at 200611114321 replace history file
```

- 4. 为 ACR 配置数据库。此步骤是可选的，但强烈建议执行。要配置 ACR，请按照步骤在主、备用服务器上更新 `ALTERNATE SERVER` 数据库配置：

  - a. 在主服务器上（我们的测试用例中为 `LEAD`），使用以下命令将备用服务器设置为备服务器：

```
db2 update alternate server for database sample using hostname polonium port 50001
```

  - b. 在备用服务器上（我们的测试用例中为 `POLONIUM`），使用以下命令将主服务器设置为备服务器：

```
db2 update alternate server for database sample using hostname lead port 50001
```

- 5. 在主系统 `LEAD` 的 `services` 文件中更新以下字段以进行 HADR 通信：

  - 服务名称：`DB2_HADR_1`

  - 端口号：`55001`

  - 服务名称：`DB2_HADR_2`

  - 端口号：`55002`

- 6. 在备用系统 `POLONIUM` 的 `services` 文件中更新以下字段以进行 HADR 通信：

  - 服务名称：`DB2_HADR_1`

  - 端口号：`55001`

  - 服务名称：`DB2_HADR_2`

  - 端口号：`55002`

- 7. 使用以下命令更新主数据库上的 HADR 数据库配置参数。在我们的测试用例中，它是 `LEAD`。

```
db2 update db cfg for sample using HADR_LOCAL_HOST LEAD
db2 update db cfg for sample using HADR_LOCAL_SVC DB2_HADR_1
db2 update db cfg for sample using HADR_REMOTE_HOST POLONIUM
db2 update db cfg for sample using HADR_REMOTE_SVC DB2_HADR_2
db2 update db cfg for sample using HADR_REMOTE_INST DB2INSTI
db2 update db cfg for sample using HADR_TIMEOUT 3
db2 update db cfg for sample using SYNC
db2 update db cfg for sample
```

- 8. 在备用数据库（我们的测试用例中为 `POLONIUM`）上使用以下命令更新 HADR 数据库配置参数：

```
db2 update db cfg for sample using HADR_LOCAL_HOST POLONIUM
db2 update db cfg for sample using HADR_LOCAL_SVC DB2_HADR_1
db2 update db cfg for sample using HADR_REMOTE_HOST LEAD
db2 update db cfg for sample using HADR_REMOTE_SVC DB2_HADR_2
db2 update db cfg for sample using HADR_REMOTE_INST DB2INSTI
db2 update db cfg for sample using HADR_TIMEOUT 3
db2 update db cfg for sample
```

- 9. 使用以下命令更新备用数据库 `POLONIUM` 的 HADR 数据库配置参数：

```
db2 update db for sample
```

- 10. 使用以下命令更新主数据库（我们的测试用例中为 `LEAD`）的 HADR 数据库配置参数：

```
db2 update db for sample
```

### 3.3 基本操作

本节介绍了启动、停止和切换（takeover）操作。

#### 3.3.1 启动和停止

本节涵盖启动和停止程序。

##### 启动

在启动 HADR 之前，我们建议先启动备用数据库。启动 HADR 时不会等待备用数据库。

##### 使用启动命令

启动的语法如下：
