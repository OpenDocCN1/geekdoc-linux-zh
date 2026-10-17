
与每个应用程序环境一样，在将客户端输入传递给逻辑之前，有必要对其进行“安全化处理”。特别是对于 SQL 注入，来自客户端输入的字符字符串中的单引号应该双倍化或删除；客户端提供的数字型数据在将其传入 SQL 查询之前，应对对其进行验证，以确保其确实是数字。尽管 Oracle 不像微软 SQL Server 那样支持批量处理多个 SQL 查询，但由于 `UNION` 和嵌套 `SELECT`，Oracle 仍然受到 SQL 注入的影响。

# JSP 物理路径映射

当请求不存在的 JSP 页面时，会抛出 `Java FileNotFoundException`，并且包含文件物理路径的错误信息将会出现。尽管这种信息泄露并不严重，但建议您创建一个标准的 JSP 错误页面来保护这些细节。

# XSQL

`XSQL` 配置文件位于 `$/xsql/lib/XSQLConfig.xml`。该配置文件包含数据库主机名、用户 ID 和密码等信息。由于该文件存在于虚拟目录中，它通常可以被下载并查看内容。如果此文档已受保护，且对其的请求触发了 `403 Forbidden` 响应，仍然可以通过使用 `XSQLServlet` 请求文件来获取访问：`http://acleserver/servlet/oracle.xml.xsql.XSQLServlet/xsql/lib/XSQLConfig.xml`，这不可避免地绕过了保护。

# XSQL 注入

取决于 XSQL 文件的编写方式，可能对数据库服务器执行任意查询。以下是一个 XSQL 文件的示例，该文件从表中提取数据并将其转换为 XML 数据：

```
<xml version="1.0"?>
<xsql:query connection="demo" xmlns="urn:oracle-xsql">
SELECT * FROM USERS_TABLE WHERE NAME = '(@name)'
</xsql:query>
```

如果将其保存为 `file.xsql`，则对该资源的请求将类似于：

`http://acleserver/file.xsql?name=foobar`

结果将以 XML 格式返回给浏览器。然而，通过在 `name` 参数末尾插入单引号，可以运行第二个查询：

`http://acleserver/file.xsql?name=foobar' union select * from foo-`

此安全漏洞的根源与其他 SQL 注入原因相同——客户端输入在插入 SQL 查询 之前未对其进行验证。在这种情况下，验证应通过调用在 Java Server Page 中清理用户输入的库来完成。

此示例 XSQL 页面可用于任意 SQL 查询，并应该被删除：

```
http://acleserver/xsql/java/xsql/demo/adhocsql/query.xsql?stylesheet=no.xsl&sql=select+*from+sys.dba_users
```

# XSQL 样式表

早期版本的 XSQL 解析器容易受到任意 XML 执行攻击。通过指定存在于另一个网站样式表，Web 服务器将连接到远程服务器，下载 XML 并执行其中包含的任何内容。这个问题由 Georgi Guninski 发现。

XML 实际上是一种数据格式，这可能有点让人困惑。实际发生的是 SQL 命令可以作为 XML 数据发送。

# SOAP 部署

简单对象访问协议 `SOAP` 是一种用于交换结构化信息的轻量级基于 XML 的协议。Oracle Apache 安装的 SOAP 应用程序可以通过 Web 访问。部署 SOAP 应用程序应仅限于管理员。要确定您的应用程序是否可管理，请求以下内容：

```
http://acleserver/servlet/soaprouter
```

如果存在 `soaprouter`，说明服务器未经过适当安全防护。通过在  文件中添加以下元素来部署 `urn:service-manager` 和 `urn:provider-manager` 服务：。

# SOAP 配置文件

`soapConfig.xml` 文件应该受到保护。默认情况下不受保护。可以通过直接访问或使用 `XSQLServlet` 访问：

- `http://acleserver/soapdocs/webapps/soap/WEB-INF/config/soapConfig.xml`
- `http://acleserver/servlet/oracle.xml.xsql.XSQLServlet/...`

