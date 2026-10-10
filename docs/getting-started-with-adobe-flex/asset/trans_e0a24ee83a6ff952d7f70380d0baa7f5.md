
| 命令 | 描述 |
|---|---|
| `update dbm cfg using <parameter_name> <value>` | 更新 dbm cfg 参数的值 |

**表 B.3 - 用于操作 dbm cfg 的命令**

- **数据库配置文件（db cfg）** 包含影响特定数据库的参数。*表 B.4* 列出了一些用于管理 db cfg 的常用命令。

| 命令 | 描述 |
|---|---|
| `get db cfg for <database_name>` | 检索指定数据库的 db cfg 信息 |
| `update db cfg for <database_name> using <parameter_name> <value>` | 更新 db cfg 参数的值 |

**表 B.4 - 用于操作 db cfg 的命令**

- **DB2 概要文件注册表变量** 包含可能因平台而异的参数，这些参数可以全局设置（影响所有实例）或在实例级别设置（影响特定实例）。*表 B.5* 列出了一些用于操作 DB2 概要文件注册表的常用命令。

| 命令 | 描述 |
|---|---|
| `db2set -all` | 列出所有已设置的 DB2 概要文件注册表变量 |
| `db2set <parameter>==<value>` | 将给定参数设置为指定值 |

**表 B.5 - 用于操作 DB2 概要文件注册表的命令**

## B.7 连接数据库

如果数据库是本地的，即位于执行数据库操作的同一系统上；在创建数据库时，连接设置会自动完成。只需发出 `connect to database_name` 语句即可连接到数据库。

如果数据库是远程的，设置数据库连接的最简单方法是使用配置助手（Configuration Assistant）GUI 工具，按以下步骤操作：

1. 从希望连接数据库的系统启动配置助手。启动此工具时，请在 Windows 命令提示符或 Linux shell 中使用命令 `db2ca`。*图 B.9* 展示了配置助手。

![](img/c4119654311ebf24679359ca130a5ee6_222_0.png)

图 B.9 - DB2 配置助手

2. 在配置助手中，点击 *Selected -> Add database using Wizard* 菜单。

3. 在 *Select how you want to set up a connection*（选择如何设置连接）窗口中，如果网络较小且没有太多集线器，可以使用 *Search the network*（搜索网络）。如果知道运行 DB2 的服务器名称，请选择 *Known systems*（已知系统）并一直向下钻取直到找到要连接的数据库。使用默认值继续向导操作。如果不知道系统名称，请选择 *Other systems (Search the network)*（其他系统（搜索网络））。请注意，如果网络很大，这可能需要较长时间。

4. 如果 *Search the network*（搜索网络）不起作用，请返回 *Select how you want to set up a connection*（选择如何设置连接）窗口，选择 *Manually configure a connection to a database*（手动配置到数据库的连接）。选择 *TCP/IP* 并点击 *next*（下一步）。输入 DB2 服务器所在的 *host name*（主机名）或 *IP address*（IP 地址）。输入 *service name*（服务名）或 *port number*（端口号）。

5. 继续向导提示，保持默认值。

6. 设置完成后，会弹出一个窗口询问是否要测试连接。也可以在设置完成后，右键点击数据库并选择 *Test Connection*（测试连接）来测试连接。

## B.8 基本示例程序

根据所使用的编程语言不同，连接 DB2 数据库并执行操作所需的语法也不同。以下是连接数据库并检索一条记录的基本示例程序的链接。建议您先下载本节中的所有示例程序（从 ftp://ftp.software.ibm.com/software/data/db2/udb/db2express/samples.zip）：

