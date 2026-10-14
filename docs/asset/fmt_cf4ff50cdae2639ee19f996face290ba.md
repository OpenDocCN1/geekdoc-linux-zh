
- 策略——涉及项目范围以及项目将如何进行的想法。
- 分析——确定提议系统的需求以及项目规划。
- 设计——涉及数据库设计和编程模块设计。
- 实施——系统的编程和测试。
- 支持——系统投入生产，培训用户使用系统，并为系统提供支持。

## 设计师概述

- 子用户—通过同义词访问存储库的 Oracle 账户。
- 存储库—由用于与数据交互的表、视图以及用于管理这些表的存储组成。

## 大写 CASE 与小写 CASE

一个常用的术语是给定的 CASE 工具是大写 CASE（upper CASE）工具还是小写 CASE（lower CASE）工具。大写 CASE 工具用于定义系统需求，并生成图表和文档，供用户在项目早期阶段进行评审。大写 CASE 工具不用于生成实际的数据库或程序模块。小写 CASE 工具主要关注软件开发生命周期（SDLC）的设计和构建阶段。它们通过生成构建数据库和程序的语法来提高生产力。单靠任何一种工具都是不够的，因为大写 CASE 工具不会提高生产力，而小写 CASE 工具则不提供供用户验证的文档。

## 设计师概述

`Designer` 提供了完整的大写 CASE 和小写 CASE 解决方案，并支持整个 SDLC。

分析阶段创建的逻辑模型将成为设计阶段创建的物理模型的基础。应用程序是使用该模型生成的，因此，任何业务上的变化都会立即反映在应用程序中。客户也可以使用非 Oracle CASE 方法论。

安装 `Designer` 的最低需求列如下（客户端、服务器端）。

客户端需求包括：

- Pentium 90MHz 处理器或更高版本
- CD-ROM 驱动器
- 根据所选选项需要 300MB-600MB 空闲磁盘空间
- 运行应用程序至少 40MB 交换空间
- 32MB 可用 RAM
- 1GB 硬盘
- NT 4.0, Windows 95 或 Windows 98
- `SQL*NET` 版本 2.3.4（仅在针对远程服务器运行时才需要 `SQL*NET`）
- `SQL*Plus` 3.3.4 或 `SQL*Plus` 8.0.4（用于 Oracle 8 数据库）
- `Net8 client` 8.0.4（用于 Oracle 8 数据库）
- 显示设置至少使用 640x480。

### 第 32 章 管理员使用的 Designer

服务器端需求包括：

- Oracle7 版本 7.3.4 或更高
- `Shared_pool_size` 至少 18MB
- 推荐的优化器模式是基于成本（COST-based）
- 至少 30MB 可用 RAM
- `SYSTEM` 表空间留 60MB 用于存储库的 PL/SQL 包、过程和视图
- `ROLLBACK` 表空间留 70MB 用于安装存储库
- `SQL*Plus` 3.3.4 或 `SQL*Plus` 8.0.4（用于 Oracle 8 数据库）
- `Net8 client` 8.0.4（用于 Oracle 8 数据库）
- 对于基于 PC 的服务器使用 Windows NT 4.0、Windows 95 或 Windows 98
- 对于基于 UNIX 的服务器使用 Solaris 2.5 或类似的 UNIX 系统

![](img/563fad4219fcb3a5c1f1e5cc91d831ce_767_0.png)

有关产品可用性的最新信息，请联系 Oracle 全球客户支持。截至编写本模块的日期，最新的可用版本是 `Designer R2.1.2`，并已通过以下软件的认证：

- Windows NT 4.0, Windows 95 和 Windows 98
- Oracle7.3.4 或更高
- Designer Object Extensions（对象数据库设计器）R2.1.1
- 应用了 1998 年 10 月补丁的 Developer 2.1 生成
- Web Server 3.0.1, 3.0.2 和 4.0
- Netscape 3.04 Gold, Netscape 4.0.6, Internet Explorer 3.0.2 和 Internet Explorer 4.01
- Visual Basic 4.0 或更高

