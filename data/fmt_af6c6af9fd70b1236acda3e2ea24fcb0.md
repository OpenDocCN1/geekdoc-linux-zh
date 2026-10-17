
- `http://www.ibm.com/software/webservers/httpsservers/`

## 5.1.2.2 缓存与动态页面

默认情况下，大多数 Web 浏览器和代理服务器都会缓存 Web 页面。对于 JSP 文件、HTML 文件和小程序，这些 Web 页面是动态生成的，并且可能会每次尝试访问时发生变化。

为了防止缓存从而访问新生成的动态数据，我们可以在 Java Server Page（JSP）或 servlet 中添加以下代码，防止 Web 浏览器缓存 JSP/SHTML 文件和 servlet：

```
response.setHeader("Pragma", "no-cache");
response.setDateHeader("Expires", "0");
response.setHeader("Cache-Control", "no-cache")
```

使用以下代码防止代理服务器共享缓存页面：

```
response.setHeader("Cache-Control", "private");
```

这两个头部可以结合使用以防止缓存。

## 5.2 Linux 下的产品局限性

Linux 上的 WebSphere 版本落后于其他平台（如 Windows NT 或 AIX）的可用版本。这对于我们利用许多让电子商务开发变得更简单的新功能（例如 `RequestDispatcher` 类）造成了相当限制。关于该类的更全面讨论，请参见第 142 页第 5.2.1 节“RequestDispatcher 类”。

在我们的项目中，我们使用 CORBA 访问 Lotus Domino 数据库。也可以通过 JDBC 访问 Lotus Domino 服务器。然而，JDBC 的 Lotus Domino 驱动仅适用于有限的平台，Linux 并不在。关于 Lotus 此项功能的更全面讨论，请参见第 143 页第 5.2.2 节“Domino 的 JDBC 连接”。

## 5.2.1 RequestDispatcher 类

`RequestDispatcher` 类的基本用法是将当前请求传递给另一个程序（servlet 或 JSP）。Request Dispatcher 有两个主要方法可以包含另一个程序的响应或将程序的请求转发到另一个程序。

- 包含另一个程序的响应需要使用方法：

```
aRequestDispatcher.include(request, response)
```

如果我们想从当前 servlet 调用另一个 servlet， 然后在调用该其他 servlet 后在当前 servlet 中执行更多处理，就会使用此方法。

- 将请求转发到另一个程序需要使用方法：

```
aRequestDispatcher.forward(request, response)
```

我们将此用于转发到另一个 servlet，然后允许此新 servlet 直接将响应返回给客户端。

遗憾的是，`RequestDispatcher` 类仅在 Java SDK 2.1 API 的 `javax.servlet` 类中可用（在 WebSphere 3.02 中支持并扩展）。在我们的 servlet 中，为了处于仅支持和扩展 SDK 2.0 的 WebSphere 2.03 环境，我们被迫使用 `com.sun.servlet.http` 包中已弃用的 `callPage` 方法。这也解释了为什么在 servlet `AccessUsersf` 的 Java 代码中使用了 `HttpServletResponse` 和 `HttpServletRequest` 对象。

参阅 URL `http://novocode.doc/servlet-essentials/chapter0.html` 获取 `RequestDispatcher` 类的良好教程。参阅 URL `http://java.sun.com` 获取各种 Java API 规范的官方规范和文档。

## 5.2.2 Domino 的 JDBC 连接

JDBC 是一种对象接口，允许 Java应用程序、applets 和代理使用 SQL 在数据库系统中检索和操作数据。该接口允许单个应用程序通过标准协议连接到许多不同类型的数据库。

Lotus JDBC 驱动实现了 JDBC 1.0 规范。它可以适用于 Windows 95、Windows 98 和 Windows NT 4.0 操作系统。这是一个 Type 2 驱动，由 Java 类和非编译代码组成。目前不适用于任何其他平台（包括 Linux）。

Domino JDBC 驱动允许 Java 程序使用 JDBC 访问 Domino/Notes 数据库。Java 可以与任何支持 JDBC 的报告工具配合访问 Domino 数据库。Java 程序员可以使用启用 Java Database Connectivity (JDBC) 标准的应用工具像访问任何关系型数据库一样访问 Lotus Domino 数据库。在 Domino R5 上运行此 JDBC 驱动时，Java 程序员可以创建访问 Domino 数据的 Servlet。Lotus Domino JDBC 驱动通过产生镜像关系模型的结果集，使 Domino 数据库像 SQL 工具或应用程序接口的另一个关系型后端源。应用程序还可以对 Domino 数据与关系型数据库（如 Oracle、Sybase 或 DB/2）的数据执行 SQL Join 操作。

产品特性包括：

