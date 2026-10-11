
- 1. 如下检查所有资源状态是否正常：

`(S) getstatus`

如果你设置了 HA IP 地址，应该看到类似下面的代码输出。如果你没有设置 HA IP 地址，则后续输出将不包含 IP 资源：

| 组名称 | 资源 |
| :--- | :--- |
| db2_db2inst_0-rg | db2_db2inst_0-rs |
| db2_db2inst_0-rg | db2_db2inst_0-rs_ip |
| | |
| db2_db2inst_0-rg | db2_db2insts_0-rs |
| db2_db2insts_0-rg | db2_db2insts_0-rs_ip |

-- 资源 -- 

| 资源名称 | 节点名称 | 状态 |
| :--- | :--- | :--- |
| db2_db2instp_0-rs | hadr01 | Online |
| db2_db2instp_0-rs_ip | hadr01 | Online |
| db2_db2insts_0-rs | hadr02 | Online |
| db2_db2insts_0-rs_ip | hadr02 | Online |
| db2_hadr_haddrb-rs | hadr01 | Online |
| db2_hadr_haddrb-rs | hadr02 | Offline |

- 2. 以 root 身份，通过重启 Linux 模拟主节点 (`hadr01`) 故障：
`(P) # init 6`
- 3. 以 root 身份，重复执行以下命令检查恢复状态：
`(S) # getstatus`

五分钟或更多后，如果你设置了 HA IP 地址，应该看到类似下面的代码输出。如果你没有设置地址，则在后续输出中将看不到 IP 资源：

| 资源组和资源 |
| 组名称 | 资源 |
| :--- | :--- |
| db2_db2instp_0-rg | db2_db2instp_0-rs |
| db2_db2instp_0-rg | db2_db2instp_0-rs_ip |
| db2_db2insts_0-rg | db2_db2insts_0-rs |
| db2_db2insts_0-rg | db2_db2insts_0-rs_ip |

| 资源名称 | 节点名称 | 状态 |
| :--- | :--- | :--- |
| db2_db2instp_0-rs | hadr01 | Online |
| db2_db2instp_0-rs_ip | hadr01 | Online |
| db2_db2insts_0-rs | hadr02 | Online |
| db2_db2insts_0-rs_ip | hadr02 | Online |
| db2_hadr_haddrb-rs | hadr01 | Unknown |
| db2_hadr_haddrb-rs | hadr02 | Unknown |

使用 DB2 `SNAPSHOT` 命令验证 HADR 数据库现在在节点 `hadr2` 上已为主数据库：

```
% snapshot for db on hadrb
```

- 4. 一旦主机器 (`hadr01`) 恢复上线，就可以重新建立 HADR 对。作为原始主实例 `db2inst`，运行以下命令：

```
(P) % db start hadr on hadrdb as standby
```

- 5. HADR 对现在应该重新建立了。你可以根据需要执行 `getstatus` 进行检查。要将主数据库移回 `hadr01`，执行以下（“令牌”）：

```
(P) # rg -o move -n hadr02 db2hadrdb-rg
```

- 6. 检查 HADR 是否返回原始状态：

```
(P) # getstatus
```

输出类似以下几行：

| 资源组和资源 |
| 组名称 | 资源 |
| :--- | :--- |
| db2_db2instp_0-rg | db2_db2instp_0-rs |
| db2_db2instp_0-rg | db2_db2instp_0-rs_ip |
| db2_db2insts_0-rg | db2_db2insts_0-rs |
| db2_db2insts_0-rg | db2_db2insts_0-rs_ip |

| 资源名称 | 节点名称 状态 |
| :--- | :--- |
| db2_db2instp_0-rs | hadr01 | Online |
| db2_db2instp_0_rs_ip | hadr01 | Online |
| db2_db2insts_0-rs | hadr02 | Online |
| db2_db2insts_0_rs_ip | hadr02 | Online |
| db2_hadr_haddrb-rs | hadr01 | Online |
| db2_hadr_haddrb-rs | hadr02 | Offline

# Q 复制

在本章中，我们提供了 Q 复制的介绍及其简单概述。我们还提供了设置单向复制的步骤。

### 11.1 简介

Q 复制是一种使用 WebSphere MQ 队列在源和目标之间传输事务的解决方案。

Q 复制分为：

- 单向：在单向复制中，更改从源被捕获。单向复制可以从一个源到多个目标。单向复制的目标通常是只读。
- 双向：在双向复制中，两个服务器上的表相互复制。任何一侧表的更改都会复制到相应的表。你无法复制行集，且每个表必须具有相同数量的列以及这些列的数据类型。
- 点对点：在点对点 Q 复制中，表在两个或多个服务器之间进行复制。与双向 Q 复制一样，所有表必须结构相同，但每个表可以有自己的架构。

有关不同 Q 复制配置的更多信息，请参考 DB2 信息中心：

`http://publib.boulder.ibm.com/infocenter/db21uw/v9/index.jsp`

我们描述了 Q 复制的基本结构：

字体 运行在源端的 Q Capture 程序读取 DB2 恢复日志，以获取指定的源表的更改。然后它将消息放在发送队列中。Q Capture 程序使用一组称为 Q Capture 控制的 表。控制表存储有关复制源、相应目标、使用的 MQ 队列和其他数据。
- Q 订阅定义了要复制的源表和目标表。Q 订阅需要复制队列映射来识别用于发送和接收事务的 WebSphere MQ 队列。
- Q Apply 程序运行在目标端，接收消息并应用于目标表。Q Apply 程序也有一组 DB2 表。

在本章的剩余部分中，我们关注单向 Q 复制设置。

### 11.2 单向设置

本节提供了两个远程服务器之间单向复制设置的逐步示例。见图 11-1。

![](img/a97b7826c3cf736045d80f48b5520a20_334_0.png)

图 11-1 单向设置图

设置单向 Q 复制必须完成以下任务：

- 1. 在源端和目标数据库服务器上设置数据库。
- 2. 在源端服务器和目标服务器上设置 WebSphere MQ 对象。
- 3. 在源端和目标端启动监听器和通道。
- 4. 可选：测试队列。
- 5. 创建 Q Capture 控制表。
- 6. 创建 Q Apply 控制表。
- 7. 创建 Q 订阅。
- 8. 配置从目标端到源端服务器的连接性。
- 9. 启动 Q Capture。
- 10. 启动 Q Apply。

在我们的示例中，我们使用了两个运行 DB2 版本 9.1 和 WebSphere MQ 6.0 的 Windows 服务器。使用远程服务器设置单向复制的逐步过程如下：

- 1. 在源端和目标服务器上进行初始数据库设置：
a. 源数据库（在我们测试用例中的 `SAMPLE`）必须将数据库配置参数 `LOGRETAIN` 设置为 `RECOVERY`。

```
db2 update database configuration for sample using LOGRETAIN RECOVERY
```

如果是第一次将 `LOGRETAIN` 设置为 `recovery`，则需要备份。
b. 识别你的目标数据库。在我们的示例中，目标数据库是 `TGTDB`。

- 2. 在源端服务器上设置 WebSphere MQ 对象：
a. 从命令行窗口创建队列管理器 `QMGR1`：

```
strmqm QMGR1
```

b. 启动你刚刚创建的队列管理器：

```
strmqm QMGR1
```

c. 要创建所需的 MQ 对象，请使用示例 11-1 所示的脚本运行以下命令。记得将 IP 和端口号替换为所需的 IP 和端口号：

```
runmqsc QMGR1 < QMGR1.DEF
```
