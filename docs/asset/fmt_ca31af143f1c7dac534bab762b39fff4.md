
`ibm_db2`: `ibm_db2` 扩展提供了一种过程式应用程序接口，用于创建、读取、更新和写入数据库操作，此外还能广泛访问数据库元数据。它可以与 PHP 4 或 PHP 5 一起编译。

`pdo_ibm`: `pdo_ibm` 是 PHP 数据对象 (`PDO`) 扩展的驱动程序，它通过 PHP 5.1 中引入的标准面向对象数据库接口提供对 DB2 数据库的访问。它可以针对 DB2 库直接编译。

PHP 扩展和驱动程序可以从 [http://pecl.php.net/](http://pecl.php.net/) 的 PECL 存储库免费获取。扩展和驱动程序的 Windows 构建版本可在 [http://sourceforge.net/projects/db2mc/files/](http://sourceforge.net/projects/db2mc/files/) 获取。

在 Linux 和 UNIX 上安装 PHP 扩展需要 IBM Data Server Driver for ODBC and CLI。`ibm_db2` 和 `pdo_ibm` 都基于 IBM DB2 CLI 层。

## 1.3.8 Ruby on Rails

Ruby 是一种开源的面向对象语言。Rails 是使用 Ruby 创建的 Web 框架。Ruby on Rails (`RoR`) 是开发数据库支持 Web 应用程序的理想手段。这项热门新技术基于模型、视图、控制器 (`MVC`) 架构，并遵循敏捷软件开发的原则。

Rails 不需要特殊的文件格式或集成开发环境 (`IDE`)；您可以使用文本编辑器开始。不过，有多种支持 Rails 的 IDE 可用，例如 RadRails，它是 Eclipse 的一个 Rails 环境。有关 RadRails 的更多信息，请访问 [http://www.radrails.org/](http://www.radrails.org/)。

DB2 支持 Ruby 1.8.5 及更高版本以及 Ruby on Rails 1.2.1 及更高版本。`IBM_DB` gem 包含 `IBM_DB` Ruby 驱动程序和 Rails 适配器，允许您与 DB2 交互，并基于 CLI 层。必须与 IBM Data Server Client 一起安装此 gem。安装 `IBM_DB` 驱动程序和适配器时，可以使用 Ruby gem 或作为 Rails 插件。

## 1.3.9 Perl

Perl 是一种流行的解释型编程语言，在许多操作系统上均可免费使用。它使用动态 SQL，非常适合用于应用程序原型设计。

Perl 提供了一个名为数据库接口 (`DBI`) 模块的标准模块，用于访问不同的数据库。该模块可从 [http://www.perl.com](http://www.perl.com) 获取。该模块与不同数据库供应商的驱动程序进行“通信”。在 DB2 的情况下，这是 `DBD::DB2` 驱动程序，可从 [http://www.ibm.com/software/data/db2/perl](http://www.ibm.com/software/data/db2/perl) 获取。

## 1.3.10 Python

Python 是一种常用于脚本编写的动态语言。它强调代码可读性，并支持多种编程范式，包括过程式、面向对象、面向方面、元编程和函数式编程。Python 非常适合快速应用程序开发。

## 1.4 XML 和 DB2 pureXML

表 1.4 展示了可用于从 Python 应用程序访问 DB2 数据库的扩展。

| 扩展 | 描述 |
| :--- | :--- |
| `ibm_db` | 由 IBM 定义。<br>提供对高级功能的最优支持。<br>允许你发出 SQL 查询、调用存储过程、使用 pureXML® 以及访问元数据信息。 |
| `ibm_db_dbi` | 实现了 Python 数据库 API 规范 v2.0。<br>它不提供 `ibm_db` API 支持的一些高级功能。<br>如果你有一个使用支持 Python 数据库 API 规范 v2.0 的驱动器的应用程序，你可以轻松切换到 `ibm_db`。`ibm_db` 和 `ibm_db_dbi` API 是一起打包的。 |
| `ibm_db_sa` | 支持 SQLAlchemy，这是一个流行的开源 Python SQL 工具包和对象-关系映射器 (`ORM`)。 |

表 1.4 - IBM 数据服务器 - Python 扩展

*可扩展标记语言 (XML)* 是 Web 2.0 工具和技术以及*面向服务体系结构 (SOA)* 的底层技术。IBM 很早就认识到 XML 的重要性，并投入大量资源以提供 pureXML® 技术——一种为在 DB2 软件中更好地存储 XML 文档提供支持的技术。

2006 年推出的 DB2 9 是一个混合数据服务器：它允许原生存储关系数据以及层次数据。虽然市场中的 DB2 早期版本和其他数据服务器可以存储 XML 文档，但 DB2 9 中使用的存储方法提高了性能和灵活性。借助 DB2 9 的 pureXML 技术，XML 文档在内部以解析后的层次方式存储为一棵树；因此，处理 XML 文档的能力得到了极大增强。DB2 的较新版本，如 DB2 9.5 和 DB2 9.7，进一步改进了对 pureXML 的支持。*第 15 章，DB2 pureXML* 详细论述了这一主题。

## 1.5 Web 服务

作为一个简单的定义，可以将 Web 服务看作是一个你可以通过网络调用的函数，你不需要知道开发该函数所使用的编程语言，不需要知道该函数将在哪个操作系统上运行，也不需要知道其运行的位置。Web 服务允许一个应用程序使用基于 XML 的可扩展行业标准协议与另一个应用程序交换数据。这在*图 1.8*中进行了说明。

![](img/5f6ba170efa3a607142589708531bef8_39_0.png)

图 1.8 – 示例 Web 服务的工作原理

在图中，假设左侧代表一家虚构航空公司 Air Atlantis 的系统，该系统使用 Linux 上的 DB2，并在 DB2 数据库中以 XML 格式存储其航班信息。右侧是另一家虚构航空公司 Air Discovery 的系统，该系统使用运行在 Windows 上的 SQL Server。现在假设 Air Atlantis 和 Air Discovery 签署了一项合作协议，两家公司希望共享调度和定价信息以协调它们的航班。鉴于两家公司使用不同的操作系统（Linux、Windows）和不同的数据服务器（DB2、SQL Server），在这两家公司之间共享信息可能是一个挑战。当 Air Atlantis 更改其从多伦多飞往北京的航班时刻表时，Air Discovery 如何自动调整其从北京飞往上海的中转航班时刻表？答案在于 Web 服务。Air Atlantis 可以通过创建一个*数据 Web 服务*来公开其部分航班信息，该服务返回存储过程（`getFlightInfo` 存储过程）的输出，其中包含来自 DB2 数据库的航班信息。*数据* Web 服务是基于数据库信息的 Web 服务。当此数据 Web 服务部署到 WebSphere Application Server 等应用程序服务器时，像 Air Discovery 这样的客户端或合作伙伴可以轻松地使用浏览器访问 Air Atlantis 的航班信息。在这个例子中，Air Atlantis 充当 Web 服务提供者，因为它开发并提供了该 Web 服务，而 Air Discovery 充当 Web 服务消费者，因为它消费或使用该 Web 服务。

Air Discovery 还可以从其自身的 JDBC 应用程序中调用该 Web 服务，以便执行使用其 SQL Server 数据库中的数据进行的计算。例如，如果从多伦多飞往北京的航班平均耗时 12 小时，Air Discovery 可以通过将 Air Atlantis 航班离开多伦多的起飞时间加上飞行时间以及几个缓冲小时，来计算出从北京飞往上海的中转航班时刻表。在 Air Discovery 系统中，可用于缓冲的小时数可以存储在 SQL Server 数据库中，而在 JDBC 应用程序中使用的简单等式如下所示：

![](img/5f6ba170efa3a607142589708531bef8_40_0.png)

如果 Air Atlantis 更改其航班起飞时间，当它调用 Web 服务时，此信息会自动传达给 Air Discovery 系统。

## 1.6 管理 API

DB2 软件（“DB2”）提供了大量管理 API，开发人员可以使用这些 API 构建自己的实用程序或工具。例如，要创建数据库，你可以调用 `sqlcrea` API；要启动实例，使用 `db2lInstanceStart` API；或者要将数据导入表中，使用 `db2lImport` API。完整的列表可在 DB2 信息中心中找到。有关 DB2 信息中心的 URL，请参见*资源*部分。

## 1.7 开发工具

Microsoft Visual Studio 和 Eclipse 是当今开发人员使用的两个最受欢迎的集成开发环境 (`IDE`)。这两个 IDE 都能很好地与 DB2 软件（“DB2”）配合使用。
