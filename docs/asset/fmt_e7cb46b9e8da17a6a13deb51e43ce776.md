
### 安装
`dbMan` 以 RPM 包的形式分发，也提供源码形式。可以从 `dbMan` 主页 `http://dbman.linux.cz/` 获取 `dbMan`。该网站包含了一份安装指南文档，你需要安装它才能使用。

**连接到数据库服务器。** 你可以 X 应用程序启动 `dbMan`，也可以作为纯文本控制台应用程序。要在 X 环境下启动，请在 `xterm`（或其他 X 终端）中输入 `dbman` 并按回车。要作为控制台应用程序启动，在 shell 提示符下输入 `dbman -l`（小字母 L，不是数字 1）并按回车。

启动时，`dbMan` 会提示你输入主机名、端口、`DBD` 驱动程序、数据库名、登录名和密码。为数据库提供所需的值（有关 DBI 连接的信息，请参见第 12 章“DBI 与 Perl”）。

### 获取数据
`dbMan` 的用户界面非常简单，你可以在控制台版本中使用与图形版本相同的命令。在图形版本中，只需在标记为 SQL 的字段中输入 SQL 语句，并点击 Do 或按 `Ctrl+Enter`。结果将出现在滚动窗口区域，如图 10.6 所示。

`dbMan` 具有一些扩展功能，包括描述表结构、在浏览器网格中显示 SQL 查询结果，以及在浏览器网格中编辑表的内容。`dbMan` 还包含 `\x` 命令，它可以将表定义及其内容转储为 SQL 。要查看 `dbMan` 功能的完整列表，请查看帮助菜单中的“内联命令索引”或查看 `dbMan` 文档。

## Gnome Transcript

`Gnome Transcript` 是一个允许你定义表和数据输入表单的图形环境。你可以使用这些表单从表中添加、编辑和删除数据。在编写此时，`Gnome Transcript` 支持 PostgreSQL 和 MySQL。更多信息（包括下载）可以在 `http://gtranscript.sourceforge.net` 找到。

## PostgreSQL 工具

让我们来看看一些专门为 PostgreSQL 提供的工具。

- `kpsql` 是一个图形查询工具，用于向 PostgreSQL 数据库服务器发送 SQL 并查看结果。该工具具有 SQL 语法高亮功能，并允许你生成多种格式的输出，包括 HTML 和分隔符文本。你可以在 `www.mutinybaysoftware.com/kpsql` 获取 `kpsql`。
- `PgAccess` 这是一个用 Tcl/Tk 编写的复杂数据库开发环境。它具有许多模仿 Microsoft Access 风格的功能，包括表单生成器、报告设计器、架构设计工具和强大的功能。`PgAccess` 主页位于 `www.flex.ro/pgaccess`。

## Oracle 工具

以下是一些专门为 Oracle 设计的工具：

- `OraSoft` 应用程序套件。适用于 Linux 的 `OraSoft` 应用程序位于 `http://oracle.matthouse.com`，这是一个构建全功能套件的开发项目，包括表浏览器、存储过程编辑器和许多其他功能。
- `DBD:Oracle` 驱动（参见第 12 章中“安装数据库驱动程序”章节以了解如何获取）是一个强大的管理工具，一个令人印象深刻的工具。

## MySQL 工具

以下是两个与 MySQL 工作的工具：

- `MySQLGUI`。`MySQLGUI` 是 MySQL 的图形化前端，在主站（`www.mysql.com`）的下载页面分发。
- `KMySQLAdmin`。这是一个 MySQL 的管理工具，你可以用它监控服务器、修改用户权限、修改表和导出数据。它包含一个具有一些酷功能的表浏览器，包括查询表的视觉化界面以及导出为文本、HTML 或 LaTeX 的能力。`KMySQLAdmin` 位于 `www.webeifer-de/alin/Programs/KMySQLAdmin/index.html`。

## Sybase 工具

现在来看看为 Sybase 设计的工具：

- `sqsh`。`sqsh` 是 Sybase 自带 `isql` 程序的极替代品。`isql` 是一个向 Sybase 发送 SQL 的有用批工具，而 `sqsh` 是一个功能齐全 SQL Shell，包含了作业控制、变量、重定向等许多功能。`sqsh` 主页位于 `www.voicenet.com/-gray/`
- `Sybase central`。这是一个全面的 Sybase 管理工具。它包含了管理用户、数据库、表以及 Sybase 服务器许多其他方面的功能。它位于 `http://perso.wanadoo.fr/laserquest/linux/`

## 驱动程序和驱动管理器

