
列处理完成后，如果 SQL 有参数需要绑定，你需要分配一个参数列表来存放 IN/OUT 参数。通过使用语句句柄并指定结果集中的列位置，可以获取每个列的元数据。在 SQL 类型已知后，它们需要映射到相应的 dbExpress 逻辑类型。某些 SQL 类型可能需要特殊处理。作为元数据的一部分，始终保留 SQL 类型、精度和标度。根据长度和数据类型，可以计算记录缓冲区的大小。大对象数据（`Blob data`）不应作为记录缓冲区的一部分，因为它们可能高达几个 GB。相反，在记录缓冲区中分配足够的空间来存放定位符。如果 RDBMS 使用块读取（blocks fetches），可以通过减少网络流量来提高性能。接下来，遍历列列表并通过调用供应商调用来绑定列及其空指示器（见图 16.2）。

# 数据访问层 (Data Access Layer)

第 16 章

## 16

| 4 字节 | 4 字节 | 4 字节 |
| --- | --- | --- |
| 列1 数据 | 列2 数据 | 列 <n> 数据 |
| uOffset1 | uOffset2 | uOffset<n><n> |

图 16.2 列数据和空指示器的偏移量。

`getRowsAffected()` 的实现应返回更新、插入、删除操作后受影响的行数，该信息在 SQL 成功执行后可用。

# 参数绑定 (Parameter Binding)

`SQLCommand` 方法 `setParameter()`、`getParameter()` 和 `close()` 处理了所有的运行时绑定。对于 SQL 中的每个标记，dbExpress 客户端使用 `setParameter()` 绑定 IN/OUT 参数，使用 `getParameter()` 获取输出数据。`set()` 将逻辑类型映射到 SQL 数据类型，复制参数数据并在内部存储为需要绑定到客户端的 SQL 格式。空指示器可以设置为绑定并返回 NULL。

此外，`setParameter()` 的参数允许指定输出参数缓冲区的需求；从而支持缓冲区需求大于输入参数的输出参数。例如，当 CHAR 和 VARCHAR 类型作为 IN/OUT 参数时，`uLength` 指定输入数据的大小，`uMaxPrecision` 可以设置为长度以指定输出数据的最大值。因此，对于输出或 IN/OUT 参数，应根据 `uMaxPrecision` 和 `uLength` 中的较大者分配缓冲区。对于非字符类型，`uMaxPrecision` 和 `uMaxScale` 应指定数值的精度和标度。

成功执行后，`getParameter()` 通过从参数缓冲区复制输出数据并执行任何物理到逻辑转换，返回输出或 IN/OUT 参数的输出。在获取所有输出参数并抓取所有结果游标后，`close()` 将释放所有参数缓冲区、记录缓冲区以及执行 SQL 语句的其他分配资源。

# 存储游标 (Stored Cursors)

对于可以返回多个游标的存储过程，`getCursor()` 将返回下一个可用的游标（如果有）。在到达当前游标末尾后，实现

# DataCLX

# 第四部分

`forNextCursor()` 应该通过调用供应商库来检查是否有额外的游标可用。如果有，则应该实例化一个新的 `SQLCursor` 对象，并遵循与 `execute()` 相同的步骤。只有少数几个 RDBMS（如 Oracle 或 DB2）支持返回多个游标。

请参阅列表 16.3 以获取 `SQLCommand` 实现示例。

# SQLCursor

`SQLCursor` 持有与执行的查询或存储过程有关的数据和元数据，并具有获取单个字段值的方法。`SQLCursor` 的实现使用与其关联的 `SQLCommand` 来访问元数据记录缓冲区。游标列的元数据在执行 SQL 后将即可可用。然而，要访问数据，应该调用 `next()`；它封装了 fetch 或扩展 fetch 供应商调用，将一条或多条记录检索到 dbExpress 记录缓冲区。

`SQLCursor` 数据访问方法如 `getString()` 和 `getBytes()` 会检查空偏移量中的列 NULL 指示器，如果它为空，则使用列数据偏移量并将 SQL 数据转换为 dbExpress 逻辑数据表示。

请参阅列表 16.4 以获取 `SQLCursor` 实现示例。

# SQLMetadata

