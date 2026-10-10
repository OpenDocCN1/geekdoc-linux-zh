
## 1.3.5 OLE DB

对象链接和嵌入，数据库 (OLE DB) 是一组接口，用于访问存储在多种来源中的数据。它被设计作为 ODBC 的替代品，但扩展以支持更广泛的来源，包括非关系型数据库，例如面向对象数据库和电子表格。OLE DB 使用组件对象模型 (COM) 技术实现。

OLE DB 用户可以使用 IBM OLE DB Provider for DB2 来访问 DB2 数据库。此提供程序具有以下特性：

- 提供程序名称：IBMDADB2
- 支持 OLE DB 提供程序规范的 0 级，包括一些额外的 1 级接口
- 符合 Microsoft OLE DB 规范版本 2.7 或更高版本
- 必须安装带有 Microsoft 数据访问组件 (MDAC) 的 IBM 数据服务器客户端
- 如果未显式指定 IBMDADB2，则默认使用 Microsoft OLE DB 驱动程序 (MSDASQL)。MSDASQL 允许使用 OLE DB 的客户端通过 ODBC 驱动程序访问非 Microsoft SQL Server 数据源，但不保证 OLE DB 驱动程序的全部功能。

## 1.3.6 ADO.NET

.NET 框架是 Microsoft 对组件对象模型 (COM) 技术的替代方案。使用 .NET 框架，您可以使用 40 多种不同的编程语言编写 .NET 应用程序；其中最流行的是 C# 和 Visual Basic .NET。

.NET 框架类库提供了构建 .NET 应用程序的基本构件。该类库与语言无关，并提供操作系统和应用程序服务的接口。您的 .NET 应用程序（无论使用何种语言）都会编译为中间语言 (IL)，这是一种字节码。

通用语言运行时 (CLR) 是 .NET 框架的核心，它即时编译 IL 代码，然后运行它。在运行编译后的 IL 代码时，CLR 激活对象，验证其安全权限，分配内存，执行它们，并在执行完成后清理内存。

以 Java 的工作方式作为类比，在 Java 中，一个程序可以在多个平台上运行，只需很少或无需修改：一种语言，但多个平台。在 .NET 中，用 40 种受支持语言中的任意一种编写的程序可以在一个平台（Windows）上运行，只需很少或无需修改：多种语言，但一个平台。

ADO.NET 是 .NET 框架中提供数据访问支持的方式。ADO.NET 支持连接式和断开式访问。ADO.NET 中断开式数据访问的关键组件是 DataSet 类，其实例充当驻留在应用程序内存中的数据库缓存。

对于连接式和断开式访问，您的应用程序通过被称为数据提供程序的机制使用数据库。各种数据库产品包含它们自己的 .NET 数据提供程序，包括用于 Windows 的 DB2。

.NET 数据提供程序具备以下基本类的实现：

- Connection：建立并管理数据库连接。
- Command：对数据库执行 SQL 语句。
- DataReader：从数据库读取并返回结果集数据。
- DataAdapter：将 DataSet 实例与数据库关联。通过 DataAdapter 实例，DataSet 可以读取和写入数据库表数据。

*表 1.3* 中显示了三个可以与 DB2 软件一起使用的数据提供程序。

| 数据提供程序 | 特性 |
|---|---|
| ODBC .NET 数据提供程序（不推荐） | - 使用 DB2 CLI 驱动程序对 DB2 数据源进行 ODBC 调用。<br>- 其关键字支持和限制与 DB2 CLI 驱动程序相同<br>- 可与 .NET 框架版本 1.1、2.0 或 3.0 一起使用。 |
| OLE DB .NET 数据提供程序（不推荐） | - 使用 IBM DB2 OLE DB 驱动程序 (IBMDADB2)。<br>- 其关键字支持和限制与 DB2 OLE DB 驱动程序相同<br>- 仅可与 .NET 框架版本 1.1、2.0 或 3.0 一起使用。 |
| DB2 .NET 数据提供程序（推荐） | - 扩展了对 ADO.NET 接口的 DB2 支持。<br>- DB2 受管提供程序实现了相同的一组标准 ADO.NET 类和方法<br>- 它定义在 IBM.DATA.DB2 命名空间下。<br>- 可以通过下载以下任意一项获取：<br>  - ODBC、CLI 和 .NET 的数据服务器驱动程序<br>  - IBM 数据服务器运行时客户端<br>  - DB2 数据服务器 |