如果你正在编写一个需要连接数据库的程序，建立这种连接的最佳方法是什么？就像图形应用程序需要链接 X Windows 系统库（如 `libX11.so,0`）一样，需要连接到 MySQL 数据库的应用程序需要链接 `libmysqlclient.so`。与 MySQL 一样，每个数据库系统都包含头文件以及用于连接到数据库的库。PostgreSQL 拥有 `libpq`，Oracle 拥有 `libclntsh.so`，以此此类推。

总的来说，涉及这些客户端库并不是一个好主意，因为你将编写出一个只能与特定数据库运行的应用程序。相反，你应该使用数据库无关的 API，例如 `ODBC`（C 和 C++）、`DBI`（Perl）或 `JDBC`（Java）。这样做有许多优势：

- 使用数据库无关的 API，你的程序在其他平台和数据库服务器上具有更高的可移植性。
- 每个客户端库本质上做的是相同的事情：它便于了访问、查询和修改存储在数据库中的数据。为什么要为每个数据库都使用不同的客户端库呢？

如果你使用 `ODBC`（或 `DBI` 或 `JDBC`）开发 MySQL 应用程序，可以通过不同的数据库驱动程序将其转换为 PostgreSQL、Oracle、Mini SQL 或 Sybase 应用程序。你的程序连接到驱动程序管理器，它充当你的程序和数据库之间的中间人。驱动程序管理器使用你系统上的某个驱动程序来实际向数据库发出调用。作为程序员，你只需要关心 `ODBC`（或 `DBI` 或 `JDBC`）API，而不需要考虑你想要连接的任何数据库的客户端 API。

然而，数据库无关的 API（如 `ODBC`）让你免于担心程序如何连接和与数据库交互的底层机制。如果你选择使用特定于厂商的 SQL 扩展，可能会引入额外的复杂性，降低应用程序的可移植性。例如，MySQL 支持 `REPLACE` 语句，它将 `DELETE` 和 `INSERT` 合并为一个操作。其他数据库服务器不支持，`JDBC`、`ODBC` 或 `DBI` 将无法翻译你的 SQL。

## ODBC

`ODBC` 是数据访问 API 的古老祖先之一。它是用于开发连接到 SQL 数据库系统的可移植应用程序的标准 API。`ODBC` 最初在 Microsoft Windows 平台上开发，但也适用于许多其他平台。`ODBC` 应用程序通常用 C 或 C++ 编写。我们在本书中不会查看任何特定的 `ODBC` 示例，但从其他语言到 `ODBC` 有桥接，包括 Java (`JDBC-ODBC` 桥) 和 Perl (`DBI:ODBC`)。此外，`GNOME-DB` 可以连接到 `ODBC` 数据源，即使你在本书中没有学习编写 `ODBC` API，你也可以学习如何设置 `ODBC` 驱动程序，并从 Java（见第 11 章）、Perl（见第 12 章）或用 C 编写的 `GNOME-DB` 应用程序（见第 13 章）中使用它们。

Linux 有两个免费分发的 `ODBC` 工具件：`iODBC` 和 `unixODBC`。这些工具件包含了 `ODBC` 驱动程序管理器，它充当数据库和 `ODBC` 驱动程序之间的媒介。`ODBC` 驱动程序执行连接数据库服务器的工作。除了驱动程序管理器，两个 `ODBC` 工具件都包含了开发 `ODBC` 应用程序和驱动程序所需的头文件和库。`unixODBC` 包还包含几个 `ODBC` 驱动程序。

### ODBC

`ODBC` 是由 OpenLink Software (`www.openlink.com`) 维护的 `ODBC` 驱动程序管理器和软件开发包。你可以在 `www.odbc.org` 找到关于 `ODBC` 的更多信息以及最新版本的下载。

#### 安装
你可以下载 `ODBC` 的二进制或源码发行。源码发行包含一个 `README` 和 `INSTALL` 文件，其中包含了如何编译和安装它的说明。自动配置脚本使得在编译之前准备源代码变得简单。

#### 安装驱动程序
一旦你安装了 `ODBC`，你就需要获取一些 `ODBC` 驱动程序，以便连接到数据库。`ODBC` 应该与 Linux 上的任何 `ODBC` 驱动程序兼容，包括 `unixODBC` 提供的免费驱动程序。要查找特定数据库服务器的 `ODBC` 驱动程序，请咨询该服务器的主页（数据库主页列表见第 9 章表 9.6）。`ODBC` 的维护者 OpenLink Software 为许多数据库服务器提供了商业驱动。其他供应商可能有类似的产品。

一旦你获得了想要配合 `ODBC` 使用的 `ODBC` 驱动程序，请参考 `ODBC` 文档详情。到目前，你需要手动编辑 `ODBC` 配置文件（但开发者正在开发图形化配置工具）。