`SQLMetadata` 接口定义了在打开的数据库连接上可以获得的各种数据库元数据。来自 `SQLConnection` 对象的 `getSQLMetadata()` 方法将返回 `SQLMetadata` 对象。`SQLMetadata` 仅提供 DataSnap、Kylix、Delphi 和 C++ Builder 组件所需的元数据。保留其他各种数据库元数据属性以使实现更简单。然而，大部分这些属性可以使用 `SQLMetadata` 对象上的 get 和 set 选项公开，而无需更改接口。

可以向 `SQLMetadata` 添加新方法，以返回有关表和列权限、可用 SQL 函数和 SQL 关键字、引用完整性约束等元数据。

## 总结

本章为您提供了 Kylix 中数据访问的体系概述，解释了为什么数据访问是这样实现的，以及如何创建您自己的 dbExpress 驱动程序。您应该检查 FreeCLX 网站 (`http://freeclx.sourceforge.net`) 和 Borland 社区网站 (`http://community.borland.com`)，获取在您阅读本书时可能已经发布的开源 dbExpress 驱动程序的信息。

# 创建一个现实世界的应用

由 John Kaster 编写

# 第 17 章

## 本章内容

- 应用描述 758
- 数据库定义 759
- 基础设计 769
- GUI 接口 774
- Web 接口 778
- 总结 789

# DataCLX

第四部分

在本章中，你将创建一个完整的数据库应用程序，包括设计数据库和操作数据的 GUI 应用程序。

# 应用背景

在开始编写这样的章节之前，你必须想出一个“现实世界”的应用作为示例。我们讨论过为书中提供的所有示例编写一个连接到具有可搜索 GUI 界面的应用程序，但我们没有时间按照我们想要的方式创建该应用程序。

幸运的是，我在 David Intersimore 处的全职工作（非正式称为“Borland Relations 关系的特殊项目总监”）提供了一个解决方案。对于在加利福尼亚州长滩举行的 2001 年 Borland 大会 (`BorCon 2001`)，我们汇集了一个展示应用，演示了 Borland 所有开发工作的协同工作。由于我们想出一个相当有趣且吸引人的内容，我们创建了虚拟公司 Mobi-E-Tailer，应用规范也随之诞生。

多个人参与了该展示应用的制作，来自 Borland 的各个产品组，按无特定顺序列在此：

- Mike Rozlog，架构师和技术传播者，负责应用服务器 Enterprise Java Beans (`EJBs`)
- Sung Nguyen，销售工程师，负责 C++ CORBA 货币转换器
- Blake Stone，JBuilder 架构师，负责 Java Server 页面、购物车和手机客户端
- Sriram Balsubramanian，InterBase 研发部门，负责数据库设计和实现
- John Ray Thomas，Kylix 和 C++ Builder 产品经理，负责 Kylix 应用
- Thomas Eberald，Delphi 产品经理，负责 Web 服务通知器
- David Intersimore，开发者关系副总裁，负责定义需求（客户端）
- Pat Kerpan，DSP 组副总裁，负责在协作开发中使用 TeamSource DSP
- John Kaster，开发者关系高级经理，项目协调员和全职“催促者”

# 应用描述

Mobi-E-Tailer 销售电影和电影纪念品。Kylie（实际上是 CLX）满足的两个需求是：一个提供快速向数据库输入信息的 GUI 应用程序，以及一个提供应用程序中数据信息的 Web 数据库导航系统。当时还发生了一些其他事情（例如使用 Delphi 6 集成 Web 服务），我实际上通过 CLX GUI 应用程序和 Windows 上使用 Delphi 6 的基础 Web 服务器应用程序进行了开发。然后，John Ray Thomas (`JT`) 将这些应用程序迁移到 Kylik 并增强了 Web 服务器部分，开始与 JBuilder 构建的 Java Server 页面 (`JSP`) 通信。

由于他在 Web 服务器方面的工作转向支持另一个项目，我们将使用我最初交付给他的那个版本，以及我之后做的一些增强。

我们在本章中讨论的这个“现实世界”应用的部分如下：

- 用于数据库管理的 CLX GUI 应用程序
- 用于导航的 NetCLX Web 服务器

# 数据库定义

在对 GUI 接口进行一些微调后，我们得到了以下表定义：

这是客户表（`CUSTOMERS`）：

```sql
CREATE TABLE CUSTOMERS (
  CUSTOMER_KEY INTEGER PRIMARY KEY,
  NAME VARCHAR(25),
```
