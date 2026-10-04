

# Oracle 攻击与防御 • 第13 章

- http://oracleserver/pls/dadname/http.print?cbuf=<script>alert('Doh!')</script> 跨站脚本攻击此前已被广泛讨论并构成了潜在威胁；因此，应通过将 http 包添加到 `wdbsvr.app` 文件的排除项中，禁止对该包的访问。

# OracleJSP

本节涵盖了 Java 节点页面 (JSP) 和结构化查询语言 Java 页面 (SQLSP) 应用程序，它们都由同一个组件 OracleJSP 进行分发。

# JSP 翻译文件

当 Web 客户端请求 JSP 页面时，页面本身需要翻译成 Java 应用程序。此过程需要创建一个 .java 源文件，然后将其即时编译为 .class 文件。这些文件被留存在文件系统中，并可以通过 Web 访问。默认情况下，没有任何机制可以阻止匿名用户访问 java 源文件，该文件包含业务/应用程序逻辑，并且通常使用用户 ID 和密码连接到数据库服务器。系统会创建三个翻译文件。当请求名为 "/foo.jsp" 的页面时，将生成以下翻译文件：

$foo$__jsp_StaticText.class
$foo.class
$foo.java

这些翻译文件存储在 "/_pages" Web 目录中。如果 foo.jsp 存在于名为 bar 的子目录中，即 /bar/foo.jsp，则会在 _pages 目录下创建一个 _bar 目录并在其中放置三个文件。关于具体命名规范的详情，请阅读 http://downloadwest.oracle.com/otndoc/oracle9/901_doc/java.901/a90208/trandepl.htm。为了防止攻击者获取这些翻译文件，有必要对 httpd.conf 文件进行修改。添加以下条目：

```
<Location /_pages>
Order deny,allow
Deny from all
</Location>
```

![](img/729efc56f204a2ebffb8295c3a2dfdfb_731_0.png)

# 第13 章 + Oracle 攻击与防御

注意如果 JSP 页面存储在别名目录中（即不是 htdocs 的子目录），则需要添加以下条目，其中 dirname 是别目录的名称：

```
<Location /dirname/_pages>
Order deny,allow
Deny from all
</Location>
```

# JSP Global.jsa 访问

与 JSP 翻译文件可以直接访问一样，JSP 应用程序的 globals.jsa 文件也可以被访问。该文件包含全局范围的信息，并且通常包含用户 ID 和密码。如果 JSP 应用程序使用了 globals.jsa 文件，可以通过在 httpd conf 文件中添加以下条目来对其进行保护：

```
<Files ~"globals.jsa">
Order allow,deny
Deny from all
</Files>
```

# JSP SQL 注入

与每个应用程序环境一样，在将客户端输入传递给逻辑之前，有必要对其进行“安全化处理”。特别是对于 SQL 注入，来自客户端输入的字符字符串中的单引号应该双倍化或删除；客户端提供的数字型数据在将其传入 SQL 查询之前，应对对其进行验证，以确保其确实是数字。尽管 Oracle 不像微软 SQL Server 那样支持批量处理多个 SQL 查询，但由于 UNION 和嵌套 SELECT，Oracle 仍然受到 SQL 注入的影响。

# JSP 物理路径映射

当请求不存在的 JSP 页面时，会抛出 Java FileNotFoundException，并且包含文件物理路径的错误信息将会出现。尽管这种信息泄露并不严重，但建议您创建一个标准的 JSP 错误页面来保护这些细节。

# XSQL

XSQL 配置文件位于 $/xsql/lib/XSQLConfig.xml。该配置文件包含数据库主机名、用户 ID 和密码等信息。由于该文件存在于虚拟目录中，它通常可以被下载并查看内容。如果此文档已受保护，且对其的请求触发了 "403 Forbidden" 响应，仍然可以通过使用 XSQLServlet 请求文件来获取访问：http://acleserver/servlet/oracle.xml.xsql.XSQLServlet/xsql/lib/XSQLConfig.xml，这不可避免地绕过了保护。

