
| 类型 4 | 原生协议 pure-java 驱动程序。 | 这是最灵活的 JDBC API。此驱动程序将 JDBC 调用直接转换为 DB2 使用的网络协议。这允许从客户端机器直接调用 DB2 服务器，而无需安装 DB2 客户端。 | 是 |

**表 4.1 - JDBC 驱动程序类型**

虽然有几种类型的 JDBC 驱动程序，但类型 2 和类型 4 驱动程序是最受欢迎的且性能最佳；因此，在 DB2 9.7 中，为了支持这两种类型，已经取消了对其余类型的支持。类型 2 驱动程序需要在运行 Java 应用程序的机器上安装 DB2 客户端。类型 2 驱动程序使用 DB2 客户端建立与数据库的通信，如图 4.2 所示。

![](img/5f6ba170efa3a607142589708531bef8_126_0.png)

**图 4.2 - 使用 JDBC 类型 2 驱动程序的 Java 应用程序**

类型 4 是一种纯 Java 客户端，因此不需要 DB2 客户端，但驱动程序必须安装在运行 JDBC 应用程序的机器上。图 4.3 说明了使用类型 4 驱动程序的 JDBC 应用程序。

![](img/5f6ba170efa3a607142589708531bef8_127_0.png)

*表 4.2* 提供了有关 DB2 JDBC 和 SQLJ 驱动程序的更多详细信息。

| 驱动程序类型 | 驱动程序名称 | 打包形式 | 支持的 JDBC 规范 | 所需的最低 Java SDK 级别 |

| :--- | :--- | :--- | :--- | :--- |

| 类型 2 | Linux、UNIX 和 Windows 的 DB2 JDBC 类型 2 驱动程序 (*已弃用*) | `db2java.zip` | JDBC 1.2 和 JDBC 2.0 | 1.4.2 |

| 类型 2 和类型 4 | IBM Data Server Driver for JDBC and SQLJ | `db2jcc.jar` 和 `sqlj.zip` | 符合 JDBC 3.0 | 1.4.2 |

| | | `db2jcc4.jar` 和 `sqlj4.zip` | JDBC 4.0 及更早版本 | 6 |

**表 4.2 - DB2 JDBC 和 SQLJ 驱动程序**

* * “已弃用”意味着它仍受支持，但不再增强*

正如 *表 4.2* 所示，类型 2 提供了两种不同的驱动程序；然而，打包为 `db2java.zip` 的 Linux、UNIX 和 Windows 的 DB2 JDBC 类型 2 驱动程序已弃用。

打包为 `db2jcc.jar`（`com.ibm.db2.jcc`）的 IBM Data Server Driver for JDBC and SQLJ 包括对类型 2 和类型 4 驱动程序两者的支持。驱动程序的选择取决于在 Java 程序中连接数据库时使用的语法：如果连接字符串中包含主机名或 IP 地址以及端口，则使用类型 4；否则，使用类型 2。这将在本章的后续部分中详细讨论。IBM Data Server Driver for JDBC and SQLJ 已优化以访问所有平台上的所有 DB2 服务器，包括大型机。

当您安装 DB2 服务器、DB2 客户端或 IBM Data Server Driver for JDBC and SQLJ 时，符合 JDBC 3.0 的 `db2jcc.jar` 和 `sqlj.zip` 文件会自动添加到您的 **CLASSPATH** 中。如果您希望使用 JDBC 4.0 规范，请确保将 **CLASSPATH** 中的 `db2jcc.jar` 和 `sqlj.zip` 分别替换为 `db2jcc4.jar` 和 `sqlj4.zip`。

**注意：**

如果您是 Java 编程语言以及 JVM、JRE 或 JDK 概念的初学者，请回顾本书系列中免费电子书 *Getting Started with Java*。

## 4.3 JDBC 编程

开发 JDBC 程序包括以下步骤：

-   1. 使用 JDBC 类型 2 或类型 4 连接到数据库

-   2. 执行 SQL 语句

-   3. 接收结果

-   4. 处理 SQL 错误和警告

-   5. 关闭连接

我们将在后续章节中更详细地讨论这些步骤。*图 4.4* 总结了 JDBC 程序中使用的步骤、接口、类和方法。这些内容也会在后续章节中更详细地讨论。

![](img/5f6ba170efa3a607142589708531bef8_128_0.png)

图 4.4 - JDBC 编程的步骤、对象和方法

**注意：**

本节中使用的几个示例和图表取自 IBM 红皮书 *DB2 Express-C: The Developer Handbook for XML, PHP, C/C++, Java, and .NET* (SG24-7301-00)。有关更多信息，请参阅本书的资源部分。

### 4.3.1 连接到 DB2 数据库

本节将展示如何使用 JDBC 类型 2 和 JDBC 类型 4 连接到数据库。让我们检查以下 *清单 4.1* 中展示的关于使用 JDBC 类型 2 进行连接的代码片段。

```java
import java.sql.*;

class myprg {
    public static void main (String argv[]){
        try {
            (1)  Connection con = null;
            (2)  Class.forName("com.ibm.db2.jcc.DB2Driver");
            (3)  String url = "jdbc:db2:SAMPLE";
                 if (argv.length == 2) {
                     String userID = argv[0];
                     String passwd = argv[1];
            (4)  con = DriverManager.getConnection(url,userID,passwd);
                 }
                 else
                 {throw new Exception
                     ("\n Usage: java myprg userID password\n");
                 }
        ...
        }
    }
}
```

**清单 4.1 - 使用 JDBC 类型 2 连接到 DB2 数据库**

让我们回顾 *清单 4.1* 中显示的每个项目：

-   (1) 该语句导入了 **java.sql** 包，其中包含 JDBC 核心 API。

-   (2) 该语句从 IBM Data Server Driver for JDBC and SQLJ (*db2jcc.jar/db2jcc4.jar/sqlj.zip/sqlj4.zip*) 加载驱动程序类。**forName** 方法接受一个字符串参数，其值是实现了 **java.sql** 包中定义的接口的类的名称。在这种情况下，类名为 "com.ibm.db2.jcc.DB2Driver"。如果您展开 *db2jcc.jar* 文件，在 Windows 上您会看到：

```
C:\Program Files\IBM\SQLLIB\java\db2jcc\com.ibm.db2\jcc\DB2Driver.class
```

对于已弃用的 Linux、UNIX 和 Windows 平台的 DB2 JDBC 类型 2 驱动程序，在 `forName` 方法中使用的类名应为 `"COM.ibm.db2.jdbc.app.DB2Driver"`。如果您在 Windows 上解压 `db2java.zip`，您会看到：

```
C:\Program Files\IBM\SQLLIB\java\db2java\COM.ibm.db2\jdbc\app\DB2Driver.class
```

-   (3) 在此行中，我们初始化 URL 并选择连接到 **SAMPLE** 数据库。在 URL 语法中，我们没有包含主机名或端口号；因此，这意味着使用的是类型 2。类型 2 需要安装 DB2 客户端，并使用它来配置与 **SAMPLE** 数据库的连接。
