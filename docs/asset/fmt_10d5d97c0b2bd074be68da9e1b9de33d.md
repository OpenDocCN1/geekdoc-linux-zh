
# DB2 Connect 概述

`DB2 Connect` 提供 `DRDA` 应用程序请求者 (`AR`) 功能。`DB2 Connect` 允许运行在 `Linux`、`UNIX` 和 `Windows` 平台上的 `DB2 UDB` 应用程序访问并更新 `DB2 for MVS`、`DB2 for OS/390`、`DB2 for z/OS`、`DB2 for VM and VSE`、`DB2 for iSeries` 以及其他符合 `DRDA` 标准的数据库管理系统的数据。`DB2 Connect` 包含了以下 `DB2` 工具和功能：

- 命令行处理器 (`CLP`)，允许您发布 `SQL` 语句以访问主机平台。
- 数据库系统监控，问题领域的辅助工具。
- `bind`，允许您将包绑定到主机平台。
- `IMPORT` 和 `EXPORT` 程序，允许您在主机平台和 `DB2 Connect` 工作站之间移动数据。

## 连接到 DB2 数据库服务器

`DB2` 通用数据库可以在本地运行，并由安装了 `DB2` 运行时客户端的远程客户端访问。`DB2` 运行时客户端提供运行时环境，允许客户端访问一个或多个远程数据库。`DB2` 客户端包支持包括 `Windows`、`AIX`、`HP-UNIX`、`Linux` 和 `Solaris` 在内的许多平台。如果您想从数据库服务器跨局域网访问数据，请安装工作组版 (`Workgroup Edition`) 或企业版 (`Enterprise Edition`)。每个想要访问数据库服务器的客户端工作站都必须安装 `DB2` 运行时客户端。支持的局域网协议：命名管道 (`Named Pipes`)、`NetBIOS` 和 `TCP/IP`。

除了为应用程序提供环境外，运行时还提供了功能完整的命令行处理器。此外，运行时客户端还带有 `ODBC` 和 `JDBC` 支持。

`DB2` 个人开发者版（图 1.5）提供了用于 `Windows` 和 `Linux` 的 `DB2` 通用个人版和 `DB2 Connect` 介质。这些

`CD-ROM` 仅用于测试应用程序。如果您需要安装并使用数据库，必须购买 `DB2` 通用数据库产品获取有效许可。

![](img/aa524d8157d0abd09e6f87c5b1aeab3b_26_0.png)

图 1.5 连接到 `DB2 UDB` 数据库服务器。

- 适用于所有平台的运行时客户端。应用程序可以在任何系统上的运行时客户端上运行。运行时客户端不具备管理客户端的某些功能，例如 `DB2` 控制中心和事件分析器，因此占用的空间较小。
- `DB2` 扩展程序 (`DB2 Extenders`)
- `VisualAge for Java`，专业版 (`Windows`)
- `Webphere Studio`
- `Webphere Application Server`，标准版
- 查询管理设施（可试用并购买）

此外，对于两个版本的开发版（`Developer's Editions`），您还可以获得其他可能对开发应用程序有用的软件副本。这些软件可能会随时间而变化，并附带使用许可协议。

`DB2 Connect` 提供了访问主机数据库的 `DRDA` 应用请求者 (`AR`) 支持。`DB2 Connect` 可 `DB2 Connect` 个人版、`DB2 Connect` 企业版或 `DB2 Connect` 无限制版中使用。见图 1.6。

![](img/aa524d8157d0abd09e6f87c5b1aeab3b_27_0.png)

图 1.6 `DRDA` 应用请求者 (`AR`) 支持。

`DB2 Connect` 个人版提供从单个工作站访问位于 `OS/390`、`z/OS`、`OS/400`、`VM` 和 `VSE` 等服务器上的 `DB2` 数据库，以及访问 `UNIX` 和 `Windows` 操作系统上的 `DB2` 通用数据库。`DB2 Connect` 个人版提供了与 `DB2 Connect` 企业版相同的 `API` 集。该产品目前适用于 `Linux` 和 `Windows` 操作系统。

`DB2 Connect` 个人版用于将单个 `Windows` 操作系统或工作站连接到主机或 `iSeries` 数据库。`DB2 Connect` 个人版最数据库服务器提供原生 `TCP/IP` 支持，且部署的应用程序为传统二层客户端/服务器应用程序的环境。

`DB2 Connect` 企业版是一个连接服务器，它集中并管理从多个桌面客户端和 `Web` 到主机或 `iSeries` 系统上 `DB2` 数据库的连接。`IBM` 用于 `iSeries` 的 `DB2` 通用数据库 (`UDB`)、用于 `OS/390` 和 `z/OS` 的 `DB2` 以及用于 `VSE` 和 `VM` 的 `DB2` 仍然是全球性组织管理大多数关键数据的首选系统。虽然这些主机和 `iSeries` 数据库负责管理，但将其与运行在 `Windows` 和 `UNIX` 工作站上的应用程序集成仍需要大量工作。

`DB2 Connect` 企业版允许本地和远程客户端使用结构化查询语言 (`SQL`)、`DB2 API`（应用程序接口）、`ODBC`（开放数据库连接）、`JDBC`（Java 数据库连接）、`SQLI`（Java 嵌入 `SQL`）或 `DB2 CLI`（调用级接口）创建、更新和管理 `DB2` 数据库和主机。此外，`DB2 Connect` 支持 `Windows` 数据接口，如 `ActiveX` 数据对象 (`ADO`)、远程数据对象 (`RDO`) 和 `OLE DB`。

`DB2 Connect` 企业版通常安装在中间服务器上，以将 `DB2` 客户端连接到主机或 `iSeries` 数据库。它也可以用于多个本地用户希望直接访问主机或 `iSeries` 服务器的机器。

`DB2 Connect` 企业版最适用于环境：

- 主机和 `iSeries` 数据库服务器不支持原生 `TCP/IP` 连接；不希望通过 `SNA` 从桌面工作站直接连接。
- `Web` 服务器运行基于 `Web` 的应用程序。
- `Web` 服务器运行使用数据感知 `Java` 应用程序的 `Web` 应用程序。
- 使用中间层应用程序服务。