## unixODBC

`unixODBC` 项目的特点是一个 `ODBC` 驱动程序管理器、几个 `ODBC` 驱动程序以及用于配置 `ODBC` 的图形化实用。此外，`unixODBC` 还包含一个驱动程序模板，旨在让编写新驱动程序变得更容易。`unixODBC` 主页地址为 `www.odbc.org`，你可以在那里下载 `unixODBC` 源码并浏览在线文档。

#### 安装
`unixODBC` 源码包含 `README` 和 `INSTALL` 文件，帮助你为编译和安装做好准备。`unixODBC` 自带的 autoconfigure 脚本处理大部分工作，因此安装应该是顺畅的。一旦你安装了 `unixODBC`，就需要对其进行配置。在 Linux 上配置 `ODBC` 曾是一个大难题，而 `unixODBC` 通过 `ODBCConfig` 程序极大地简化了这一点，该程序具有 Windows 上 `ODBC` 用户熟悉的界面。

### 添加驱动程序

`unixODBC` 分发包含几个驱动程序。要配置你的安装以使用这些驱动程序：

1. 登录 `root` 用户。
2. 如果尚未启动，请启动 X Windows 系统。
3. 从 shell 提示符运行 `ODBCconfig` 程序。出现 `ODBC` 数据源管理员，如图 10.7 所示。
4. 选择 Drivers（驱动程序）选项卡。起初列表中没有驱动程序。点击 Add（添加），出现 New Driver 对话框（见图 10.8）。
5. 你可以提供所需的驱动程序名称和描述。例如，我们将使用 PostgreSQL 驱动程序，因此在 Name 中输入 PostgreSQL，在 description 中输入 “PostgreSQL ODBC Driver”。
6. 一个驱动程序由两个共享库组成：一个是驱动程序本身，另一个是添加新数据源的设置代码。你必须阅读 `unixODBC` 文档以获取这两个共享库的位置。在图 10.8 中，它们位于 `/usr/local/lib/`。`libodbcpsql.so.1.0.0`（驱动程序）和 `libodbcpsql.so.1.0.0`（设置）。
7. 点击 OK 添加驱动程序。

图 10.7 `unixODBC` 数据源管理员。

图 10.8 带有 New Driver 对话框的 `ODBC` 设置

### 添加数据源

一旦安装了驱动程序，你就可以配置所需的多个数据源。数据源是与驱动程序关联的参数命名资源。每个数据源由数据源名称（`DSN`）命名。

你可以使用数据源为数据库服务器创建逻辑入口点。例如，`PRODUCTION` 源可以使用 PostgreSQL 驱动程序连接到 `odbc.org` 上的 PostgreSQL 服务器，对应于服务器的数据库。你还可以有一个 `DEVELOPMENT` 源，它连接到同一个服务器，但使用不同的数据库，对应正在开发的系统。当需要部署开发中的系统时，你可以让你的程序开始使用 `PRODUCTION` 数据源。

在添加数据源之前，你应该决定它是用户数据源（仅对一个用户可用）还是系统数据源（对系统上的所有用户可用）。添加数据源：

1. 以具有访问数据源的用户身份登录。如果你想创建系统数据源，请以 `root` 用户身份登录。
2. 如果尚未启动，请启动 X Windows。
3. 从 shell 提示符运行 `ODBCConfig` 程序。出现 `ODBC` 数据源管理员（见图 10.7）。
4. 要创建用户数据源，点击 User DSN 选项卡。要创建系统数据源，点击 System DSN 选项卡。点击 Add 按钮。出现 Adding New Data Source 对话框，如图 10.9 所示。
5. 选择使用的 `ODBC` 驱动程序（例如 PostgreSQL 驱动程序）。点击 OK。出现 New Data Source 对话框，如图 10.10 所示。
6. 取决你选择的 `ODBC` 驱动程序，New Data Source 对话框可能会有所不同。请查看文档或驱动程序以获取此对话框的详情。
7. 提供新数据源所需的任何值，并点击确定创建新数据源。

图 10.9 使用随 `unixODBC` 提供的 `ODBCConfig` 添加新的数据源

图 10.10 新数据源对话框。

**DataManager.** `unixODBC` 包含一个名为 `DataManager` 的图形实用程序。你可以启动 X Windows 系统，并在 shell 提示符中运行 `DataManager` 命令来运行此程序。`DataManager` 实用程序

图 10.11 `unixODBC` 的 `DataManager` 实用程序。

如图 10.11 所示，它允许你导航数据源、检查数据库结构并执行 SQL 查询。