CLI 程序
[http://www.ibm.com/developerworks/db2/library/techarticle/dm-0401chong/index.html#scenario1](http://www.ibm.com/developerworks/db2/library/techarticle/dm-0401chong/index.html#scenario1)

ODBC 程序
[http://www.ibm.com/developerworks/db2/library/techarticle/dm-0401chong/index.html#scenario2](http://www.ibm.com/developerworks/db2/library/techarticle/dm-0401chong/index.html#scenario2)

带有嵌入式 SQL 的 C 程序
[http://www.ibm.com/developerworks/db2/library/techarticle/dm-0401chong/index.html#scenario3](http://www.ibm.com/developerworks/db2/library/techarticle/dm-0401chong/index.html#scenario3)

使用 Type 2 Universal (JCC) 驱动程序的 JDBC 程序
[http://www.ibm.com/developerworks/db2/library/techarticle/dm-0401chong/index.html#scenario6](http://www.ibm.com/developerworks/db2/library/techarticle/dm-0401chong/index.html#scenario6)

使用 Type 4 Universal (JCC) 驱动程序的 JDBC 程序
[http://www.ibm.com/developerworks/db2/library/techarticle/dm-0401chong/index.html#scenario8](http://www.ibm.com/developerworks/db2/library/techarticle/dm-0401chong/index.html#scenario8)

使用 IBM DB2 的 IBM OLE DB 提供程序 (IBMADb2) 的 Visual Basic 和 C++ ADO 程序
[http://www.ibm.com/developerworks/db2/library/techarticle/dm-0402chong2/index.html#scenario1](http://www.ibm.com/developerworks/db2/library/techarticle/dm-0402chong2/index.html#scenario1)

使用 Microsoft OLE DB 提供程序用于 ODBC (MSDASQL) 的 Visual Basic 和 C++ ADO 程序
[http://www.ibm.com/developerworks/db2/library/techarticle/dm-0402chong2/index.html#scenario2](http://www.ibm.com/developerworks/db2/library/techarticle/dm-0402chong2/index.html#scenario2)

使用 IBM DB2 .NET 数据提供程序的 Visual Basic 和 C# ADO.Net
[http://www.ibm.com/developerworks/db2/library/techarticle/dm-0402chong2/index.html#scenario3](http://www.ibm.com/developerworks/db2/library/techarticle/dm-0402chong2/index.html#scenario3)

使用 Microsoft OLE DB .NET 数据提供程序的 Visual Basic 和 C# ADO.Net
[http://www.ibm.com/developerworks/db2/library/techarticle/dm-0402chong2/index.html#scenario4](http://www.ibm.com/developerworks/db2/library/techarticle/dm-0402chong2/index.html#scenario4)

使用 Microsoft ODBC .NET 数据提供程序的 Visual Basic 和 C# ADO.Net
[http://www.ibm.com/developerworks/db2/library/techarticle/dm-0402chong2/index.html#scenario5](http://www.ibm.com/developerworks/db2/library/techarticle/dm-0402chong2/index.html#scenario5)

## B.9 DB2 文档

DB2 信息中心提供最新的在线 DB2 文档。DB2 信息中心是一个 Web 应用程序。您可以在线访问 DB2 信息中心 (http://publib.boulder.ibm.com/infocenter/db2luw/v9r7/index.jsp)，或者将 DB2 信息中心下载并安装到您的本地计算机。在线 DB2 信息中心的链接以及可下载版本可以在 http://www.ibm.com/software/data/db2/9/download.html?S_TACT=download&S_CMP=exp csite 处获取

## 参考文献

- [1] Adobe Flex 开发者中心 - <http://www.adobe.com/devnet/flex/>
- [2] Flex 开发者社区网站 - <http://flex.org>
- [3] IBM 按需网站，<http://www.ibm.com/ondemand>
- [4] SARACCO, C. <em>Understanding pureXML</em>，developerWorks 文章，2006 <http://www.ibm.com/developerworks/articles/saracco1>

# 资源

## 网站

### Flex

1. Flex 搜索：[http://flexxsearch.org](http://flexxsearch.org)
   这是一个面向社区的定制 Flex 搜索引擎
2. Flex 编码者：[http://www.adobe.com/go/flexcoders](http://www.adobe.com/go/flexcoders)
   flexcoders 邮件列表面向软件开发者
3. Flex 搜索：[http://flexxsearch.org](http://flexxsearch.org)：
   这是一个面向社区的定制 Flex 搜索引擎
4. Flex 组件开发：[http://tech.groups.yahoo.com/group/flexcomponents](http://tech.groups.yahoo.com/group/flexcomponents)
5. Flex 支持论坛：
   [http://www.adobe.com/cfusion/webforums/forum/index.cfm?forumid=60](http://www.adobe.com/cfusion/webforums/forum/index.cfm?forumid=60)
6. Flex 组件 – [http://www.adobe.com/go/flexcomponents](http://www.adobe.com/go/flexcomponents)
7. Flex Builder 3 Adobe 论坛
   [http://www.adobe.com/cfusion/webforums/forum/categories.cfm?forumid=72&catid=651&entercat=y](http://www.adobe.com/cfusion/webforums/forum/categories.cfm?forumid=72&catid=651&entercat=y)
8. Flex 团队博客
   [http://blogs.adobe.com/flex/](http://blogs.adobe.com/flex/) 这是 Adobe Flex 团队的官方博客。
9. Mike Morearty 的博客
   [http://www.morearty.com/blog/](http://www.morearty.com/blog/)
   Mike 是 Flex Builder 调试部分背后的核心人物。他的博客让您了解 Flex 世界的最新动态。
10. Chet Haase 的博客：[http://graphics-geek.blogspot.com/](http://graphics-geek.blogspot.com/)
   Chet 的博客专注于 Flex/Flash 图形技术。

### DB2

11. DB2 Express-C 网站：
    [ibm.com/db2/express](http://ibm.com/db2/express)
    使用此网站下载 DB2 Express-C 服务器、DB2 客户端、DB2 驱动程序、手册的映像，访问团队博客，注册邮件列表等。
12. DB2 Express-C 论坛：
    [www.ibm.com/developerworks/forums/dw_forum.jsp?forum=805&cat=19](http://www.ibm.com/developerworks/forums/dw_forum.jsp?forum=805&cat=19)

