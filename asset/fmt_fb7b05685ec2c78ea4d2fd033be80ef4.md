
> 图 7.14 健康指标设置。

# 266 DB2 数据库：Linux、UNIX 和 Windows 管理

`db2 get description for health indicator db.spilled_sorts`

`db.spilled_sorts` 的描述

如果有足够的堆空间来执行排序，且排序没有发生不溢出，则排序被认为是健康的。溢出到磁盘的排序会导致显著的性能下降。如果发生这种情况，可能会生成警报。该指标使用以下公式计算：`(db.sort_overflows / db.total_sorts)*100`。系统监控数据元素 `db.sorts` 是耗尽堆内存并可能需要磁盘空间临时存储的排序总数。数据元素 `db.total_sorts` 是已耗尽的排序总数。

`db2 update alert cfg for database on sample using db.spilled_sorts`

`60, warning 40 DB20000I UPDATE ALERT CONFIGURATION 命令成功完成。`

`db2 get alert cfg for database on sample using db.spilled_sorts`

## 警报配置

| 指标名称 | 数值 |
| :--- | :--- |
| `db.spilled_sorts` | - |
| 类型 | 基于阈值 |
| 警告 | 40 |
| 警报 | 60 |
| 敏感性 | 0 |
| 公式 | `(db.sort_overflows/db.total_sorts)*100;` |
| 操作 | 已禁用 |
| 阈值或状态检查 | 已启用 |

注意，`SAMPLE` 数据库有一个特定的设置，因此不再返回 `SQL2204` 消息。

## 健康中心—警报视图

让我们看看当健康监控器检测到突破阈值时（数值进入警报区域）会发生什么。我们将识别如何发现警报、警告或注意状态。在健康中心（图 7.15）中，当一个对象进入警报、警告或注意状态时，你将看到对象发生变化（例如，红色的停止符号表示警报状态）。右侧格的信息表明溢出正在导致警报。从命令行界面，你还可以获取健康快照，以确定哪些指标将监控对象置于非正常状态。

## 健康中心监控与问题确定 267

![](img/aa524d8157d0abd09e6f87c5b1aeab3b_284_0.png)

`db2 get health snapshot for database on sample`

图 7.15 健康中心—警报视图。

当触发警报时，会发生两种情况：

- 可以通过电子邮件或向传寻机地址发送警报通知，允许你联系负责系统的人员。
- 可以采取预配置的操作。例如，可以运行脚本或任务（从新的任务中心实现）。

使用健康监控器的下钻取功能，你可以访问有关当前警报的详细信息，并获取一个描述如何解决警报的建议操作列表。

`db2 get health snapshot for database on sample`

数据库健康快照 = 01-24-2003 19:55:09.78343

```
Database name = SAMPLE

Database path = C:\DB2\NODE0000\SQL00002\

Input database alias = SAMPLE

Operating system running at database server= NT

Location of the database = Local

Database highest severity alert state = Alarm
```