**查找驱动程序。** 虽然 `unixODBC` 带有许多驱动程序，但你可能需要自行查找其他驱动程序。`unixODBC` 网站包含指向 *Drivers*（驱动）页面的链接，该页面列出了 `unixODBC` 包含的所有驱动程序，以及搜索 `unixODBC` 开发人员知道的所有驱动程序。这是你搜索的好起点。你可能还想参考数据库服务器的主页，因为它们可能也有指向 `ODBC` 驱动程序来源的链接。

## DBI

`DBI` 是 Perl 使用的数据库无关 API。它与 `ODBC` 有许多相似之处，但它是一个更高级接口，设计得比 `ODBC` 更易用。某些 Linux 发行版包含了 `DBI` 和至少一个驱动程序 (`DBD`)，但在某些系统上你可能需要安装它。第 12 章提供了有关安装和使用 `DBI` 的更多细节。

如果你正在使用 Oracle 或 `dbMan`，可能需要使用 `DBI` 连接字符串来指定要连接的数据库。请参第 12 章关于用于不同服务器的各种连接字符串的讨论。

## JDBC

`JDBC` 是 Java 的数据库无关 API。它与 `ODBC` 相似，但像 `DBI` 一样，它在高级别上暴露其功能，这让程序员无需担心连接到数据库的许多细节。有关 `JDBC` 的更多细节请见第 11 章。

## 建模/绘图工具

这里是一些你可能会发现有用的绘图和建模工具：

- `Dia`。`Dia` 是一种与商业产品 Visio 类似的绘图工具。你可以使用 `Dia` 绘制几乎任何类型的图，既可以使用内置形状，也可以创建自己的形状。`Dia` 包含了一套丰富的 UML 图形形状，还用于网络图、实体关系图和流程图。`Dia` 的主页可以在 `www.lysator.liu.se/-alla/dia/` 找到。
- `Argo/UML`。`Argo/UML` 开发者的目标是产生一个为面向对象的设计提供认知支持的系统。虽然它表面看起来是另一个 UML 设计工具，但 `Argo/UML` 会在你开发过程中分析并批判你的设计，维护一个待办任务列表，并提供各种设计表示以帮助你理解你的设计。`Argo/UML` 主页可以在 `www.arguml.com` 访问。
- `DOME`。这一卓越的工具是一个用于开发和使用 CASE（计算机辅助软件工程）软件模型的系统。它支持多种现有记法（如 UML），并具有高度的可扩展性。你可以使用 `DOME` 开发新的记法，或使用任何支持的记法开发图表。在本书期间，正在努力为 `DOME` 添加对实体关系图的支持，但这项工作尚未整合到核心包中。`DOME` 主页在 `www.htconeywell.com/dome/`
- `tgif`。书中的大多数图都是使用 `tgif`制作的，这是一种交互式矢量绘制工具，用于制作各种图。虽然对 UML 或实体关系图没有专门的支持，但 `tgif` 可以轻松开发此类图表。它还具有与万维网集成的图形编辑和浏览功能。坦率地说，我们觉得这令人恐惧又令人敬畏。`tgif` 主页在 `http://bourbon.cs.umd.edu:8001/tgif/`

## 总结

本章介绍了许多工具。你如何跟上这些变化？`unixODBC` 网站列出了许多此类工具。

通常情况下，最好找到针对你想要连接的数据库的驱动程序。

例如，如果你使用 `JDBC-ODBC` 桥接到连接 MySQL，那么你的程序需要加载 `JDBC-ODBC` 驱动程序，该程序部分是用 C 语言编写的。然后，`JDBC-ODBC` 驱动连接到 `ODBC` 驱动管理器，再使用 MySQL `ODBC` 驱动连接到数据库。请注意这只是一个示例；如果你想从 Java 连接到 MySQL，你可能会使用适用于 MySQL 的类型 4 `JDBC` 驱动程序之一。

使用 `JDBC` 驱动不仅可以避免额外的间接层，而且你通常可以找到 100% Java 编写的 `JDBC` 驱动程序（这些被称为类型 3 和类型 4 驱动，将在本节稍后讨论）。如果你使用纯 `JDBC` 驱动程序，你的应用程序更有可能受益于 Java 的跨平台能力。使用 Java 和原生代码混合的驱动程序（例如 `JDBC-ODBC` 桥接）会对可移植性产生显著障碍。

Sun Microsystems 维护了一个 `JDBC` 驱动程序列表，你可以在网站上下载（或购买）这些驱动程序。该列表可以通过 `http://java.sun.com/products/jdbc/drivers.html` 获取。

`JDBC` 驱动程序分为四类：