*表 1.3 - ADO.NET 数据提供程序*

## 1.3.7 PHP

*PHP 超文本预处理器 (PHP)* 是一种开源、平台无关的脚本语言，专为 Web 应用程序开发设计。它可以嵌入到 HTML 中，通常运行在 Web 服务器上，该服务器将 PHP 代码处理并创建 Web 页面作为输出。

PHP 是一种模块化语言。您可以使用扩展来定制可用的功能。一些最受欢迎的 PHP 扩展是用于访问数据库的扩展。IBM 通过两个扩展支持访问 DB2 数据库：

- **ibm_db2:** ibm_db2 扩展提供了一种过程式应用程序接口，用于创建、读取、更新和写入数据库操作，此外还能广泛访问数据库元数据。它可以与 PHP 4 或 PHP 5 一起编译。
- **pdo_ibm:** pdo_ibm 是 PHP 数据对象 (PDO) 扩展的驱动程序，它通过 PHP 5.1 中引入的标准面向对象数据库接口提供对 DB2 数据库的访问。它可以针对 DB2 库直接编译。

PHP 扩展和驱动程序可以从 [http://pecl.php.net/](http://pecl.php.net/) 的 PECL 存储库免费获取。扩展和驱动程序的 Windows 构建版本可在 [http://sourceforge.net/projects/db2mc/files/](http://sourceforge.net/projects/db2mc/files/) 获取。

在 Linux 和 UNIX 上安装 PHP 扩展需要 IBM Data Server Driver for ODBC and CLI。ibm_db2 和 pdo_ibm 都基于 IBM DB2 CLI 层。

## 1.3.8 Ruby on Rails

Ruby 是一种开源的面向对象语言。Rails 是使用 Ruby 创建的 Web 框架。Ruby on Rails (RoR) 是开发数据库支持 Web 应用程序的理想手段。这项热门新技术基于模型、视图、控制器 (MVC) 架构，并遵循敏捷软件开发的原则。

Rails 不需要特殊的文件格式或集成开发环境 (IDE)；您可以使用文本编辑器开始。不过，有多种支持 Rails 的 IDE 可用，例如 RadRails，它是 Eclipse 的一个 Rails 环境。有关 RadRails 的更多信息，请访问 [http://www.radrails.org/](http://www.radrails.org/)。

DB2 支持 Ruby 1.8.5 及更高版本以及 Ruby on Rails 1.2.1 及更高版本。IBM_DB gem 包含 IBM_DB Ruby 驱动程序和 Rails 适配器，允许您与 DB2 交互，并基于 CLI 层。必须与 IBM Data Server Client 一起安装此 gem。安装 IBM_DB 驱动程序和适配器时，可以使用 Ruby gem 或作为 Rails 插件。

## 1.3.9 Perl

Perl 是一种流行的解释型编程语言，在许多操作系统上均可免费使用。它使用动态 SQL，非常适合用于应用程序原型设计。

Perl 提供了一个名为数据库接口 (DBI) 模块的标准模块，用于访问不同的数据库。该模块可从 [http://www.perl.com](http://www.perl.com) 获取。该模块与不同数据库供应商的驱动程序进行“通信”。在 DB2 的情况下，这是 DBD::DB2 驱动程序，可从 [http://www.ibm.com/software/data/db2/perl](http://www.ibm.com/software/data/db2/perl) 获取。

## 1.3.10 Python

Python 是一种常用于脚本编写的动态语言。它强调代码可读性，并支持多种编程范式，包括过程式、面向对象、面向方面、元编程和函数式编程。Python 非常适合快速应用程序开发。