# 默认暴露的 Web 服务

与 Oracle 安装的许多服务（如动态监控服务）可以被匿名用户远程访问。允许远程访问这些服务允许攻击者收集应用程序信息，这在策划攻击时可能价值。应编辑 `httpd.conf` 文件以防止访问以下内容：

# 动态监控服务

- `http://acleserver/dms0`
- `http://acleserver/dms/DMSump`
- `http://acleserver/servlet/DMSump`
- `http://acleserver/servlet/Spy`
- `http://acleserver/soap/servlet/Spy`
- `http://acleserver/dms/AggreSpy`

# Oracle Java Manager

- `http://acleserver/oprocmgr-status`
- `http://acleserver/oproccmgr-service`（当前损坏）

# Perl 别名

在某些 Oracle Application Server 版本中，`perl` 虚拟目录映射到与 `/cgi` 目录相同的物理位置。然而，`perl` 被标记为 Apache 别名而非脚本别名。因此，可以通过 `/perl` 目录访问 `/cgi-bin` 中任何脚本的源代码。可以通过修改 `httpd.conf` 文件来修复，将 `/perl` 别名转换为脚本别名。如果未使用 `perl`，可以安全地删除。

# 危险示例

与 Oracle Application Server 安装的许多示例页面可能被滥用来破坏系统安全。例如，`/oracleserver/demo/email/sendmail.jsp` 可用于发送任意电子邮件。其他页面容易受到 SQL 注入攻击，其他页面则泄露信息，例如 `http://oracleserver/demo/basic/info.jsp` 会泄露环境变量。其他泄露额外信息的页面如下：

- `/cgi-bin/printenv`
- `/fcgi-bin/echo`
- `/fcgi-bin/echo2`

在将 Web 服务器引入生产环境之前，应当删除所有示例页面和脚本。

## 防御 Oracle

保护 Oracle 服务器在初看之下可能是一项艰巨的任务。由于 Oracle 的很多部分内容没有文档说明，在 Oracle 被认为是“安全的”之前，还需要很长一段时间。这需要进行全面的调查；在本章的研究过程中，发现了超过 22 多个漏洞，其中一些已经进行过讨论。新的漏洞将不断不断被发现，你所能做的最好的工作就是采用最佳实践来降低风险，这些实践将在本节中讨论。

## 保护监听器 Listener

如果你已经读过“攻击 Oracle 服务器”章节，你应该意识到，在保护 Oracle 方面，第一也是最重要的一步是保护监听器。许多针对监听器的攻击不需要用户 ID 和密码，因此这将是试图入侵 Oracle 数据库服务器的攻击者的首选目标。

## 有效节点检查 Valid Node Checking

可以通过主机名或 IP 地址限制对监听器（从而对 Oracle）的访问。虽然基于此类准的验证机制在任何意义上都不是万无一的（因为熟练的攻击者可以绕过它），但对于保护服务器非常有帮助。该过程被称为 `有效节点检查`，通过编辑 `sqlnet.ora` 文件来设置。在 Oracle8i 及之前的版本中，该文件位于 `$ORACLE_HOME\network\admin` 目录下，而你需要编辑的是 `protocol.ora` 文件。

添加以下行：

```
tcp.validnode_checking = YES
```

这将开启此保护机制。可以允许主机访问或特定拒绝访问。对于你希望允许访问的每个主机（例如 DBA 的工作站以及需要访问的 Web 应用服务器等机器），请添加类似下面的条目：

要拒绝某些主机的访问，请添加类似下面的条目：

```
tcp.excluded_nodes = (10.1.1.99)
```

如果某台机器表现得“麻烦”（也就是说，你的用户正在攻击你的服务器！），这可能很有用。不否认，如果攻击者通过拒绝服务攻击“干掉”了一台受邀机器，她可以更改 IP 地址并获得访问。人们可能会想，那么这样做值得吗？嗯，答案在于“深度防御”策略。通过在攻击者面前设置障碍，他们需要更长时间才能入侵，并希望在你察觉到异常发生之前。

## 设置监听器密码