- 通过 Java 标准访问 Domino 4.5x、4.6x 和 R5x 数据库。
- 兼容 Netscape Communicator 4.05 及更高版本。
- 兼容带有 service pack 1 的 Microsoft Internet Explorer 4.01。
- 提供签名和未签名版本，为创建使用 JDBC 的 Java applets 提供最大的灵活性。
- 准备好应对千禧年问题，因此它可以正确读取和解释两位年份（mm/dd/yy）和四位年份（mm/dd/yyyy）格式的日期。
- 通过了 IBM Visual Age for Java Version 2.0、IBMSphere Application Server 2.0、Lotus eSuite DevPack 1.5、Borland JBuilder 3 Professional、Jinfonet Software JReport Professional 1.3、EnterpriseSoft Enterprise Reports 3.0、Symantec Virtual Database Development Edition 3.0 以及 NetObjects BeanBuilder 1.0 测试。
- 用于高性能 Web 使用的多线程。
- 通过负载均衡和故障转移支持集群服务器的高可用性。
- 文档提供了四个示例源码（`.java` 文件）。
- Lotus Domino JDBC 驱动是 Lotus 开放标准和数据库服务访问性的又一步，使用户无论企业配置或工具选择如何都能将 Domino 集成到任何电子商务解决方案。

JDBC API 包含在 JDK v1.1 及更高版本中。在下载和安装 Lotus Domino JDBC 驱动时会提供 Lotus Domino JDBC 所需的 DLL 连接 Domino/Notes 数据库（即上述的非 Java 编译代码）。

- 如果您的 Java 程序运行在客户端计算机上，则必须安装 客户端。
- 如果您的 Java 应用程序运行在未运行 Domino 的服务器上，则必须安装并配置 客户端以连接 Domino 服务器。
- 如果您的 Java 应用程序运行在 Domino 服务器上（例如在 R5 上作为 Servlet 运行），则 Notes DLL 和 API 已经存在，无需安装。

# Notes API 知识

| 描述 |
| :--- |
| 您不需要 Notes API。Lotus Domino JDBC 驱动屏蔽了这些，并让您能够使用 JDBC API 连接到 Domino 并使用 SQL 查询、更新和处理 Domino 数据 |

参阅 URL `http://www.lotus.com` 获取有关 Lotus Domino JDBC 驱动的更多信息。

144 使用 WebSphere、DB2 和 Domino 的 Linux 托管

## 附录 A. 创建 USERSTUF 表的 SQL 脚本

本附录提供了项目中创建 DB2 表的源文件列表。

### A.1 USERINFO 表

```
create table userinfo (
first_name varchar(20) not null,
last_name varchar(20) not null,
email_address varchar(50) not null,
date_joined date not null,
birth_date date not null,
address varchar(200) not null,
username varchar(20) not null,
primary key (username)
);
```

### A.2 USERVERIFY 表

```
create table userverify (
username varchar(20) not null,
password varchar(20) not null,
primary key (username)
);
```

### A.3 USERPROFILE 表

```
create table userprofile (
username varchar(20) not null,
s000 char(1),
ettfinity char(1),
ncf char(1),
nw char(1),
s390 char(1),
r6000 char(1),
scalable char(1),
vm char(1),
vse char(1),
windows char(1),
other char(1),
primary key (username)
);
```

### A.4 USERORDERs 表

```
create table userorders (
  username varchar(20) not null,
  order_timestamp timestamp not null,
  product_id varchar(20) not null,
  order_id int not null,
  primary key (order_id)
);
```

## 附录 B. 与 DB2相关的 Java 代码

本附录提供了 DB2 相关的 Java 代码列表。

### B.1 Java servlet TestDB2

```java
package penguins.access.db2;

import java.sql.*;
import javax.servlet.http.*;
import javax.servlet.*;
public class TestDB2 extends HttpServlet {
    try {
        Class.forName("com.ibm.db2.jdbc.app.DB2Driver");
    } catch (Exception e) {
        e.printStackTrace();
    }

    public TestDB2() {
        super();
    }

    public void doGet(HttpServletRequest req, HttpServletResponse res) {
        String url = "jdbc:db2:sample";
        String uid = "db2inst";
        String pwd = "db2password";
        Connection conn = DriverManager.getConnection(url, uid, pwd);
        ServletOutputStream out = res.getOutputStream();
        out.setContentType("text/html");
        out.print("<html><head>TestDB2</head><body><p>");
        out.print("select * from department");
        Statement stmt = conn.createStatement();
        ResultSet rs = stmt.executeQuery("select * from department");
        while (rs.next()) {
            out.print(rs.getString(1) + ":" + rs.getString(2) + "<p>");
        }
        out.print("</body></html>");
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```

### B.2 Java servlet AccessUserstuff
