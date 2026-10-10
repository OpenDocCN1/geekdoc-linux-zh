

# 5.2 配置环境

C/C++ 应用程序采用客户端-服务器架构，其中 C/C++ 应用程序作为客户端，DB2 作为服务器。客户端向服务器发送请求，服务器执行操作。C/C++ 应用程序可以是嵌入式 SQL 应用程序或 CLI/ODBC 应用程序。图 5.2 展示了 C/C++ 应用程序与 DB2 服务器交互的客户端-服务器架构。

![](img/5f6ba170efa3a607142589708531bef8_165_0.png)

**图 5.2 – C/C++ 应用程序访问 DB2 服务器**

图 5.2 展示了如何构建 C/C++ 应用程序以及如何访问 DB2 数据库。包含 SQL 语句的嵌入式 SQL 应用程序必须由 DB2 预编译器进行预编译。为了便于此预处理过程，应用程序中嵌入的每个 SQL 语句必须以关键字 `EXEC SQL` 开头，并以分号（;）结尾。

另一方面，CLI 或 ODBC 是嵌入式动态 SQL 的替代方案，但与嵌入式 SQL 不同，它不需要宿主变量或预编译器。应用程序可以针对来自不同供应商的多种数据库运行，这些供应商会提供自己的 ODBC 驱动程序。应用程序无需针对每个数据库进行编译。ODBC/CLI 应用程序的处理由 ODBC/CLI 驱动程序完成。应用程序在运行时使用过程调用连接数据库、发出 SQL 语句，并检索数据和状态信息。

我们将在后续章节中更详细地讨论上述每种方法。

在开始构建嵌入式 SQL C/C++ 应用程序或 ODBC/CLI 应用程序之前，您需要安装受支持的 C/C++ 编译器。对于嵌入式 SQL C/C++ 程序，您还需要预编译器；幸运的是，DB2 已包含该预编译器。

## 5.2.1 受支持的编译器

表 5.1 列出了在 32 位和 64 位平台上开发 DB2 数据库应用程序时受支持的 C/C++ 编译器。

| 操作系统 | 受支持的编译器 |
| --- | --- |
| AIX® | AIX 的 IBM XL C/C++ Enterprise Edition Version 7.0<br>AIX 的 IBM XL C/C++ Enterprise Edition Version 8.0<br>AIX 的 IBM XL C/C++ Enterprise Edition Version 9.0 |
| Linux | GNU/Linux gcc 版本 3.3 和 3.4<br>Intel C 编译器版本 9.1<br>Intel C 编译器版本 10.1 |
| Windows® | 用于 Windows 32 位应用程序的 Intel Proton 编译器，版本 9.0.021 或更高版本<br>Microsoft® Visual C++ .NET 或更高版本 |

**表 5.1 – 受支持的 C/C++ 编译器**

> **注意：** 此列表并非完整列表。有关受支持的 C/C++ 编译器版本的更多详细信息和最新信息，请参阅 http://publib.boulder.ibm.com/infocenter/db2luw/v9r7/topic/com.ibm.db2.luw.apdv.gs.doc/doc/r0023434.html 处的 DB2 9.7 信息中心以及 http://www.ibm.com/software/data/db2/udb/ad/ 处的 DB2 应用程序开发网站。

在本书中，我们使用 Microsoft Visual C++ 编译器（Windows）和 GNU/Linux gcc 编译器（Linux）。Microsoft Visual C++ 编译器是许可软件，随 Microsoft Visual Studio 提供。Visual Studio 的 Express 版本可以从 http://www.microsoft.com/express/Downloads/ 下载。GNU Linux gcc 编译器随 GNU 操作系统免费提供，但也可以从 http://gcc.gnu.org/ 下载。

## 5.2.2 配置 C/C++ 环境

要配置 C/C++ 环境，请遵循以下步骤：

- **1. 验证是否已安装受支持的 C/C++ 编译器**
  确保在受 DB2 Express-C 支持的平台上已安装受支持的 C/C++ 编译器。查看表 5.1 中的受支持编译器版本列表。
  在 Linux 上，要检查 C/C++ 编译器是否成功安装，请在 Linux shell 中执行以下命令：
  `which gcc`
  如果已安装编译器，屏幕上应显示 `/usr/bin/gcc`。

  在 Windows 上，如果使用 Microsoft Visual C++ 编译器，请执行 `c1` 命令。图 5.3 显示了执行此命令后的输出。

  ![](img/5f6ba170efa3a607142589708531bef8_167_0.png)

  **图 5.3 – c1 命令的输出**

  如果使用 Intel 编译器，请执行 `icl` 或 `ec1` 命令。图 5.4 显示了执行此命令后的输出。

  ![](img/5f6ba170efa3a607142589708531bef8_167_1.png)

  **图 5.4 – icl 命令的输出**

