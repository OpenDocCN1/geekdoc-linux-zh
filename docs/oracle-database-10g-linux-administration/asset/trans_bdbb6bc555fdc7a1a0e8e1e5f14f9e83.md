

- **Oracle 应用服务器 InterConnect** 用于集成企业应用。InterConnect 使用高层集成逻辑和底层平台服务。集成功件由 RDBMS 高级队列组件和 Oracle 工作流组成。此外，还有用于应用程序和协议的各种适配器，以实现应用程序集成。
- **Oracle 应用服务器 Process Connect** 这是一种 Oracle 元数据业务集成工具，用于转换、翻译和验证业务交互。

## 使用 Oracle 应用服务器 10g

使用 OracleAS 10g 完整的企业版（Enterprise Edition）可为组织提供部署、保护集成各类应用程序的手段。利用 OracleAS 10g 实现其指定用途最高效的方式是使用 DCM（分布式配置管理）的命令行实用工具。企业经理（Enterprise Manager）网格控制也用于操作 OracleAS 10g 实例。这些应用程序的详细分解超出了本章的范围，但在有关 OracleAS 10g 配置的部分中有所演示。图 18-1 提供了企业经理应用服务器控制（Enterprise Manager Application Server Control）的一个示例。

当配置多个 OracleAS 10g 实例以实现高可用性或集群时，使用 DCM 可以简化相关管理。实际上，DCM 允许你：
- 保持各个实例同步。
- 备份和恢复实例配置。
- 在实例之间导入和导出配置。
- 启动和关闭实例或子组件。
- 验证实例状态。

DCM 管理的组件包括以下内容：
- OC4J（Oracle Java 组件）（J2EE）
- Oracle HTTP 服务器
- OC4J 应用程序
- OPMN（Oracle 进程管理和通知服务器）
- JAZN（Oracle 应用服务器 Java 身份验证服务）

![](img/9479df2d00f5e62b87366b125224950f_461_0.png)

### 图 18-1. 企业经理应用服务器控制

下表提供了按命令类型分组及其用途的 DCM 命令行命令的详尽列表：

| DCMCTL Shell 命令 | 用法 |
|---|---|
| !! | 重复执行上一条命令 |
| shell | 调用 dcmctl shell |
| echo | 将字符串输出 |
| setLogLevel | 设置日志记录级别 |
| exit | 退出 shell |
| quit | 退出 shell |

## DCMCTL 归档命令

| 命令 | 用法 |
|---|---|
| applyArchiveTo | 将配置归档应用到实例或集群 |
| createArchive | 创建集群/实例归档 |
| exportArchive | 将归档从/向存储库导出到 JAR 文件 |
| importArchive | 将归档导入存储库 |
| listArchives | 列出归档 |
| removeArchive | 删除归档 |

## DCMCTL 应用程序命令

| 命令 | 用法 |
|---|---|
| deployApplication | 部署 J2EE 应用程序 |
| listApplications | 列出 OC4J 实例应用程序 |
| redeployApplication | 重新部署 J2EE 应用程序 |
| undeployApplication | 取消部署 J2EE 应用程序 |
| validateEarFile | 验证 EAR J2EE 合规性 |

## DCMCTL 属性命令

| 命令 | 用法 |
|---|---|
| getError | 显示错误 |
| getReturnStatus | 返回最后一条命令的状态 |
| getState | 返回请求组件的状态：OC4J、Oracle HTTP 服务器、JAZN |
| help | 列出 dcmctl 命令 |
| listComponentTypes | 列出支持的组件类型 |
| set | 设置 dcmctl 选项 |

## 非托管集群命令

| 命令 | 用法 |
|---|---|
| addOPMNLink | 创建非托管的 OracleAS 10g 集群 |
| getOPMNPort | 显示 ONS 远程端口和主机名 |
| listOPMNLinks | 列出包含本地实例的非托管 AS 集群 |
| removeOPMNLink | 从非托管集群中移除实例 |

## DCMCTL 进程管理命令

| 命令 | 用法 |
|---|---|
| restart | 重启应用程序堆栈 |
| shutdown | 停止应用程序堆栈 |
| start | 启动应用程序堆栈 |
| stop | 停止应用程序堆栈 |

图 18-2 展示了一个简单的 DCMCTL 属性命令示例。图中所示的命令是一个通用的高层状态命令，用于列出所有实例组件的状态。要执行 DCMCTL 命令，必须导航到 `$ORACLE_HOME/dcm/bin/dcmctl`。

