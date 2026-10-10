
嵌入式 SQL C/C++ 应用的一个优势在于，ODBC 应用可以针对来自不同供应商的多种数据库运行，而无需针对每个数据库编译代码。要运行已编译的 ODBC/CLI 应用，您只需在运行该应用的机器上安装供应商提供的 ODBC/CLI 驱动程序及其客户端即可。应用程序在运行时使用过程调用连接数据库、发出 SQL 语句以及检索数据和状态信息。

## 5.5.1 CLI/ODBC 应用的额外环境设置

除了 5.2 节中讨论的内容外，若要让 ODBC/CLI 应用访问 DB2 数据库，您还需要执行以下步骤：

### 5.5.1.1 Linux

- 安装 ODBC 驱动程序管理器。
- 在 `.odbc.ini` 文件中将 DB2 数据库注册为 ODBC 数据源。例如，若要注册 SAMPLE 数据库，`.odbc.ini` 文件必须包含以下行：
  `SAMPLE=IBM DB2 ODBC DRIVER`
- 将 `LD_LIBRARY_PATH` 环境变量设置为 `libodbc.so`。
- 按如下方式设置 `ODBCINI` 环境变量：
  `ODBCINI=/opt/odbc/system_odbc.ini; export ODBCINI`

### 5.5.1.2 Windows

