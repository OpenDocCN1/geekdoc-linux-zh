
```java
import java.sql.*;
Connection con;
Statement stmt;

try {
    con = DriverManager.getConnection("jdbc:mysql://...");
    stmt = con.createStatement();

} catch (SQLException ex) {
    System.out.println("SQLException: " + ex.getMessage());
    System.out.println("SQLState: " + ex.getSQLState());
    System.out.println("VendorErr: " + ex.getErrorCode());
    ex.printStackTrace();
    return;
}
```

尽管 JDBC 抽象了 DBMS 操作，但它与它们并不遥远。某些 SQL 知识是至关重要的。JDBC 可用于发布模式定义和数据操语句。接下来，我们使用一个 SQL 定义语句来创建表。由于我们正在对数据库进行操作，因此使用 `java.sql.executeUpdate()` 方法将 SQL 语句传递给 DBMS。此方法还用于填充表或更改表中的某行数据：

```java
// 在连接的数据库中创建 location 表
stmt.executeUpdate("CREATE TABLE location " +
    "(id int not null auto_increment, primary key (id)," +
    "city varchar(40) not null," +
    "state char(2) not null," +
    "zip char(10) not null," +
    "area char(3))");

// 在 location 表中插入行
stmt.executeUpdate("INSERT INTO location values (" +
    "0, 'Spokane', 'WA', '98207')");
} catch (SQLException ex) {
    System.out.println("SQLException: " + ex.getMessage());
}
```

DBMS 使用的大大部分是在数据库上执行查询。查询按行请求结果表中的列。请求使用数据库游标枚举这些行。JDBC 将结果表封装在 `Statement.executeQuery()` 方法调用返回的 `java.sql.ResultSet` 实例中：

```java
// 从 location 表请求邮政编码
ResultSet rs = stmt.executeQuery("SELECT city, state FROM location " +
    "WHERE zip = '98207'");

while(rs.next()) {
    System.out.println(rs.getString("city") + 
        ", " + rs.getString("state"));
}

// 释放
rs.close();
} catch (SQLException ex) {
    System.out.println("SQLException: " + ex.getMessage());
}
```

每个连接和打开的语句都应该关闭以释放资源。最后关闭连接，如下：

```java
try {
    stmt = conn.createStatement();
    // ...
} catch (SQLException ex) {
    System.out.println("SQLException: " + ex.getMessage());
}
```

JDBC 是底层的，因为它是 DBMS API 的抽象。有一些持久化框架将持久数据抽象为业务数据对象。Crosslogic 的 Strata Framework™提供了在 JDBC 之上映射持久数据的选择。Sun 的 Enterprise JavaBeans 规范提供了允许使用 DBMS 作为存储的实体 bean。在底层，通常是 JDBC 提供了到 DBMS 的平台中性路径。

## 消息队列

面向消息的中间件（MOM）经常用于胶接分离的分布式应用程序。消息队列异步支持获取和放入消息。它是应用程序的电子邮件。这种松耦合克服了网络框架与应用程序之间的阻抗匹配。例如，运行消息队列客户端的笔记本销售人员可以将订单输入到 IBM 主机 DB2 数据库。或者，Windows XP 笔记本向 Red Linux™ 服务器输入订单，这符合本书的主题。

图 6–7 显示了场景的功能单元。客户端销售人员在白天从客户处输入订单。Windows XP 笔记本上的本地 DB2 数据库持有产品目录。当销售人员从电子表单提交订单时，它会被组合并放入本地消息队列。客户端应用程序可能是使用 JMS 访问消息队列并使用 JDBC 访问本地数据库的 Java 程序。

在一天结束时，销售人员使用如 IBM WebSphere Messaging（也称为 MQSeries）连接到 Linux 服务器。当 Windows XP 笔记本的队列为空时，服务器执行消息获取操作。服务器端处理每个订单，并通过消息队列系统传回确认记录。如果拨号中断，确认记录仍在服务器队列中，直到客户端在后续连接期间获取消息。

使用消息队列我们获得了什么？连接的异步特性允许在不连续的情况下执行客户端-服务器操作具有灵活性。消息中间件还允许

### 订单输入客户端

![](img/9e81145387d1e3c67216814bd87285fe_192_0.png)

### 订单输入服务器

![](img/9e81145387d1e3c67216814bd87285fe_192_1.png)

图 6-7 订单输入应用程序

这使我们能够以简单的方式异步互连应用程序，而无需复杂的协议。我们的应用程序端只需要知道如何打开队列并执行由 MOM 语言绑定（如 JMS）定义的 `get` 或 `put` 操作即可。当然，连接和队列操作伴随着各种设置和选项，但用户代码看到的只是简单的 `get/put` 协议。

消息队列的另一个用途是保证消息的递送。想象一下同一个销售人员在笔记本电脑断开连接时输入订单。当他重新连接时，队列中的进行中交易将完成。此时，他会收到任何缺货通知。