# XSQL 注入

取决于 XSQL 文件的编写方式，可能对数据库服务器执行任意查询。以下是一个 XSQL 文件的示例，该文件从表中提取数据并将其转换为 XML 数据：

```
<xml version="1.0"?>
<xsql:query connection="demo" xmlns="urn:oracle-xsql">
SELECT * FROM USERS_TABLE WHERE NAME = '(@name)'
</xsql:query>
```

如果将其保存为 file.xsql，则对该资源的请求将类似于：
http://acleserver/file.xsql?name=foobar

结果将以 XML 格式返回给浏览器。然而，通过在 name 参数末尾插入单引号，可以运行第二个查询：
http://acleserver/file.xsql?name=foobar' union select * from foo-

此安全漏洞的根源与其他 SQL 注入原因相同——客户端输入在插入 SQL 查询 之前未对其进行验证。在这种情况下，验证应通过调用在 Java Server Page 中清理用户输入的库来完成。

此示例 XSQL 页面可用于任意 SQL 查询，并应该被删除：

```
http://acleserver/xsql/java/xsql/demo/adhocsql/query.xsql?stylesheet=no.xsl&sql=select+*from+sys.dba_users
```

# XSQL 样式表

早期版本的 XSQL 解析器容易受到任意 XML 执行攻击。通过指定存在于另一个网站样式表，Web 服务器将连接到远程服务器，下载 XML 并执行其中包含的任何内容。这个问题由 Georgi Guninski 发现。

XML 实际上是一种数据格式，这可能有点让人困惑。实际发生的是 SQL 命令可以作为 XML 数据发送。

# SOAP 部署

简单对象访问协议 (SOAP) 是一种用于交换结构化信息的轻量级基于 XML 的协议。Oracle Apache 安装的 SOAP 应用程序可以通过 Web 访问。部署 SOAP 应用程序应仅限于管理员。要确定您的应用程序是否可管理，请求以下内容：

```
http://acleserver/servlet/soaprouter
```

如果存在 soaprouter，说明服务器未经过适当安全防护。通过在  文件中添加以下元素来部署 urn:service-manager 和 urn:provider-manager 服务：。

# SOAP 配置文件

soapConfig.xml 文件应该受到保护。默认情况下不受保护。可以通过直接访问或使用 XSQLServlet 访问：

- http://acleserver/soapdocs/webapps/soap/WEB-INF/config/soapConfig.xml
- http://acleserver/servlet/oracle.xml.xsql.XSQLServlet/...

# 默认暴露的 Web 服务

与 Oracle 安装的许多服务（如动态监控服务）可以被匿名用户远程访问。允许远程访问这些服务允许攻击者收集应用程序信息，这在策划攻击时可能价值。应编辑 httpd.conf 文件以防止访问以下内容：

# 动态监控服务

- http://acleserver/dms0
- http://acleserver/dms/DMSump
- http://acleserver/servlet/DMSump
- http://acleserver/servlet/Spy
- http://acleserver/soap/servlet/Spy
- http://acleserver/dms/AggreSpy

# Oracle Java Manager

- http://acleserver/oprocmgr-status
- http://acleserver/oproccmgr-service（当前损坏）

# Perl 别名

在某些 Oracle Application Server 版本中，perl 虚拟目录映射到与 /cgi 目录相同的物理位置。然而，perl 被标记为 Apache 别名而非脚本别名。因此，可以通过 /perl 目录访问 /cgi-bin 中任何脚本的源代码。可以通过修改 httpd.conf 文件来修复，将 /perl 别名转换为脚本别名。如果未使用 perl，可以安全地删除。

# 危险示例

与 Oracle Application Server 安装的许多示例页面可能被滥用来破坏系统安全。例如，/oracleserver/demo/email/sendmail.jsp 可用于发送任意电子邮件。其他页面容易受到 SQL 注入攻击，其他页面则泄露信息，例如 http://oracleserver/demo/basic/info.jsp 会泄露环境变量。其他泄露额外信息的页面如下：

