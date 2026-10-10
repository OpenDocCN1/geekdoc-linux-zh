

5. 哪种“策略结果集”模式可用于获取组策略建模信息？
a. 记录模式
b. 规划模式
c. 事件查看器模式
d. 设计模式

6. 哪个数据库包含 Windows 管理仪器（WMI）使用的信息？
a. 策略结果集 (RsOP)
b. SYSVOL
c. 公共信息管理对象模型 (CIMOM)
d. 组策略容器 (GPC)

7. 哪个基于图形用户界面（GUI）的查询引擎可以查看林中的已配置 GPO 并报告其结果？
a. 策略结果集 (RSOP)
b. Gpresult
c. Gpupdate
d. 组策略管理编辑器

8. 编写 WMI 查询使用什么语言？
a. SQL
b. T-SQL
c. VBScript
d. WQL

9. 组策略管理控制台中的哪个节点提供应用于特定用户/计算机组合的有效策略设置？
a. 组策略建模
b. 组策略结果
c. 组策略管理编辑器
d. 组策略对象编辑器

10. 你有一个用于安装特定软件应用程序的组策略对象。由于此应用程序资源密集，你希望仅在拥有至少 1GB RAM 的计算机上安装该软件。你可以使用什么功能来限制此 GPO 仅应用于符合此标准的计算机？
a. 安全组筛选
b. WQL 筛选
c. WMI 筛选
d. CIMOM 筛选

## 案例场景

## 场景 10-1：为 Tailspin Toys 规划 GPO

Tailspin Toys 正在运行一个包含单个 Windows Server 2008 Active Directory 域的环境，为 12 个地点中的每一个配置了多个 OU。每个地点的管理员负责管理 GPO 和用户帐户。你是负责规划基础设施的企业管理员。针对以下每个挑战，记录你的选项并准备好与其他学生分享。

- 位于每个地点的管理员应能够创建新的 GPO 并编辑他们创建的 GPO。他们不应能够更改或删除他们未创建的 GPO。提供此功能的选项有哪些？
- 目前每个地点的所有用户都在一个 OU 中。某些组策略仅应适用于某些部门的用户，而不适用于其他部门。你应该考虑哪些选项，以便将组策略仅应用于必要的用户？
- 尽管你创建了一个域范围的策略，强制执行对管理工具的限制，但你不想让这些设置适用于你已在其 OU 上委托管理权限的每个地点的用户。解决此问题的选项有哪些？

![](img/a8ee53dbf1310726255b6fbb9f296fb2_262_0.png)

## Active Directory 维护、故障排除和灾难恢复

### 目标领域矩阵

| 技术技能 | 目标领域 | 目标领域编号 |
| :--- | :--- | :--- |
| 维护 Active Directory | 执行离线维护。 | 5.2 |
| 备份 Active Directory | 配置备份和恢复。 | 5.1 |
| 使用可靠性和性能监视器 | 监视 Active Directory。 | 5.3 |

### 关键词

- ADSIEdit
- 权威还原
- 反向链接
- bcdedit
- 启动配置数据 (BCD)
- 启动卷
- bootmgr.exe
- 检查点文件
- 复制备份
- 关键卷
- 碎片整理
- 目录服务还原模式
- dsacis
- edb.log
- 可扩展存储引擎 (ESE)
- 碎片
- 垃圾回收
- LDP
- 手动备份
- ntltest
- 非权威还原
- 离线碎片整理
- 在线碎片整理
- 性能计数器
- 性能对象
- 可靠性和性能监视器
- Repadmin
- 可重启的 Active Directory 域服务
- 计划备份
- 系统卷
- 墓碑
- 事务缓冲区
- VSS 完整备份
- wbadmin
- Windows PowerShell
- Windows Server 备份

Lucerne Publishing 是一家全球出版公司，在北美、欧洲和印度设有办事处。在过去几周里，Lucerne Publishing 的 IT 人员设计和实现了一个包含多个站点、OU 和 GPO 的 Windows Server 2008 Active Directory 网络。为了维护 Active Directory 网络，Lucerne Publishing 需要制定一个针对 Active Directory 的备份和恢复计划，以防止单个域控制器、对象或容器的丢失。此外，Lucerne Publishing 的 IT 人员需要实施一个持续的监控方案，以确保新的 Active Directory 环境对所有用户、工作站和成员服务器保持可用。

完成本课后，您将能够监控、故障排除、备份和还原 Windows Server 2008 中的 Active Directory 域服务。您将能够讨论新的 Windows Server 备份技术，该技术用于执行 Active Directory 数据库的备份和还原。您将能够监控 Active Directory，包括监控 Windows 事件查看器以及使用新的 Windows Server 2008 可靠性和性能监视器工具。最后，您将使用几种工具和技术来故障排除 AD DS 服务，以及确定错误原因并解决错误的诊断工具。

## 维护 Active Directory

> 成功部署 Microsoft Windows Server 2008 环境后，重要的是制定维护程序以保持其平稳运行。稳固的监控和维护计划可以预防潜在问题。

![](img/a8ee53dbf1310726255b6fbb9f296fb2_263_0.png)

当维护和监控程序就位以识别潜在问题并主动管理环境时，就不再需要在问题发生后进行故障排除了。本课题介绍了监控和维护 Active Directory 的指南。它还描述了用于监控、维护和故障排除 Active Directory 的工具。最后，它提供了备份、还原和碎片整理 Active Directory 数据库的适当方法。

Active Directory 是基于 *Extensible Storage Engine (ESE)* 格式的数据库。ESE 负责管理 Active Directory 数据库的更改。更改被称为 *事务*。事务可以包含多个更改，例如添加新对象和修改现有对象的属性。当提出创建或修改数据库对象的请求时，ESE 通过以下过程执行这些请求：

1.  Active Directory 将事务写入位于服务器内存中的 *事务缓冲区*。该事务缓冲区将数据存储在服务器 RAM 中，直到实际写入服务器的硬盘，以便可以将事务中的所有数据一次性写入磁盘。
2.  Active Directory 将事务写入事务日志文件。默认日志文件的名称为 *edb.log*。日志文件允许事务存储，直到它可以写入实际数据库。事务日志文件的默认大小为 10 MB。当默认的 edb.log 文件已满时，它会被重命名以包含一个顺序编号作为后缀，例如 edb1.log。当 edb.log 文件达到 10 MB 容量时，它会被重命名为 edbx.log，其中 x 被替换为下一个顺序编号。
3.  Active Directory 将事务从事务缓冲区写入 ntds.dit 数据库。
4.  Active Directory 将数据库与第 2 步中 edbx.log 文件的更改进行比较，以确保写入的事务与日志文件中的事务匹配。
5.  Active Directory 更新 edb.chk *检查点文件*。检查点文件用作写入磁盘的数据库信息的参考。在 Active Directory 需要从故障中恢复的情况下，检查点文件用作起点。它包含日志文件中必须从中开始恢复的点的引用。

![](img/a8ee53dbf1310726255b6fbb9f296fb2_263_1.png)

