
# 表 11-1（续）

| 工具 | 用途 | 示例语法 |
| --- | --- | --- |
| `make_binary_release` | 创建编译后的 MySQL 二进制版本。此类文件随后可以通过 FTP 或其他机制传输给本地或远程用户。 | `$ make_binary_release -w --wait` <br> `-1, --no-svlinks`: 使 MySQL 在修复表时不遵循符号链接。<br> `-r, --recover`: 恢复模式，可以修复许多数据库问题。<br> `-0, --safe-recover`: 使用较慢但在某些情况下更可靠的修复方法。<br> `-s, --silent`: 静默模式；仅在发生错误时写入输出。<br> `-S, --sort-index`: 按高低序排序索引；用于优化搜索并按键进行表扫描。<br> `-R index_num, --sort-records=index_num`: 根据索引排序记录，后者由数字指定。 |
| `mysql2mysql` | 将 MySQL 程序（即脚本或 SQL 文件）从 MySQL（MySQL 的前身）转换为 MySQL 的 Shell。处理大多数但并非所有文件。 | MySQL 文档建议使用 `msql2mysql` 的以下两步过程：<br>1. 在 `mysql` 源码上运行该工具。这需要 `replace` 程序，该程序随 MySQL 分发。<br>2. 重新编译 |
| `mysqladmin` | 执行管理任务，如创建或删除数据库、重载权限表、将表刷新到磁盘以及重新打开日志文件。 | `$ mysqladmin command [command-option] command ...` |
重要命令：
- `create db_name`: 创建一个指定名称的新数据库。
- `drop db_name`: 删除指定的数据库及其所有表。
- `flush-hosts`: 刷新所有缓存主机。
- `flush-logs`: 刷新所有日志。
- `flush-tables`: 刷新所有表。
- `flush-privileges`: 刷新所有权限表。
- `processlist`: 显示服务器中活动线程的列表。
- `refresh`: 刷新所有表；关闭并重新打开日志文件。
- `shutdown`: 停止 MySQL 服务器。
| `mysqlbug` | 用于向 MySQL 邮件列表提交错误报告的脚本。 | MySQL 组表示：“我们鼓励每个人使用 `mysqlbug` 脚本来生成报告（或关于任何问题的报告）。可以在发行版的 `scripts` 目录中找到 `mysqlbug`，对于二进制发行版，可以在 MySQL 安装目录下的 `bin` 目录中找到。” |
| `mysqldump` | 将 MySQL 数据库导出到输出文件，该文件可以是 SQL 语句或制表符分隔文本。 | `$ mysqldump [options] database [tables]` |
重要选项：
- `--add-locks`: 在每次导出前使用 `LOCK TABLES`，导出后使用 `UNLOCK TABLE`。
- `-A, --all-databases`: 导出所有数据库。
- `-C,--compress`: 如果客户端和服务器都支持，则压缩客户端和服务器之间的信息。
- `-B,--databases`: 导出多个数据库。所有名称参数均被视为数据库名。
- `--delayed`: 使用 `INSERT DELAYED` 命令插入行。
- `-e,--extended-insert`: 使用多行 `INSERT` 语法进行更紧凑、快速的插入。
- `-F,--flush-logs`: 在开始导出前刷新 MySQL 服务器上的日志文件。
- `-f,--force`: 即使在表导出期间发生 SQL 错误也继续导出。
- `-h,--host-`: 从指定主机上的 MySQL 服务器导出数据。
- `-l,--lock-tables`: 在开始导出前锁定所有表。
- `-d,--no-data`: 不为表写入记录。实际上仅导出模式结构（schema）。
- `-q,--quick`: 快速导出，即无缓冲并直接发送到标准输出
| `mysqlimport` | 将文本文件导入 MySQL 表。 | `$ mysqlimport [options] database_name [要导入到] text_input_file (从此处导入)` |
| `mysqlshow` | 显示有关 MySQL 数据库、表、列和索引的信息。 | `$ mysqlshow [options] [table [column]]` |
| `replace` | `mysql2mysql` 使用的工具，但也具有更通用的适用性。在文件或标准输入中就地更改字符串。用于修改字符串。 | `$ replace abba file2` |

