
# JDBC 驱动程序类型

## 类型 1：JDBC-ODBC 桥接
此类型的 JDBC 驱动程序（如随 JDBC 提供的）使用本地安装的 ODBC 驱动管理器连接到数据库。如果你使用此驱动程序，你还需要配置你的 ODBC 驱动管理器，如第 10 章“Linux 开发工具目录”所述。你可能需要对你的 Java 安装添加一些额外配置，使其能够识别 ODBC 驱动管理器。

## 类型 2：混合驱动程序
这种驱动程序部分用 Java 编写，部分用 C 编写。这些驱动程序通常使用特定的客户端 API 连接数据库。

## 类型 3：使用网络协议的 100% Java
这种 JDBC 驱动程序是用 100% Java 编写的。但它并不直接连接到数据库服务器，而是连接到一个中间件服务器，该服务器作为类型 3 驱动程序和数据库之间的代理器。

## 类型 4：使用原生协议的 100% Java
这种类型的驱动程序是用 100% Java 编写的，并使用数据库服务器的网络协议直接连接到数据库服务器。这通常是客户端 API 的 Java 实现。它消除了对 C API 链接的需求。

表 11.2 列出了几种数据库的 JDBC 驱动程序信息，包括你可以在哪里找到 JDBC 驱动程序，以及你需要安装的 jar 文件名称。注意，随着版本号的变化，这些文件的名称也可能发生，请参考出的网站（或 Java JDBC 驱动列表）获取最新信息。

## 表 11.2 JDBC 驱动程序

| 数据库 | JAR 文件名 | 下载驱动 |
| --- | --- | --- |
| PostgreSQL | `postgresql.jar` `jdbc6.5-1.2.jar` (RedHat 6.1 包) | `www.postgresql.org`: 查看 PostgreSQL 分发版中的 `src/interfaces/jdbc/` 子目录。它也作为包 `postgresql-jdbc` 随 RedHat 6.1 提供。 |
| MySQL | `Mysql_comp.jar` `mysql_uncomp.jar` | `www.worldserver.com/mm.mysql` `www.mysql.com/Contrib/` |
| Mini SQL | `Msql-jdbc-1.rb1.jar` (JDK 1.1) `msql-jdbc-2-0bs5.jar` (JDK 1.2) | `www.imaginary.com/Java/Soul/` |
| Oracle | （分发为类文件） | `technet.oracle.com` |
| Sybase | `Jconn2.jar` | `www.sybase.com/java` |
| FreeTDS (Sybase 和 MS SQL Server) | `Freetds_jdbc.jar` | `www.fretds.org` |

某些 JDBC 驱动程序封装在 `jar`（Java 归档工具）中。文件非常简单，安装方法取决于你使用的 JDK 版本。然而，你应该参考随 JDBC 驱动程序一起的信息，获取可能需要的额外步骤的详情。关于如何正确设置 `CLSPATH` 的更多细节，请检查你正在使用的 JDK 版本的文档。

# 在 JDK 1.1.x 下安装 JDBC 驱动程序

在 JDK 1.1.x 版本下，安装通常涉及：

- 将 `jar` 文件复制到共享位置，例如 `/usr/local/classes`。
- 将 `jar` 文件的位置添加到你的 `CLSPATH` 环境变量中。

例如，随 RedHat 6.1 提供的 PostgreSQL JDBC 驱动程序名为 `jdbc6.5-1.2.jar`，位于目录 `/usr/lib/postgresql/`。要将此 `jar` 文件添加到你的 `CLSPATH` 中，你可以在启动脚本（如 `.bashrc` 或 `.bash_profile`）中放入以下语句之一。

在 `bash` shell 下：

```
export CLSPATH=$CLASSPATH:/usr/lib/postgresql/jdbc6.5-1.2.jar
```

在 `csh` shell 下：

```bash
if ($CLASPATH) then
    setenv CLASPATH \
        $(CLASPATH):/usr/lib/postgresql/jdbc6.5-1.2.jar
else
    setenv CLASPATH /usr/lib/postgresql/jdbc6.5-1.2.jar
endif
```

