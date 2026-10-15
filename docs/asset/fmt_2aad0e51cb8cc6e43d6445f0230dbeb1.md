
- 确保 IBM Java Development Kit 已设置在你的路径中，输入：

```
echo $PATH
```

如果在其中找不到 JDK 路径，请将其附加到 `PATH`。例如，如果你的 JDK 路径是 `/opt/IBMJava2-131/bin`，输入：

```
PATH=$PATH:/opt/IBMJava2-131/bin
```

- 如果你使用 `make` 命令，很可能需要对 `makefile` 文件进行更改，以便使其与你的环境配合使用。

有关 DB2 上 Java 编程的更多信息，请参阅 IBM DB2 UDB Application Development Guide: Building and Running Applications V8, SC09-4825。

除了本节讨论的编程语言外，DB2 还可以使用 BASH 和 AWK 等脚本语言访问。这些脚本语言随 Linux 提供，不需要特殊设置。它们对于简单的 DB2 任务或建模非常方便。

### 8.4 Application tools

DB2 提供了许多用于开发 DB2 应用程序的有用工具，例如 Command Center、Script Center、SQL Assist 和 Development Center。安装 Application Development Client 后，这些工具即可供你使用。

#### 8.4.1 Command Center

DB2 Command Center（图 8-3）是一个功能强大的交互式工具，可用于执行 DB2 SQL 语句和 DB2 命令，以及构建脚本。你可以从 Control Center 的 Tools 菜单或 DB2 提供的任何图形工具启动 Command Center。

### Figure 8-3 Command Center window

在 Interactive 页面上，你可以直接针对 DB2 数据库执行任何 DB2 命令或 SQL 语句。对于复杂的 SQL 语句，Command Center 允许你通过按 Append to Script 按钮将其存储为脚本。此脚本可选择存储在 Task Center 中，以便在特定时间运行。

Script 页面允许你按顺序执行命令、导入存储的脚本以供执行，或生成新脚本。

任何命令或 SQL 语句的结果都显示在 Query Results 页面上。

要显示 DB2 如何为特定 SQL 语句检索你的数据，请使用 Access Plan 页面。

The SQL Assist button starts the SQL Assistant tool (Figure 8-4) which you can use to easily select or modify your data. This tool can be called from many other tools.

![](img/d95c931f4f3da4a6bd0ee55148fefad7_299_0.png)

#### 8.4.2 Development Center

Development Center 是一个功能强大的工具，用于开发存储过程、用户定义函数或结构化类型。要启动 Development Center（图 8-5），请使用命令行输入 `db2dc &` 或从 DB2 提供的任何图形工具的 Tools 菜单启动它。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_300_0.png)

Figure 8-5 Development Center main window

Development Center 为您提供函数和过程，可通过向导或手动创建 DB2 应用程序对象。通过右键单击对象，会显示不同操作的选项。您可以编辑或运行现有对象，创建新对象，或从另一个项目或文件系统导入对象。在目录 `$INSTHOME/sqllib/samples` 中，您会找到许多可导入的示例。图 8-6 显示了从示例目录导入的存储过程示例。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_301_0.png)

Figure 8-6 Stored Procedure edit window

要使用 Development Center 编译存储过程，我们必须配置两个 DB2 环境变量（示例 8-6）：

- `DB2_SQLROUTINE_COMPILER_PATH` 用于设置 C 编译器的路径

- `DB2_SQLROUTINE_COMPILE_COMMAND` 用于定义编译过程的参数。

Example 8-6 Set C compiler environment for Linux

```
DB2SET DB2_SQLROUTINE_COMPILER_PATH=/usr/bin
DB2SET DB2_SQLROUTINE_COMPILE_COMMAND=cc -fpic -I$HOME/sqllib/include SQLROUTINE_FILENAME.c -shared -o SQLROUTINE_FILENAME -L$HOME/sqllib/lib -ldb2
```

> Important: The database server on which you want to use the Development Center must have the Application Development Client installed, even if you are developing from a Windows or Linux Client.

除了存储过程、UDF 和触发器，您还可以使用 Development Center 开发 OLEDB 应用程序。

以下 DB2 UDB 版本 8 手册提供了详细的 DB2 应用程序开发信息：

- IBM DB2 UDB Application Development Guide: Building and Running Applications V8, SC09-4825

- IBM DB2 UDB Application Development Guide: Programming Client Applications V8, SC09-4826

- IBM DB2 UDB Application Development Guide: Programming Server Applications V8, SC09-4827

有关 Development Center 的更多信息，请参阅 IBM DB2 UDB Guide to GUI Tools for Administration and Development, SC09-4851。

#### 8.4.3 Additional development tools

除了随 DB2 发货的工具外，市场上还有许多其他工具。DB2 Development Center 还为以下 Microsoft 产品提供开发插件：

- Visual C++

- Visual Basic

- Visual InterDev

以下是 DB2 在 Linux 上支持的开发工具列表：

- Borland Kylix

  http://www.borland.com/kylix/index.html

- IBM Visual Age for Java

  http://www-3.ibm.com/software/ad/vajava/

- Net.Data

  http://www-3.ibm.com/software/data/net.data/

- WebSphere Integration

  http://www7b.boulder.ibm.com/wsdd/products/

- DB2 Extenders

  http://www-3.ibm.com/software/data/db2/extenders/

- Bunker Hill

  http://www.bunkerhill.com/ei-0_files/WebHelp/2/index.htm

![](img/d95c931f4f3da4a6bd0ee55148fefad7_304_0.png)

![](img/d95c931f4f3da4a6bd0ee55148fefad7_304_1.png)

## Issuing commands to multiple database partitions