对任何 DBMS 管理员来说，以下工具特别重要：
- `mysisamchk`，因为它有助于维护表的完整性
- `mysqladmin`，因为它是日常管理任务的核心
- `mysqlimport`，因为它允许管理员轻松地将文本文件导入 MySQL 表
- `mysqlshow`，如果你想查看 MySQL 数据库组件的统计数据，则需要它

# 第三方工具

本节总结了用于 Linux 数据库的多种第三方工具，涵盖商业供应商和开源供应商。我们选择了我们认为对数据库管理员可能最有用的工具。

## Brio.Report

`Brio.Report` 是名为 `Brio ONE` 的大型套件组件，提供了 DBMS 报告和管理工具，除例外外，它可以从 Windows 客户端运行。

- 作者：Brio Technology（部分组件从 SQRIBE Technologies 收）
- 网站：`www.brio.com`
- 分发方法：专业销售、商业许可
- 源码可用：否

`Brio.Report` 在 Brio Technology 网站上标记为工业级企业报告套件，包含以下组件，这些组件可以在包含 Linux DBMS 的异构环境中运行。

- `Brio.Report Builder`：基于 Windows 的图形化开发工具，允许您创建企业和 B2B 报告。它包含一个查询生成器，支持多个查询和嵌套子查询，以及报告功能，如加载查找、报告页头和页脚以及异常通知。
- `Brio.Report Viewer`：用于 Windows 客户端的报告查看实用程序，可在打印前显示报告的屏幕视图。
- `Brio.Insight`：一种浏览器插件，为通过 SQR Server 生成报告的数据提供可选的基于 Web 的交互式分析和报告查看功能。
- `Brio.Report SQR Server`：一种报告处理和数据操作工具，提供对 60 多种数据库和操作系统环境组合的原生访问。最新版本的 SQR Server 已经增强，支持 XML 输入/输出以及访问多维数据库。`SQR Server` 允许您向 SQL 查询和命令中添加过程化语言和控制。
- `Brio.Report Personal SQR`：单用户基于 Windows 的 SQR Server 仿真。`Personal SQR` 允许您在部署到后端 SQR 之前，在非 Linux 客户端上本地测试应用程序。

## C/Database Toolchest

`C/Database Toolchest` 实际上允许向现有的、尤其是大型数据集中添加 DBMS 能力。`Toolchest` 提供的库提供了 150 多个数据库管理函数，包括创建、打开和关闭等文件操作。

- 作者：Mix Software
- 网站：`www.mixsoftware.com`
- 分发方法：零售
- 源码可用：是

`C/Database Toolchest` 包含了 C 和 C++ 库以及一个简单的接口。这些工具允许您使用库执行以下任务：
- 转换 dBASE 数据文件
- 创建、打开、关闭等文件操作
- 索引
- 锁定
- 记录操作，如添加、查找、修改和删除
- 查看和压缩

最后，`Toolchest` 提供了 `LDM`，一种可以交互式创建和编辑数据库的管理器。

## SQL 还是 SQR？

不，你没有读错那个缩写。Brio Technology 的 SQR 指结构化查询报告（Structured Query Reporting）。

## CoSORT

`CoSORT` 是一种独立开发的、基于标准的跨平台排序工具，被称为 UNIX 系统上最快、许可最广泛的商业排序包。

- 作者：CoSORT 公司
- 网站：`www.iri.com/external/products.html`
- 分发方法：FTP
- 源码：无

`CoSORT` 是一系列用于数据库、数据仓库和应用程序内部提供排序功能的工具，用于文件排序：提取、排序、总结和报告。`CoSORT` 通过一种软件架构加速数据库加载，该架构直接通过内存传输记录，并可以利用直接顺序并行处理（SMP），即并行 CPU 能力。

`CoSORT` 支持许多文件大小、记录格式和数据类型，包括字母数字和二进制形式；C 和 COBOL 数字；EBCDIC；带符号小数；浮点数；货币；以及儒历和跨国时间戳。它可以从或输出到新或现有的文件、磁带或光盘设备；标准输入和标准输出管道及应用程序。