为了简化操作，可以将 `dcmctl` 实用工具放入你的 `PATH` 环境变量中。在 Linux 中，默认 shell 是 BASH shell，而在用户（通常是 `oracle`）的主目录中有一个名为 `.bash_profile` 的文件。在这里可以放置 `dcmctl` 命令的路径，以便将其引入用户环境并在文件系统的任何位置运行。这样就无需每次执行 `dcmctl` 命令时都导航到 `$ORACLE_HOME/dcm/bin` 目录。正如所注，管理 OracleAS 10g 服务器或服务器集群所需的大多数操作都可以通过 DCMCTL 实用工具完成。

用于管理日志的一个非常有用的附加工具是由企业经理应用服务器控制提供的。这个名为 LogLoader 的工具提供了分析来自不同区域的多个日志并根据某些标准对它们进行分组的手段。LogLoader 提供了一个优秀的取证工具，用于根据时间/日期标准诊断日志。通过合并各种系统日志以匹配检测到的系统减速或错误，可以缩短搜索时间。日志根据搜索范围以逻辑集合形式分组。例如，当从 LogLoader 中选择 HTTP_Server 组件时

```
$ dcmctl getstate -c -v

Current State for Instance:testinst

Component Type Up Status In Sync Status
============================================

1 home oc4j Up True

2 HTTP Server ohs Up True

3 OC4J_Demos oc4j Up True
```

### 图 18-2. DCMCTL 命令及输出

应用程序，会搜索 `error_log` 和 `access_log`。如果将数据库组件包含在 HTTP 搜索条件中，则还会搜索 `alertsid.log`。请求的日志随后返回到浏览器并整合以便轻松审查，如图 18-3 所示。

需要定期加载以进行审查的关键监控日志包括：
- **Oracle 数据库警报日志** 如果数据库出现问题，这将有助于获取信息。它也可以用于检查任何数据库系统变更。
- **Apache access_log** 列出传入请求的地址。
- **Apache error_log** 列出与 HTTP 服务器和加载模块相关的任何错误。
- **DCM 日志** 列出与内部托管进程相关的错误。

![](img/9479df2d00f5e62b87366b125224950f_464_0.png)

### 图 18-3. 通过企业经理查看各种日志

用于监控性能并收集指标的另一个附加工具是动态监控服务（Dynamic Monitoring Service）。此服务的目的是提供一种基于在 Java 应用代码中安装 DMS 调用来仪表化 J2EE 应用的手段。Oracle 应用服务器 10g 具有用于仪表化以下对象的 DMS 服务：
- Oracle HTTP 服务器
- Java 虚拟机
- JDBC
- OC4J
- mod_plsql
- Portal
- Jserv
- Oracle 进程管理和通知服务器指标
- Oracle 应用服务器 Discoverer 指标

表 18-1 展示了 DMS 可以为 HTTP 服务器收集的指标类型示例。

| 指标名称 | 描述 | 测量单位 |
|---|---|---|
| connection.active | 当前打开的连接数 | threads |
| connection.avg | 处理 HTTP 连接所花费的平均时间 | usecs（微秒） |
| connection.maxTime | 处理任何 HTTP 连接所花费的最长时间 | usecs |
| connection.minTime | 处理任何 HTTP 连接所花费的最短时间 | usecs |
| connection.time | 处理 HTTP 连接所花费的总时间 | usecs |
| handle.active | 当前处于 handle 处理阶段的子服务器数量 | threads |
| handle.avg | 在模块处理程序中花费的平均时间 | usecs |
| handle.completed | handle 处理阶段完成的次数 | ops |
| handle.maxTime | 在模块处理程序中花费的最长时间 | usecs |
| handle.minTime | 在模块处理程序中花费的最短时间 | usecs |
| handle.time | 在模块处理程序中花费的总时间 | usecs |
| request.active | 当前处于 request 处理阶段的子服务器数量 | threads |
| request.avg | 处理 HTTP 请求所需的平均时间 | usecs |
| request.completed | 完成的 HTTP 请求数量 | ops |
| request.maxTime | 处理 HTTP 请求所需的最长时间 | usecs |
| request.minTime | 处理 HTTP 请求所需的最短时间 | usecs |
| request.time | 处理 HTTP 请求所需的总时间 | usecs |