- 确保已安装 Microsoft ODBC 驱动程序管理器和 DB2 CLI/ODBC 驱动程序。若要验证机器上存在这两个组件，请遵循以下步骤：
  - 双击控制面板中的 Microsoft ODBC 数据源图标，或从命令行运行 `odbcad32.exe` 命令。
  - 单击“驱动程序”选项卡，并检查列表中是否显示了 IBM DB2 ODBC DRIVER - `<DB2_Copy_Name>`。*图 5.24* 展示了输出结果。如果 ODBC 驱动程序管理器或 IBM DB2 CLI/ODBC 驱动程序不在列表中，您需要从 [http://www-01.ibm.com/support/docview.wss?rs=4020&uid=swg2i385217](http://www-01.ibm.com/support/docview.wss?rs=4020&uid=swg2i385217) 下载用于 ODBC 和 CLI 的 IBM 数据服务器驱动程序，并通过将 `clidriver` 文件夹复制到 `<DB2 安装目录>\sqllib` 进行安装。

![](img/5f6ba170efa3a607142589708531bef8_192_0.png)

**图 5.24 – 添加 ODBC 数据源**

- 下一步是配置 ODBC 数据源。请遵循以下步骤设置数据源。
  - 在 ODBC 数据源管理面板（如上图 5.24 所示）中，单击“系统 DSN”选项卡。
  - 单击“添加”，选择 IBM DB2 ODBC 驱动程序，然后单击“完成”以创建新数据源。
  - 在弹出的窗口中，为数据源名称输入任意名称，在此示例中我们将使用 sample，然后选择数据库 SAMPLE 并单击“添加”按钮以注册此数据库。
- 您也可以使用以下命令从 DB2 命令窗口或 Linux shell 中列出当前数据源，以检查 DB2 数据库是否已注册：

```bash
db2 list system odbc data sources
```

图 5.25 展示了上述命令的输出结果。您可以看到数据源 SAMPLE 已添加在列表中。

![](img/5f6ba170efa3a607142589708531bef8_193_0.png)

**图 5.25 – 添加 ODBC 数据源**

- 使用 ODBC 数据源管理器的替代方法是通过以下命令注册数据库：

```bash
db2 catalog system odbc data source sample
```

## 5.5.2 句柄

ODBC/CLI 句柄是指向由 ODBC/CLI 分配和管理的对象的变量。简单来说，句柄是一个指向变量的指针，用于在程序的不同部分之间传递该变量的引用。在 ODBC/CLI 中有四种类型的句柄：

- **环境句柄 (SQL_HANDLE_ENV)**
  环境句柄指的是一个对象，它包含有关应用程序全局状态、属性或连接的信息。在可以分配连接句柄之前，必须先分配环境句柄。

- **连接句柄 (SQL_HANDLE_DBC)**
  连接句柄指的是一个对象，它包含有关与特定数据库的连接的信息。对于每个数据库，都必须分配一个独立的连接句柄。在可以分配语句句柄之前，必须先分配连接句柄。

- **语句句柄 (SQL_HANDLE_STMT)**
  语句句柄指的是一个对象，它包含有关单个 SQL 语句执行的信息。在执行 SQL 语句之前，必须分配语句句柄并将其与连接句柄关联。

- **描述符句柄 (SQL_HANDLE_DESC)**
  描述符句柄指的是一个对象，它包含有关结果集中的列以及 SQL 语句中动态参数的信息。

*图 5.26 取自 IBM 红皮书 DB2 Express-C：XML、PHP、C/C++、Java 和 .NET 开发者手册 [5]，展示了不同句柄之间的关系。*

![](img/5f6ba170efa3a607142589708531bef8_194_0.png)

**图 5.26 – CLI 句柄**

## 5.5.3 开发 ODBC/CLI 应用的步骤

图 5.27 展示了开发 ODBC/CLI 应用所需的步骤。

![](img/5f6ba170efa3a607142589708531bef8_194_1.png)

**图 5.27 – ODBC/CLI 应用所需的步骤**

*图 5.27* 中所示的步骤将在以下各节中更详细地描述。

### 5.5.3.1 包含头文件

若要开始使用 CLI 开发应用程序，您需要包含 `sqlecli.h` 头文件，该文件包含开发 CLI 应用所需的 CLI 常量、函数原型和数据结构。清单 5.13 列出了 CLI/ODBC 应用所需的头文件。

```c
/* Include header files */
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <sqlecli.h>
```
*清单 5.13 - CLI 应用所需的头文件*

### 5.5.3.2 分配环境句柄

可以使用 `SQLAllocHandle` API 分配不同的句柄。`SQLAllocHandle()` 是一个通用函数，用于分配环境、连接、语句或描述符句柄。

> **注意：**
> 此函数取代了已弃用的函数 `SQLAllocConnect()`、`SQLAllocEnv()` 和 `SQLAllocStmt()`。有关 CLI 和 ODBC 函数的完整列表，请查阅此链接 http://public.boulder.ibm.com/infocenter/db2luw/v9r7/topic/com.ibm.db2.luw.apdv.cli.doc/doc/r0000553.html

清单 5.14 展示了 `SQLAllocHandle` API 的语法

```c
SQLRETURN SQLAllocHandle(
             SQLSMALLINT    HandleType,
             SQLHANDLE      InputHandle,
             SQLHANDLE      *OutputHandlePtr);
```
*清单 5.14 - `SQLAllocHandle` 函数的语法*

函数 `SQLAllocHandle` 接受句柄类型（环境、连接、语句或描述符）、输入句柄和输出句柄作为参数。要分配环境句柄，`HandleType` 的值必须为 `SQL_HANDLE_ENV`。如果句柄类型是 `SQL_HANDLE_ENV`，则 `InputHandle` 的值将为 `SQL_NULL_HANDLE`。`OutputHandlePtr` 将是一个指向缓冲区的指针，其中将返回新分配的数据结构的句柄。句柄分配后，`SQLAllocHandle` 返回以下任一具有自解释意义的返回代码：

- `SQL_SUCCESS`
- `SQL_SUCCESS_WITH_INFO`
- `SQL_INVALID_HANDLE`
- `SQL_ERROR`

让我们看一个示例。*清单 5.15* 展示了环境句柄的分配。

```c
/* allocate an environment handle */
(1) rc = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, pHenv);
(2) if (rc != SQL_SUCCESS)
    {
        printf("\n\nERROR while allocating environment handle.\n");
        funcRc = 1;
        exit (1);
    }
    printf("\n\nAllocate environment handle successfully.");
```
*清单 5.15 – 使用 SQLAllocHandle 函数分配环境句柄*

在上述清单中：

- 1. 此语句使用 `SQLAllocHandle` API 分配环境句柄，并返回指向 `pHenv` 的指针。
- 2. 此语句检查分配是否成功。

### 5.5.3.3 连接到数据库

成功分配环境句柄后，下一步是使用 `SQLConnect()` 连接到数据库。在连接到数据库之前，您需要分配一个连接句柄。可以通过使用 `SQLAllocHandle` API 并指定句柄类型为 `SQL_HANDLE_DBC` 来分配连接句柄。`InputHandle` 的值将是环境句柄变量的指针。*清单 5.16* 展示了 `SQLConnect` 的语法，*清单 5.17* 提供了使用 `SQLAllocHandle` 分配连接句柄并使用 `SQLConnect` 连接到数据库的示例。

```c
SQLRETURN SQLConnect ( ConnectionHandle, /* hdbc */
                    SQLCHAR *ServerName, /* szDSN */
                    SQLSMALLINT ServerNameLength,
                    SQLCHAR *UserName, /* szUID */
                    SQLSMALLINT UserNameLength,
                    SQLCHAR *Authentication, /* szAuthStr */
                    SQLSMALLINT AuthLength,
                    SQLCHAR *Output = NULL,
                    SQLSMALLINT *OutputLength = NULL);
```
*清单 5.16 – `SQLConnect` 函数的语法*

```c
(1) rc = SQLAllocHandle(SQL_HANDLE_DBC, pHenv, &pHdbc);
(2) rc = SQLConnect(pHdbc, "SAMPLE", SQL_NTS, "user", SQL_NTS, "password", SQL_NTS);
(3) if (rc != SQL_SUCCESS && rc != SQL_SUCCESS_WITH_INFO)
    {
        printf("\n\nERROR while connecting to database.\n");
        funcRc = 1;
        exit (1);
    }
    printf("\n\nConnect to database successfully.");
```
*清单 5.17 – 分配连接句柄并连接数据库*

在上述清单中：

- 1. 此语句使用 `SQLAllocHandle` API 分配连接句柄，并返回指向 `pHdbc` 的指针。
- 2. 此语句使用 `SQLConnect` API 连接到数据库。
- 3. 此语句检查连接是否成功。