# 在 1.x 版本下安装 JDBC 驱动程序

在 JDK 1.x 版本下，安装通常涉及：

- 将 `jar` 文件复制到共享共享位置，例如 `/usr/local/classes`。
- 将 `jar` 文件的位置添加到你的 `CLSPATH` 环境变量中。

例如，随 RedHat 6.1 提供的 PostgreSQL JDBC 驱动程序名为 `jdbc6.5-1.2.jar`，位于目录 `/usr/lib/postgresql/`。要将此 `jar` 文件添加到你的 `CLSPATH` 中，你可以在启动脚本（如 `.bashrc` 或 `.bash_profile`）中放入以下语句之一。

在 `bash` shell 下：

```
export CLSPATH=$CLASSPATH:/usr/lib/postgresql/jdbc6.5-1.2.jar
```

# 运行示例程序

如果你想在阅读本章时运行一些示例程序，这里是每个程序配套的示例程序（可以在配套网站获取）：

- `ConnectDemo.java`。建立到数据库的连接，不做其他操作。
- `SendDemo.java`。向数据库发送 SQL 以创建表并向其中放入数据（如果表存在，则先删除）。
- `ResultSetDemo.java`。获取上一个程序中插入的数据。

这些程序与文中显示的类似，但增加了额外的处理和错误检查。要运行这些任何一个程序，使用以下命令调用：

`java -Djdbcbc.drivers=DRIVERCLASS PROGRAM URL PASS`

其中：

`PROGRAM`。程序名称，不带 `.java` 后缀。

`DRIVERCLASS`。你想要使用的 JDBC 驱动类名（参见表 11.2）。

`URL`。数据库服务器的 JDBC URL（参见表 11.2）。

`USER`。用户名。

`PASS`。密码。

例如，这在运行 PostgreSQL 服务器的同一台机器上运行应该是有效的：

```
java -Djdbcbc.drivers=postgresql.Driver ConnectDemo \
jdbcbc:postgresql:postgres ''
```

（注意：最后两个字符是单引号，而不是一个双引号）。

如果在连接时遇到问题：

- 使用 `javac` 或 `jikes` 重新编译类文件。这可能会显示你未注意到的配置错误，例如系统中缺少类。
- 确保你可以从其他程序连接到数据库服务器（参见第 9 章 SQL 监控）。
- 验证你使用的是正确的 JDBC 驱动类和 JDBC URL。
- 咨询你使用的 JDBC 驱动或数据库服务器的技术支持。最好的起点是表 11.2 列出的主页。

# 使用 JDBC

当你使用 JDBC 编写程序时，通常会执行以下操作：

1. 打开到数据库服务器的连接。
2. 向服务器发送 SQL 命令。
3. 处理响应 SQL 命令生成的任何结果集。

让我们详细查看这些步骤。在这个过程中，最复杂且容易出错的步骤是建立连接，部分是因为 JDBC 驱动程序对你使用的连接字符串语法非常敏感。其他问题（例如无法连接到数据库）可能是由于数据库配置问题引起的。某些数据库（如 Mini SQL）必须配置为接受远程连接（关于各种数据库服务器配置问题的讨论，请参见第 9 章）。

## 建立连接

为了与数据库建立连接，你的程序必须：

- 导入 JDBC 类。
- 在 Driver Manager 中注册至少一个 JDBC 驱动程序（`Driver`）。
- 使用 JDBC-URL、用户名和密码调用 Driver Manager 的 `getConnection()` 方法。

## 导入 JDBC 类

要导入 JDBC 类，请在程序中包含以下行：

```
import java.sql.*;
```

## 注册驱动程序

接下来，在你的应用程序中注册计划使用的所有驱动程序。你可以在命令行上注册它，也可以在程序中硬编码驱动程序名称。如果你在程序中硬编码了驱动程序名称，将需要修改源代码并重新编译以使用不同的驱动程序。

