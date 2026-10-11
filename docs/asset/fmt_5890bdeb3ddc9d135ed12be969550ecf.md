
dbconnections 文件包含所有已安装的 dbExpress 驱动程序的信息。`LibraryName` 和 `VendorLib` 属性指定了特定特定库的名称，通过这些库向数据库发送请求和响应。除了这些属性，`dbxdrivers` 文件的每个部分包含数据库连接的默认参数值。每个新连接都使用此驱动程序创建，这些值被插入为连接默认。

# 第 11 章：调试与调试器

## 停靠 (Docking)

Kylix 的一个优秀特性是所有的调试窗口都可以停靠以节省屏幕空间。图 11-11 显示了停靠调试窗口的一种。

![](img/d784fa8294cae585d61ec86b987ea212_268_0.png)

图 11-11：停靠的调试窗口

## 调试共享对象库和包

Kylix 让共享对象库和包的调试变得简单。首先，检查 `Tools` | `Environment Options` 中的环境变量，以确保当前目录（当前目录的缩写为点 `.`）已设置在 `LD_LIBRARY_PATH` 中。然后，打开包含共享对象或包的项目。选择 `Run` | `Parameters` 来使用该共享对象或包。选择使用该共享对象或包的适当应用程序（可执行文件）。根据相应的菜单设置适当断点。现在，当应用程序使用共享对象或包时，任何断点都会停止执行。

## 总结

调试始于正确的心态。一旦具备，它将贯于开发的各个方面，从设计到测试。编写代码时，记住要防御性编程。不断问自己“如果……会发生什么”，并采取措施防止或检测这些情况。

当那些讨厌的虫虫溜过这些第一道防线时，Kylix 会介入并提供必要的工具来追踪它们并帮助消灭它们。花时间学习如何使用这些强大的工具，这样当它们出现时，任何 bug 都能被快速消除。

# 第 3 节

## 数据访问

- 第 12 章—dbExpress 和 DataCLX
- 第 13 章—客户端侧数据管理
- 第 14 章—使用字段对象

## Kylix 2 开发

## dbExpress 和 DataCLX

## 引言

Delphi 最大的卖点之一是其访问、显示和导航数据的能力。Kylix 通过其 DataCLX 组件和名为 dbExpress 的底层架构延续了这一传统，提供了高效且强大的数据访问。本章探讨了 Kylix 的数据访问架构，并演示了 dbExpress 和 DataCLX 组件的力量。

dbExpress 和 DataCLX 共同代表了 Kylix 和 Delphi 6 的数据访问和显示层。一个常见的误解是 SQLComponents（`SQLConnection`、`SQLDataSet` 等）是 dbExpress 的一部分，因为它们存在于组件调板的 dbExpress 选项卡上。事实并非如此。组件调板上的所有组件都是 DataCLX 的一部分，dbExpress 指的是底层驱动程序和数据访问架构，它提供了数据源与 DataCLX 之间的通信层。

![](img/d784fa8294cae585d61ec86b987ea212_273_0.png)

图 12-1：DataCLX 架构（经 Borland Software Corporation 授权）

# 第 12 章：dbExpress 和 DataCLX

## dbExpress

dbExpress 代表了 DataCLX 组件用于原生访问各种数据库服务器的底层数据访问架构。它是一组构建在 dbExpress 驱动程序之上的低级接口。数据库供应商实现 dbExpress 接口，以提供应用程序访问数据所需的原始数据。根据 Borland 的文档，“dbExpress 是一种跨平台、与数据库无关且可扩展的接口，用于处理动态 SQL。”

**注意：** 这些都是 BDE 的宿敌，并且在不同程度上损害了（使用 BDE 的）Delphi 在生产环境中的价值和效率。BDE 最大的限制是它是仅限 Windows 的解决方案。dbExpress 的设计使得用于构建 dbExpress 驱动程序的代码（通常是 C 代码）具有平台无关性。因此，相同的代码可以在 Windows 和 Kylix 上编译 dbExpress 驱动程序，并且理论上可以编译到 DataCLX 可能运行的任何其他平台。

## Kylix 2 开发

# 第 12 章：dbExpress 和 DataCLX

## 复杂度

> 注意：dbExpress 的目标之一是实现一个轻量、快速的数据访问层，与 BDE 相比，其配置和部署问题最少。对 BDE 的最大抱怨之一是 Delphi 部署中始终存在的耗时安装和配置问题。

![](img/d784fa8294cae585d61ec86b987ea212_275_0.png)

## 配置

dbExpress 的配置主要通过两个文件完成：`dbxdrivers` 和 `dbconnections`。`dbxdrivers` 文件包含所有已安装的 dbExpress 驱动程序的信息。`LibraryName` 和 `VendorLib` 属性指定了特定特定库的名称，通过这些库向数据库发送请求和响应。除了这些属性，`dbxdrivers` 文件的每个部分包含数据库连接的默认参数值。每个新连接都使用此驱动程序创建，这些值被插入为连接默认。`dbxdrivers` 配置文件所示：

```
[Installed Drivers]

INTERBASE=1

[INTERBASE]

GetDriverFunc=getSQLDriverINTERBASE

LibraryName=libsql.so

VendorLib=libgbds.0

BlobSize=-1

CommitRetain=True

Database=database.db

Interbase TransIsolation=ReadCommitted

Password=masterkey

RoleName=RoleName
```