Java 在此场景中处于什么位置？并不意外的是，主要的队列供应商都有 Java 连接器。它们运行在 Windows 或 Linux 上，IBM 的 MQSeries 是 MOM 市场的主要参与者，而 Java 是 IBM 软件策略的核心。但 Java 程序能够与其他供应商进行交互吗？

JMS 登场了。Sun 的 JMS 是一组 Java 接口，描述了消息提供者架构。如果你不是为它的接口编写提供者，那么从 Sun 下载 JMS 将让你失望的。像 IBM 这样主要的供应商已经编写了实现 JMS 接口的提供者。因此，使用 JMS 必须获取供应商的产品。好消息是，JMS 促进了实现 JMS 接口的 MOM 供应商之间的互操作性。当然，它适用于 Java 或 Linux 客户端。

## 目录和命名服务

当我们说 EJB 通过 JNDI 提供者进行注册和定位时，我们首先提到了 JNDI。和 JMS 一样，JNDI 是提供者接口。我们必须指定一个提供者来使用它。J2SE 提供了几个标准提供者：LDAP、COS 命名（CORBA name）和 RMI 注册。还有独立的“LDAP Booster Pack”、NIS 和文件系统提供者。在编写本书时，已经提供了域名系统（DNS）服务技术。这使得 Java 通过 JNDI 访问 DNS。此外还有目录标记语言（DSML）技术，允许 Java 访问 DSML。因此，JNDI 通过其提供者为 Windows 和 Linux 开放了许多目录和命名服务。我们将在第 15 章详细讨论这一主题。

## XML

扩展标记语言（XML）是一种用于创建描述任意复杂数据的标记语言的标记语言。有很多关于使用 XML 在不同进程和应用程序之间映射数据的文献。与 Java 一样，XML 的接受部分源于其基于标准。IBM 有许多基于 Java 的新兴技术。每种技术可以在 Web 上找到或托管在 `http://www.ibm.com/`。XML 通过选择的方法进行解析。第一种方法使用文档对象模型（DOM）解析器，它在内存驻留树中构建 XML 文档的数据结构。使用一个 API 来遍历树并修改元素和属性。该 API 也可以用于构建树。还可以使用导出函数将树序列化为 XML 文本流。第二类解析器是 XML 简单访问（SAX）解析器。SAX 解析器是处理海量结构化数据（如 GUI 等事件驱动型应用程序）的良好选择。至少有一个 DOM 解析器——Apache Xerces 实际上是使用 SAX 解析器构建其 DOM 的。程序员编写处理器并重写事件方法。这些包括：

- 文档的开始和结束
- 元素的开始和结束
- 属性的开始和结束
- 检查或捕获 XML 文档的字符数据

可以使用类型声明（DTD）来描述文档的合法结构。另一种方法是它描述文档的语法或模式（schema）。DTD 是继承自 XML 父级标准标记语言（SGML）的独立语言。DTD 的一个缺点是它仍然是语言。另一个问题是它对 XML 语法可以描述的结构是有限的。为什么没有一种描述 XML 结构的 XML 语言呢？存在这种 XML 语言称为 XML schema。Xerces 编辑器会将 DTD 转换为 XML schema。

某些 DOM 解析器或 SAX 解析器是验证解析器。这意味着如果文档不遵守底层结构，它们将通过给出解析器错误来强制 DTD 或 XML schema。其他解析器是非验证的。只有当文档不符合 XML 规则时，它们才会给出语法错误。

IBM 基于 Java 的解析器格式化了基于 Apache Xerces 的 XML 解析器的代码。该解析器实际上包含四个解析器：都是一个 SAX 解析器和一个 DOM 解析器，且其中任何一个都可以被设置为针对 DTD 或 schema 进行验证。DTD 或 schema 可以嵌入文档中，也可以从外部引用。该基于 Java 的编辑器允许用户创建和编辑符合 DTD 或 XML schema 的 XML 文档。它可以用于将 DTD 转换为 XML schema。由于它是基于 Java 的，因此它可以运行在 Windows 或 Linux 上。

XML 的主要用途是允许应用程序交换数据。不同的应用程序不会使用相同的数据结构或格式。称为可扩展样式语言（XSL）的 XML 技术利用 XML 创建从一个文档模式转换为另一个模式的 XML 映射。XML 的一个组件 XML 转换（XSLT）利用另一种语法 XPath 能够访问 XML 数据结构中的任何节点，而不需要显式编程。因此，映射到输入 XML 文档的 XSL 映射会产生转换后的 XML 输出。XSLT 的常见应用是根据 XML 描述的数据生成 HTML。一个常用的 Java XSL 转换工具是 Apache 的 Xalan。

## 网络上的互操作性

ment。因此，命名空间支持允许我们混合名称而无需担心发生冲突。让我们通过应用以下变换，将这些数据转换为 HTML 文档？

