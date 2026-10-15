
图 8.3：可以在 JSP 中访问 JDBC。

在开发时可能会可能会使用 JSP 而不是 servlet，因为编译过程是自动的。然而，当将复杂代码保留在 Java servlet 中并将 JavaServer Pages 用于表示层时，生产环境 Web 应用程序运行得更好。

## 本章总结

## 关键术语

| 数据类型 | 连接 | 关系型数据库 |
|---|---|---|
| 驱动管理器 | JSP | SELECT |
| 外键 | ODBC | 结构化查询语言 |
| INSERT | 主键 | 集合处理 |
| JDBC | 引用完整性 | UPDATE |

## 复习题

1. JDBC 的四个组成部分是什么？
2. 什么是关系型数据库？
3. 什么是主键？
4. 什么是外键？
5. 列出三种数据类型。

## 编程作业

### 练习 1：创建数据库

1. 按照章节创建 order、detail 和 customer 表。在适当的地方添加外键关系。如果你使用 PostgreSQL 数据库，这里有几点：
   a) 记得第 5 章 PostgreSQL 文档位于 `/usr/share/doc` 目录。
   b) 以下命令启动 PostgreSQL：
   `# /etc/rc.d/init.d/postgresql start`
   c) 设置 PostgreSQL 用户，使用以下步骤：
      i. 以 root 登录，
      ii. 使用 `su` 命令参数 `postgres`：
      `# su postgres`
      iii. 使用 PostgreSQL `createuser` 命令并按照提示：
      `# createuser username`
      iv. 使用 PostgreSQL `createdb` 命令并按照提示：
      `# createdb username`
   d. 使用 `psql` 命令调用交互式 SQL 会话。

2. 在每个表的主键上创建索引。确保不允许重复键。

3. 为每个客户填充多个订单，为每个订单填充多个项目。

4. 尝试添加包含重复键的行。如果你在该表上创建了唯一索引，DBMS 将不允许添加与现有行具有相同的键。

### 练习 2：显示数据库信息

使用练习1创建的数据库执行以下操作：

1. 按客户列出订单。
2. 列出特定客户的订单。
3. 列出特定客户的订单和订单详情。

### 练习 3：JDBC

1. 将 Basics.1 中的 `JDBCBasics` servlet 部署到 Tomcat。
   a) 将代码输入名为 `JDBCBasics.java` 的文件。
   b) 运行以下 SQL 语句以创建并填充 `JDBCBasics` 使用的表：

