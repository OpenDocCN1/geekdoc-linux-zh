
## 配置参数

| `catalog_noauth` | YES, NO <br>默认值: YES | 指定系统管理员 (SYSADM) 权限是否允许目录和取消目录节点、数据库或 DCS 和 ODBC 引用。 |

| `clnt_krb_plugin` | 任何有效字符字符串 <br>默认值: NULL 或 "IBMkrb5" | 指定用于客户端侧 Kerberos 认证和本地授权的库中默认 Kerberos 插件的名称。当客户端使用 KERBEROS 认证时，使用此插件库。 |

## 配置实例和数据库

### 表 2.3 DB2 数据库管理器实例配置参数（续）

| 参数 | 范围/默认值 | 描述 |
|---|---|---|

| `clnt_pw_plugin` | 任何有效字符字符串 默认值: NULL | 指定用于客户端侧认证和本地授权的用户 ID-密码插件库名称。当客户端使用 CLIENT、SERVER 或 SERVER_ENCRYPTION 认证时，使用此插件库。 |

| `comm_bandwidth` | 0.1–100,000 兆字节/秒 默认值: -1 | 指定通信带宽计算值（每秒兆字节），DB2 优化器使用该值估算分区数据库系统的数据库分区服务器之间执行某些 SQL 操作的成本。 |

| `conn_elapse` | 0–100 秒 默认值: 10 | 指定两个节点之间建立 TCP/IP 连接的秒数。（如果未在此参数指定的时间内建立连接，将进行其他尝试，次数直到 `max_retries` 参数指定的次数。如果所有尝试均失败，则返回错误。） |

| `cpuspeed` | -1, 10⁻⁻¹ 默认值: -1 | 指定安装 DB2 的工作站上使用的 CPU 速度，以每指令毫秒数。 |

| `dft_account_str` | 任何有效字符字符串 默认值: NULL | 指定在连接到 DRDA 服务器时使用的默认费用会计字符串。 |

| `dft_mon_buffool` | ON, 默认值: OFF | 指定快照监控缓冲区池开关的默认值。 |

| `dft_mon_lock` | ON, 默认值: OFF | 指定快照监控锁开关的默认值。 |

| `dft_mon_sort` | ON, 默认值: OFF | 指定快照监控排序开关的默认值。 |

| `dft_mon_stmt` | ON, 默认值: OFF | 指定快照监控语句开关的默认值。 |

| `dft_mon_table` | ON, 默认值: OFF | 指定快照监控表开关的默认值。 |

| `dft_mon_timestamp` | ON, 默认值: ON | 指定快照监控时间戳开关的默认值。 |

| `dft_mon_uow` | ON, 默认值: OFF | 指定快照监控工作单元 (UOW) 开关的默认值。 |

| `dftdbpath` | 任何有效字符字符串 默认值: C  (Windows) 或实例用户主目录 (UNIX) | 指定用于存储新数据库的驱动器（Windows）或目录路径（UNIX）。如果在创建数据库时未指定路径，将在此参数标识的位置创建数据库。） |

### 表 2.3 DB2 数据库管理器实例配置参数（续）

| 参数 | 范围/默认值 | 描述 |
| --- | --- | --- |

| `diaglevel` | 0–4 默认值: 3 | 指定诊断设施捕取的诊断信息级别。 |

| `diagpath` | 任何有效字符字符串 默认值: NULL | 指定存储诊断数据的路径。 |

| `dir_cache` | YES, NO 默认值: YES | 指定是否缓存目录信息。（当此参数设置为 YES 时，减少 I/O。） |

| `discover` | DISABLE, KNOWN, SEARCH 默认值: SEARCH | 指定使用的发现机制。（如果此参数设置为 SEARCH，DB2 将搜索网络；如果设置为 KNOWN，则使用指定的位置。） |

| `discover_inst` | ENABLE, DISABLE 默认值: ENABLE | 指定是否启用实例发现。 |

| `fcm_num_buffers` | AUTOMATIC, 128–300 (32位), 128–288 (64位) 默认值: AUTOMATIC | 用于内部通信的 4KB 缓冲区数量。当设置为 AUTOMATIC 时，FCM 监控使用并分配资源。 |