```xml
<?xml version="1.0"?>
<html version="1.0"
xmlns="http://www.w3.org/TR/xhtmlml/strict"
xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
<head><title>Inventory</title></head>
<body bgcolor="darkblue" fgcolor="white" text="white">
<h1>Profound Bargains</h1>
<xsl:for-each select="ITEMS/PRODUCT">
<xsl:sort select="BRAND" />
<table border="1" cellpadding="2">
<tbody>
<tr><th align="right">Manufacturer:</th</th>
<td><td width="200"xsl:class="class"><xsl:value-of select="BRAND"/></td</td></tr>
<tr><th align="right">Class:</th</th>
<td><xsl:value-of select="CLASS/text()"/></td</td></tr>
<tr><th align="right">Type:</th</th>
<td><xsl:value-of select="CLASS/TYPE"/></td</td></tr>
<tr><th align="right">Name:</th</th>
<td><xsl:value-of select="NAME"/></td</td></tr>
<tr><th align="right">Speed:</th</th>
<td><xsl:value-of select="FEATURES/SPEED"/></td</td>
<td><![CDATA[ - ]]></td>
<td><xsl:value-of select="FEATURES/SPEED/Units"/></td</td></tr>
<tr><th align="right">Quality:</th</th>
<td><xsl:value-of select="FEATURES/QUALITY/Units"/></td</td></tr>
<tr><th align="right">Retail:</th</th>
<td><xsl:value-of select="PRICE/RETAIL"/></td</td></tr>
<tr><th align="right">Units:</th</th>
<td><xsl:value-of select="PRICE/@Units"/></td</td></tr>
<tr><th align="right">Wholesale:</th</th>
<td><xsl:value-of select="PRICE/WHOLESALE"/></td</td></tr>
<tr><th align="right"></th></th>
<td><xsl:value-of select="PRICE/@Units"/></td</td></tr>
<tr><th align="right">Weight:</th</th>
<td><xsl:value-of select="=""/></td</td>
<td><xsl:value-of select="WEIGHT/@Units"/></td</td></tr>
</tbody>
</table>
</xsl:for-each>
</body>
</html>
```

# 180 第 6 章 编程：Java、网络与 Web

```html
<table>
<br/>
< xsl:for-each>
<hr>
<body>
</html>
```

该变换遍历文档以查找项目中的产品。注意 `for-each` 循环和 `sort` 规范。XSL 表达式是定义在 XML 命名空间中的一种语言。这里使用 XPath 表达式来查找项目以填充 HTML 表格单元格。我们使用 Apache 的基于 Java 的 Xalan 对 XML 文档进行变换，如下：

```bash
java org.apache.xalan.xslt.Process -IN product.xml -XSL product.xsl -OUT product.html
```

结果部分如图 6-8 所示。任何文档，甚至 Apache Xalan 工具本身，都没有绑定到特定平台。此变换在 Windows 或 Linux 上运行完全相同。输入文档和映射文档并不特定于任何平台。这是 Java 在数据转换和渲染领域促进互操作性的主要范例。从 XML 到 HTML 的转换是 XML 的常见用法。Java 经常用于此类操作，因为它独立于服务器或客户端平台。这意味着基于 Java 的包可能在 Windows 和 Linux 之间互操作。Java 在开发互联网和内网应用程序方面起着作用。

## 互联网、内网

Java 通常用于 Web 编程和互联网编程。Java 用于服务器端的应用程序，以及在浏览器中下载并运行的 Applet。Servlet、JSP 和 EJB 是用于构建基于 Java 的应用程序的技术。我们将介绍这些技术与 Windows 和 Red Hat 的关系。内网解决方案的网络编程问题导致。

## Web 编程

大多数解决方案的网络编程属于 Web 编程范畴。这并不容易。使用最新工具生成。90 年代的二层模型已扩展到三层或 n 层模型。基本概念是，三层模型中的客户端变成了表示层。数据层（或持久层）是后端数据存储。应用模型位于中间层。这并不完全清晰。应用程序的部分可能位于任何层。图 6-8。

## 客户端脚本

Web 应用的一部分可能作为脚本位于 HTML 页面中。微软最初将其称为动态 HTML（或 DHTML）。今天，由于浏览器有不同的 DOM 版本，可移植性编程变得困难。Web 管理员必须通过重跳来适应互联网上不同类型的浏览器。这使得解决方案变得更容易。DOM 脚本可以执行客户端级验证或高级效果。如果 HTML 通过对象类生成的（例如 Java Servlet），那么此类类可能包含客户端。大量的浏览器脚本会导致混乱的应用程序。JavaScript 通常用于包括 Windows 和 Red Hat Linux 在内的平台。我们可以使用客户端脚本来实现 Web 应用程序的验证或高级效果，并将重量逻辑放在应用服务器上。

## Java Applet