要在命令行上注册驱动程序，请使用 `-Djdbc.driver` 选项来指定驱动程序的类名。这必须出现在程序名之前。例如，如果你的程序名为 `Sample.java`，并且你想使用 PostgresQL 驱动程序，可以使用此命令运行它：

```
java -Djdbc.driver=postgresql.Driver Sample
```

请参见标题为“运行示例程序”的章节以获取此用法示例。所有驱动程序类名的列表请参见表 11.3。请记住，随着新版本的驱动及其变体的发布，这些名称可能会发生变化。请保留你的 JDBC 驱动文档或主页（参见表 11.2）以获取最新详情。

要在程序中硬编码驱动程序名称，你应该使用 `Class.forName("DRIVER_NAME")` 来注册驱动程序。以下代码显示了 PostgreSQL JDBC 驱动程序的示例。由于该语句可能会抛出异常，因此在代码中进行了捕获：

```
try {
  Class.forName("postgresql.Driver");
} catch (ClassNotFoundException e) {
  System.err.println(e.getMessage());
  System.exit(-1);
}
```

如此使用 `Class.forName()` 会运行驱动程序类中的静态初始化代码，并将驱动程序注册到驱动管理器中。表 11.3 显示了各种 JDBC 驱动程序的类名。

### 注意事项

如果你使用 `Class.forName(DRIVERNAME)` 且程序get“No suitable driver”（无合适的驱动程序）错误消息，尝试加上 `newInstance()`，如下：

```
Class.forName("postgresql.Driver").newInstance();
```

## 调用 getConnection()

现在驱动程序已注册到驱动管理器，你必须与驱动程序建立连接。为此，你必须要求 `DriverManager` 类创建一个连接对象。建立连接你需要提供三个变量：

`JDBC URL`。这是一个连接字符串，用于识别你想要连接的数据库服务器类型，并指定驱动程序支持的各种选项。

`用户名`。这是连接到数据库时使用的用户名。

`密码`。这是用户的密码。

表 11.3 JDBC 驱动程序类

| 数据库 | 驱动程序类 |
| :--- | :--- |
| PostgreSQL | `postgresql.Driver` |
| MySQL | `org.jdbc.mm.mysql.Driver` |
| Mini SQL | `com.imaginary.sql.MsqDriver` |
| Oracle | `oracle.jdbc.driver.OracleDriver` |
| Sybase | `com.sybase.jdbc2.SybDriver` |
| JDBC-ODBC Bridge | `sun.jdbc.odbc.JdbcOdbcDriver` |

表 11.4 某些 JDBC URL

| 数据库 | JDBC URL |
| :--- | :--- |
| PostgreSQL | `jdbc:postgresql:DATABASE`<br>`jdbc:postgresql://HOST/DATABASE`<br>`jdbc:postgresql://HOST:PORT/DATABASE` |
| MySQL | `jdbc:mysql:////DATABASE`<br>`jdbc:mysql://HOST/DATABASE`<br>`jdbc:mysql://HOST:PORT/DATABASE` |
| Mini SQL | `jdbc:msql:////HOST/DATABASE`<br>`jdbc:msql:////HOST:PORT/DATABASE` |
| Oracle | `jdbc:oracle:thin:SID`<br>`jdbc:oracle:thin:@HOST:PORT:SID` |
| Sybase | `jdbc:sybase:Tds:HOST:PORT`<br>`jdbc:sybase:Tds:HOST:PORT/DATABASE` (你可以在 `-sybase/interfaces` 中找到主机和端口号) |
| JDBC-ODBC Bridge | `jdbc:odbc:DSN` |

表 11.4 显示了各种驱动程序的基本 JDBC URL，其中：

`HOST` 是运行数据库服务器所在的主机名称。如果没有给出 host，大多数 JDBC 驱动程序会假设为 localhost。

`DATABASE` 是你连接时要使用的数据库名称（而不是数据库服务器名称）。关于数据库和数据库服务器之间区别的解释，请参见第 9 章标题为“数据库和数据库服务器有什么区别？”的章节。