| `fcm_num_channels` | AUTOMATIC, 120,000 (32位), 524,288 (64位) 默认值: AUTOMATIC | 用于内部通信的通道数量。当设置为 AUTOMATIC 时，FCM 监控使用并动态分配资源。 |

### 表 2.3 DB2 数据库管理器实例配置参数（续）

| 参数 | 范围/默认值 | 描述 |
|---|---|---|

| `fed_noauth` | YES, NO 默认值: NO | 指定是否跳过认证。（当 `fed_noauth` 设置为 YES 时，认证设置为 SERVER 或 SERVER_ENCRYPT，且 `federated` 设置为 YES，则跳过实例认证。） |

| `federated` | YES, NO 默认值: NO | 指定是否启用联邦数据库对象支持。 |

| `fenced_pool` | -1,0,maxagents 默认值: maxagents | 指定位于数据库服务器上的最大隔离进程数。（一旦达到此限制，将无法调用新的隔离请求。） |

| `group_plugin` | 任何有效字符字符串 默认值: NULL | 指定用于所有组查找的插件库名称。 |

| `health_mon` | ON, OFF 默认值: ON | 指定是否监控在健康中心配置的实例和数据库对象的健康状况。（开启时，DB2 健康监控收集这些对象的信息并在对象不健康时采取行动。） |

| `indexrec` | RESTART, RESTART_NO_REDO ACCESS, ACCESS_NO_REDO RESTART | 指定 DB2 数据库管理器何时尝试重建索引，任何索引构建将在备用数据库的回滚或 HDR 日志重放期间重做。此参数仅在配置参数 `indexrec` 设置为 SYSTEM 时有效。 |

| `instance_memory` | AUTOMATIC, 8–294,967,295 4K 页 默认值: AUTOMATIC | 指定应为实例管理保留的内存，包括描述实例控制下的数据库的内存区域。此参数分配的内存确定了同时激活的数据库最大数量以及任何给定时间激活的代理最大数量。 |

# 60 第 2 章：服务器管理

### 表 2.3 DB2 数据库管理器实例配置参数（续）

| 参数 | 取值范围/默认值 | 说明 |
| :--- | :--- | :--- |

| `intra_parallel` | SYSTEM, YES, NO 默认值: NO | 指定 DB2 数据库管理器实例是否可以使用分内并行性。 |

| `java_heap_sz` | 0-524,288 4K Pages 默认值: 2,048 | 指定 Java 解释器用于服务 Java DB 存储过程和用户定义函数的最大内存（以页计数）。 |

| `jdk_path` | 任何有效字符字符串 默认值: NULL | 指定运行 Java 存储过程和用户定义函数所需的 Java™ 软件工具包 (SDK) 安装目录。Java 解释器使用的 CLPATH 和其他环境变量是使用此参数的值计算的。 |

| `keepfenced` | YES, NO 默认值: YES | 指定在围栏调用（fenced call）完成后是否保留围栏进程。（如果将此参数设置为 NO，则每个围栏调用都会创建一个并销毁一个新的围栏进程；如果设置为 YES，则后续围栏调用将重用围栏进程。） |

| `local_gssplugin` | 任何有效字符字符串 默认值: NULL | 当身份数据库管理器配置参数设置为 GSSPLUGIN 或 GSS_SERVER_ENCRYPT 时，指定用于实例级本地授权的默认 GSS API 插件库名称。 |

| `max_connections` | -1, 1-64,000 默认值: -1 (max_coagents) | 指定连接到实例的最大应用程序数量。 |

| `max_connretries` | 0-100 默认值: 5 | 指定对数据库分区服务器可以进行的连接重试次数。如果超过了此参数指定的值，将返回错误。 |

| `max_coordagents` | -1, 0-maxagents 默认值: -1 (maxagents-num_initagents) | 指定一个节点上同时存在的协调代理（coordinating agents）的最大数量。此参数用于限制协调代理的数量或控制数据库中的负载。 |

| `max_querydegree` | ANY, 1-32,767 默认值: ANY | 指定在此 DB2 数据库管理器实例上执行的任何 SQL 语句所使用的分内并行性最大程度。 |

### 表 2.3 DB2 数据库管理器实例配置参数（续）

| 参数 | 取值范围/默认值 | 说明 |
| --- | --- | --- |