- **2. 验证您的 DB2 安装是否包含所需的库文件和头文件**
  安装 DB2 后，验证开发 C/C++ 程序所需的静态库、共享库和头文件是否存在。

  在 Linux 上，可以通过进入 DB2 安装目录并检查 `lib32` 和 `lib64` 目录来完成此操作。例如，如果 DB2 安装目录位于 $HOME，则 32 位库位置将在 $HOME/sqllib/lib32，而 64 位库位置将在 $HOME/sqllib/lib64。

  在 Windows 上，静态库位于 `<DB2 安装目录>\lib`。图 5.5 显示了静态库的位置。此处 DB2 安装目录为 `C:\Program Files\SQLLIB`。

  ![](img/5f6ba170efa3a607142589708531bef8_168_0.png)

- **3. 验证 Windows 环境**
  在 Windows 开发机器上，确保 **INCLUDE** 环境变量包含 `%DB2PATH%\include`，且该目录位于任何 Microsoft Platform SDK include 目录之前。如果情况并非如此，请遵循以下选项之一：
  - 通过执行以下命令在命令提示符处修改 **INCLUDE** 变量：`set INCLUDE=%DB2PATH%\include;%INCLUDE%`（这仅对当前窗口有效）
  - 如果要使此更改永久生效，请通过右键单击 *我的电脑* -> *属性* -> *环境变量* 来定位 Windows 环境变量，并在 **INCLUDE** 变量中添加 `%DB2PATH%\include`。

  如果使用 Visual Studio 进行开发，必须确保 **INCLUDE** 环境变量将 `%DB2PATH%\include` 作为第一个目录包含在内。为此，您需要使用以下步骤更新编译器的环境变量：
  1. 通过依次前往 *Program Files* -> *Microsoft Visual Studio .NET* -> *Visual Studio .NET Tools* -> *Visual Studio .NET Command Prompt* 打开 Visual Studio 命令提示符的快捷方式。
  2. 在 Visual Studio 命令提示符窗口中，运行 **db2cmd.exe** 以打开 DB2 命令窗口。
  3. 在 DB2 命令窗口中，按如下方式设置您的 `INCLUDE` 路径：
     `set INCLUDE=%DB2PATH%\INCLUDE;%INCLUDE%`

  图 5.7 显示了上述步骤：

  ![](img/5f6ba170efa3a607142589708531bef8_169_0.png)
  ![](img/5f6ba170efa3a607142589708531bef8_169_1.png)

  **图 5.7 – 配置 Windows 环境**

  现在，您可以在已正确设置 DB2 环境和 C/C++ 环境的 DB2 CLP 窗口中构建您的应用程序。

# 5.3 开发带嵌入式 SQL 的 C/C++ 应用程序

本节讨论开发带嵌入式 SQL 的 C/C++ 应用程序所需的步骤。

## 5.3.1 源文件扩展名

嵌入式 C/C++ SQL 程序的 C/C++ 源文件需要 DB2 预编译器能够识别的适当文件扩展名。表 5.2 列出了预编译器所需的 C/C++ 源文件扩展名。

| 平台 | C 源文件 | C++ 源文件 |
| --- | --- | --- |
| Linux | .sqc | .sqC |
| Windows | .sqc | .sqx |

**表 5.2 – 受支持的源文件扩展名**

## 5.3.2 C/C++ 中的 SQL 数据类型

为了在应用程序和数据库之间通信，使用正确的数据类型映射（宿主变量的 C/C++ 数据类型与 SQL 数据类型之间）非常重要。当预编译器找到宿主变量的声明时，它会确定适当的 SQL 数据类型。表 5.3 列出了 C/C++ 中支持的一些 SQL 数据类型。

| SQL 列类型 | C 和 C/C++ 数据类型 | SQL 列类型描述 |
| --- | --- | --- |
| SMALLINT | Short | 16 位有符号整数 |
| INTEGER | sqlint32 | 32 位有符号整数 |
| DOUBLE | Double | 双精度浮点数 |
| CHAR(n) | char[n+1] 其中 n 足够容纳数据 1<=n<=254 | 固定长度，以 null 结尾的字符串 |
| VARCHAR(n) | char[n+1] 其中 n 足够容纳数据 1<=n<=254 | 以 null 结尾的变长字符串 |
| DATE | char[11] | 以 null 结尾的字符形式 |
| TIME | char[9] | 以 null 结尾的字符形式 |

**表 5.3 – C/C++ 中支持的 SQL 数据类型**

> **注意：** 此列表并非完整列表。完整的映射列表可在以下位置找到：  
> http://publib.boulder.ibm.com/infocenter/db2luw/v9r7/index.jsp?topic=com.ibm.db2.luw.adv.embed.doc/doc/0006090.html