![](img/563fad4219fcb3a5c1f1e5cc91d831ce_767_1.png)

你应该确保所有客户端工具和存储库运行在相同的发布级别，以避免兼容性问题。

## 与 Designer/2000 R1.3.2 的差异

`Designer` 2.x 版本提供了许多新功能。这些功能汇总在以下列表中。

扩展的服务器生成包括：

- 支持 Oracle 7, Oracle RdB 和 Oracle Web 服务器
- 支持非 Oracle 数据库：MS SQL Server, Sybase, DB2/2 和 Informix
- 支持 ODBC 数据库
- 为表的 DML 和锁表过程生成 API

客户端生成包括：

- 设计复用：定义模块后，这些组件可以与其他模块共享
- 应用程序逻辑：存储 PL/SQL, Visual Basic 和 Java 代码
- 生成器集成
- 基于存储库中的声明式设计信息生成数据库触发器
- 应用程序逻辑的 100% 逆向工程以及 100% 生成

设计编辑器包括：

- 单一的、完全集成的设计和生成环境
- 通过向导、拖放、就地编辑、右键菜单和同步更新最大化地提高易用性

到 `Designer` R2.x 的迁移路径包括：

- `Designer` R2.x 可以对 `Designer` 2000 R1.x 存储库进行升级。

应用程序升级包括：

- `Designer` R2.x 可以对 `Designer` 2000 R1.x 存储库进行升级。可以使用设计编辑器 (`RON`) 升级系统。存储库管理工具 (`RAU`) 可用于管理存储库。设计编辑器可用于设计系统。生成器可创建服务器端组件和客户端应用程序。

## Designer 组件

`Designer` 工具集包含列表中的组件。

存储库服务包括：

- 存储库对象导航 (`RON`)
- 矩阵图表
- 存储库管理

系统建模器包括：

- 实体关系图表
- 功能层次图表
- 数据流图表

系统设计器包括：

- 设计编辑器
- 生成器

`Designer` 组件如图 32.1 所示。

### 图 32.1

`Designer` 界面

![](img/563fad4219fcb3a5c1f1e5cc91d831ce_770_0.png)

界面由以下部分组成：

- 系统需求建模：此区域的工具用于对业务过程建模、创建 E-R 图以及创建实体、功能和数据流的模型。
- 生成初步设计：此区域的数据库转换器和应用程序转换器用于从早期模型创建设计。
- 设计与生成：此区域的工具用于设计表示系统功能的系统。可以使用存储库中的信息创建服务器端组件和客户端应用程序。
- 工具：此区域的工具用于管理存储库；交互式编写基于 SQL 的查询并获取在线帮助。

## 设计编辑器

设计编辑器替换并增强了数据图表、模块数据图表、模块网络图表、模块逻辑导航和偏好导航的功能。设计编辑器是一个集成环境，允许您在设计时执行各种任务（参考图 32.2 和 32.3），包括：

- 创建模块图
- 创建数据图
- 拖放功能
- 允许在图表上下文之外处理数据模型的导航

### 第 32 章 针对管理员的设计器

图 32.2

设计编辑器导航器模块。

![](img/563fad4219fcb3a5c1f1e5cc91d831ce_771_0.png)

可重用模块组件

图 32.3

设计编辑器导航器服务器模型。

![](img/563fad4219fcb3a5c1f1e5cc91d831ce_771_1.png)

```
TEST()
- Draggable Module Components
+ Module
+ Module Network
+ Domains
+ Relational Table Definitions
+ Relational View Definitions
+ VIEW
+ Snapshot Definitions
- PPPP
- Instance Beta
+ Forms Generator
+ Report Generator
+ WebServer Generator
+ Help Generator
- Module Diagrams
```