`SID` 是 Oracle 系统标识符，可以在 `/etc/oratab` 中找到。这仅适用于 Oracle 数据库服务器。

`PORT` 是连接的 TCP/IP 端口。JDBC 驱动程序通常假设数据库服务器是用默认端口安装的，除非并非如此，否则你不应使用 PORT。

`DSN` 是 ODBC 数据源名称。你必须按照第 10 章所述，使用 ODBC 驱动管理器对其进行配置。

`getConnection()` 方法可能会抛出 `SQLException`，因此你必须使用 `try...catch` 结构来处理此异常。

让我们考虑一个示例，我们想要连接到一个名为 `database` 的数据库。为了建立此连接，你必须要求 `DriverManager` 类创建一个连接对象。为了建立连接你需要提供三个变量：

`JDBC URL`。这是一个连接字符串，用于识别你想要连接的数据库服务器类型，并指定驱动程序支持的各种选项。

```java
user = "manager";
pass = "";
```

# 远程服务器上的 PostgreSQL。在示例中，我们连接到运行在名为 `frobozz` 的主机上的 PostgreSQL 服务器上的 `library` 数据库。用户名为 `librarian`，没有密码：

```
url = "jdbc:postgresql://frobozz/library";
user = "librarian";
pass = "";
```

# 本地服务器上的 Oracle。此示例连接到本地 Oracle 服务器（通过 `orcl` SID 引用），用户为 `scott`，密码为 `tiger`：

```
url = "jdbc:oracle:thin:orcl"
user = "scott"
pass = "tiger";
```

### Sybase。与其他的 Sybase 工具和实用程序不同，Sybase JDBC 驱动不使用 `~sybase/interfaces` 来查找服务器名称。因此，你必须指定 Sybase 服务器的主机名和端口号。即使你尝试从运行 Sybase 服务器的同一台机器上进行连接，使用 `localhost` 也可能会遇到问题。

最好的办法是亲自查看 `~sybase/interfaces` 文件；如果你可以使用 `sql` 连接到这些条目之一，那么你应该能够使用 interfaces 文件中的主机名和端口号。以下是一个示例，它连接到运行在主机 `oscorb`（端口 `4100`）上的 Sybase 服务器上的 `bjepson_db`。用户名为 `bjepson`，密码为 `open_sesame`：

```
url = "jdbc:sybase:Tds:oscorb:4100/bjepson_db"
user = "bjepson"
pass = "open_sesame";
```

# 常见连接问题

如果你连接遇到困难，请检查以下内容：

- 错误的连接字符串。仔细检查你的 JDBC URL、末尾字符，或在不需要的地方使用了分隔符？请特别注意表 11.4，并咨询驱动程序附带的文档。
- 本地与远程访问。如果你尝试连接到远程服务器，该服务器是否允许远程连接？某些服务器默认只允许本地连接。你可能需要配置服务器以允许远程连接，或者专门授予特定远程主机的访问。详情请参阅第 9 章以及数据库服务器文档。

# 向服务器发送 SQL

建立与数据库服务器的连接后，你可以向它发送 SQL 语句。要向服务器发送 SQL：

创建一个 Statement 对象。要创建 Statement 对象，请使用 `Connection.createStatement()` 方法。如果发生错误，这将抛出 `SQLException`，因此你可能需要捕获它以防万一：

```java
Statement stmt = null;
try {
  stmt = conn.createStatement();
} catch (SQLException e) {
  System.err.println(e.getMessage());
  System.exit(-1);
}
```

调用 `executeUpdate()`。调用 Statement 对象的 `executeUpdate()` 方法（这也可能抛出 `SQLException`）：

```java
try {
  String sql = "INSERT INTO statement_demo " +
  "(name, id) VALUES('test', 100)";
  stmt.executeUpdate(sql);
} catch (SQLException e) {
  System.err.println(e.getMessage());
  System.exit(-1);
}
```

如果你想发送 SQL SELECT 语句或其他返回结果的 SQL 语句，请参见接下来的章节“处理结果集”（Process Result Sets）。