| CREATE TABLE QUSTCUSTOM (CUSNUM NUMERIC(6,0), LASTNAME(6), INIT CHAR(3), |
| STREET CHAR(13), CITY CHAR(6), STATE CHAR(2), ZIPCODE NUMERIC (5, 0), |
| CDTLMT NUMERIC (4, 0), CHCGOD NUMERIC (1,0), BALDEC DECIMAL (6, 2), |
| CNTUE NUMERIC (6, 2) ); |
| INSERT INTO QUSTCUSTOM VALUES(938472, 'Henning', 'G K', |

# 136 · 第 9 章

你可能在想，为什么会有个人或组织愿意投入时间和才华来改进一个 Web 服务器，却没有任何投资回报的承诺。首先，你必须理解回报是存在的：一个改进后的 Web 服务器。其次，组织通过扩展 Apache HTTP 服务器并与他们分享自己的改进来回馈 Apache 组织。第三，还有一些无聊的开发者，他们想要为网络空间做出贡献，并选择通过增强世界上最流行的 Web 服务器来实现这一目标。（这在简历上看起来也很不错）

## 补丁 (Patches)

“这里打一个补丁，那里打一个补丁”的想法会让人联出一条旧牛仔裤，在那些设计不当的区域胡乱打着补丁。在涉及到 HTTP 请求时，请忘记“补丁”这个词。

| 模块 | 描述 |
| :--- | :--- |
| mod_asis | 按原样发送消息，不带 HTTP 请求头。 |
| mod_actions | 将 CGI 脚本指定为特定文件的处理程序。 |
| mod_spelling | 根据系统中的文件和目录名修正 URL 解析。 |
| mod_user | 通过用户名和公共前缀选择资源。 |
| mod_alias | 将文件系统的部分映射到另一部分。 |
| mod_rewrite | 使用指定的规则重写 URL。 |
| mod_access | 根据 MIME 类型或 HTTP 请求方法运行 CGI 脚本。 |
| mod_auth | 提供针对基于文本密码文件的身份验证。 |
| mod_auth_anon | 允许对认证区域进行匿名访问。 |
| mod_auth_db | 提供针对数据库的 HTTP 身份验证。 |
| mod_expires | 处理带有过期 HTTP 头的响应。 |
| mod_headers | 操控响应头。 |
| mod_so | 在运行时加载模块。 |
| mod_setenvif | 根据请求中的头部字段设置环境变量。 |

要使用模块，你必须在配置文件中指定 `AddModule` 指令，并说明你想要在 Apache 服务器启启模块名称。这非常简洁。基础服务器非常小且运行快速，但可以通过标准模块轻松扩展，以支持如 servants、Perl、FastCGI（又称持久 CGI）、HTTP Cookie、服务器端包含和安全套接层 (SSL) 等高级功能。

然而，模块的队列并不此结束。Apache HTTP 服务器的设计旨在充分利用模块化编程的力量，从而产生了一个易于扩展和自定义的服务器。任何人都可以通过创建自定义 Apache 模块来扩展 Apache HTTP 服务器。

有时，当某个特定的自定义模块被广泛使用并获得好评后，Apache 会将将其添加到 Apache 下载包中包含的核心模块集中。许多经常使用和推荐的第三方模块可以从 http://modules.apache.org 免费获取。

## Apache 代码

附加的 Apache 模块可以静态或动态绑定到 HTTP 服务器程序。如前所述，你通过在配置文件中指定 `AddModule` 指令和和模块名称来动态绑定 Apache 模块。为了提高速度，你可以通过重新编译服务器程序将 Apache 模块静态绑定到 Apache HTTP 服务器。该服务器程序称为 `httpd`（代表“超文本传输协议守护进程”）。你可以将 `httpd` 视为一个隐藏在后台的守护进程，等待人们尝试通过 TCP/IP 和 HTTP 获取对你主机的 Web 访问。Apache HTTP 服务器交付时带有二进制可执行程序 `httpd`、`httpd` 的完整 C 源代码以及所有标准 Apache 模块扩展的 C 代码。

## Apache 启动

可以通过从终端会话调用 `httpd` 命令来启动 Apache Web 服务器，但大多数发行版都有一个简化 Apache 的启动脚本。Red Hat 的脚本也称为 `httpd`，存在于 `/etc/rc.init.d/` 目录下。如果你尝试在不带任何选项的情况下调用脚本，将收到以下消息：

```
$ /etc/rc.init.d/httpd

Usage: httpd [start|stop|restart|reload|condstart|status]
```

这条帮助信息告诉你是 `httpd` 脚本所需的参数。`status` 选项将告诉你 Apache 是否激活，其他选项则一目易见。

当 Apache 启动时，它会在 `/etc/httpd/conf` 中寻找 `httpd.conf` 文件。当你第一次查看 `httpd.conf` 时可能会有些不知所措，因此我们在图 9.1 中提供了一个最小版本。Apache 预期特定的目录结构：

- 用于存放 `httpd.conf` 文件的目录
- 一个名为 `htdocs` 的目录，用于存放 Apache 提供服务的超文本文档
- 一个名为 `logs` 的目录，用于存放 Apache 配置记录的各种信息

```
# httpd.conf Apache 配置文件

ServerRoot "/etc/httpd"

Port 8888

User nobody

Group nobody

ServerAdmin denonco@attglobal.com

ServerName localhost

DocumentRoot "/home/donat/www2/htdocs"

LoadModule mime_module modules/mod_mime.so

LoadModule dir_module modules/mod_dir.so

AddModule mod_mime.c

AddModule mod_dir.c
```
