

# Oracle 攻击与防御 • 第 13 章

使用如 SYS、SYSTEM 或 CTSYS 等默认用户登录名和密码。至少，他们可以通过修改密码并导致账户无法使用来拒绝服务。请求 http://<oracleserver>/pls/<hostname>/admin_/ 可以显示该站点是否存在漏洞。如果返回了管理页面，那么此站点确实存在漏洞。为了加固此项，需要执行以下几个步骤：编辑位于 $ORACLE_HOME\Apache\modplsql\cfg 目录下的 `wdbsvr.app` 文件；将 "adminPath" 条目修改为难以猜测或暴力破解的内容；添加一个密码。

# PL/SQL 身份验证拒绝服务

PL/SQL 模块存在拒绝服务漏洞。当模块接收到带有格式错误的 Authorization HTTP 客户端标头（且未设置授权类型，如 Basic）的请求时，Apache 会发生访问冲突或核心转储（core dump）。解决方法是安装 Oracle 提供的补丁。该补丁可以在 Metalink 网站获取。该漏洞的补丁号为 2209455。

# OWA_UTIL PL/SQL 封装

OWA_UTIL 软件包的作用是提供 Web 相关的服务，以及如超文本过程 (htp)、用于创建 HTML 内容 (htf)、生成 HTML 标签的函数等包。这些和其他包都是作为 PL/SQL Toolkit 的部分安装的。OWA_UTIL 了许多可以从 Web 直接调用的过程——本节将查看 signature、showsource、cellsprint、listprint 和 show_query_columns。

## owa_util.signature

Signature 除了返回一条消息外并无其他作用。它可以被用于验证是否可以访问 owa_util。它不需要任何参数（也可以接受某些参数）：

```
http://oracleserver/pls/dna/owa_util.signature
```

如果返回了类似“此页面由 PL/SQL 模块于 2001 年 12 月 21 日上午 04:50 生成”的消息，则说明可以访问 owa_util。如果它没有返回此内容且 Web 服务器返回了 500 或 403 响应，则可能是该包受到了保护。不过通常并非如此，取决于具体的保护方式，可以通过在路径前插入空格、制表符或换行符来绕过这种保护：

![](img/729efc56f204a2ebffb8295c3a2dfdfb_727_0.png)

http://oracleserver/pls/dadname/%20owa_util.signature
http://oracleserver/pls/dadname/%0Aowa_util.signature
http://oracleserver/pls/dadname/%08owa_util.signature

无论如何获得访问权限，一旦获得，就可以调用其他过程。

## owa_util.showsource

Showsource 会返回包的源代码。它接受一个参数 cname，即要查看的包名。以下是一个演示了如何查看 owa_util 源代码的示例：

```
http://oracleserver/pls/dadname/owa_util.showsource?cname=owa_util
```

这将给出 owa_util 包的源代码。以下是该查询输出的第一部分的片段：

```
package owa_util
 OWA_UTIL is
```

```
type ident_arr is table of varchar2(30) index by binary_integer;
type num_arr is table of number by binary_integer;
type ip_address is table of integer index by binary_integer;
```

```
********************************************************************************
/* 用于链接回你的过程 PL/SQL 源码的过程 */
********************************************************************************
/* SHOWSOURCE 可以接受过程、函数、 */
/* package.procedure 或 package.function 作为参数。 */
/* SHOWSOURCE 打印指定存储 PL/SQL 的源码。 */
/* 如果传递了 package.procedure 或 package.function，它将 */
/* 打印整个包。 */
procedure datasource(cname in varchar2);
```

## owa_util.cellsprint

Cellsprint 允许运行任意的 SELECT SQL 查询。它需要一个参数 p_theQuery，但也可以接受第二个参数 p_max_rows，该参数指定返回的行数。如果未指定 p_max_rows，则返回 100 行。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_728_0.png)

- http://oracleserver/pls/dadname/owa_util.cellsprint?p_theQuery=select**from+sys.dba_users 返回 sys 架构下 dba_users 表的前 100 行。
- http://oracleserver/pls/dadname/owa_util.cellsprint?p_theQuery=select**from+sys.dba_users&p_max_rows=1000 从同一张表中返回 1,000 行。防止访问递归的 SELECT 查询是非常重要的，因为许多表包含敏感信息，例如 sys.link。此表包含了连接到被查询数据库的数据库服务器列表。这里还存储了明文的用户 ID 和密码，这些在建立连接时会被使用。如果有任何连接，就可能从第一个数据库服务器进行“代理”访问。
- http://oracleserver/pls/dadname/owa_util.cellsprint?p_theQuery=select**from+sys.dba_users 通过添加“other.world”，此表包含了连接到被查询数据库的数据库服务器列表。

## owa_util.listprint

Listprint 允许执行任意 SQL 查询。它需要一个参数 p_theQuery，但也可以接受第二个参数 p_max_rows，这指定了返回多少行。如果没有指定 p_max_rows，则返回 100 行。

无论如何获得访问权限，一旦获得，就可以调用其他过程。

由于 DAD 仅仅是如何访问数据库的描述，执行 select * 时，返回的是 DAD 自身的列。绕过银行应用只需选择一个列名：

```
http://oracleserver/pls/dadname/owa_util.listprint?p_theQuery=select%20from%20sys&size=
```

这引出了一个问题——如何找到表的列名？

## owa_util.show_query_columns

show_query_columns 过程可以用于获取表的列列表。该过程接受一个参数 table，即表名：

```
http://oracleserver/pls/dadname/owa_util.show_query_columns?table=dba_users
```

返回的 HTML 将包含列列表。如果攻击者可以访问 OWA_UTIL 包，他就可以随心所欲地浏览数据库。因此，防御至关重要。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_729_0.png)

# PL/SQL 身份验证绕过

在某些情况下，尝试访问 PL/SQL 包时可能会绕过身份验证过程。想象有一个允许客户注册的在线银行系统。将有一个 PL/SQL 应用程序来实现，它有自己的 DAD。该 DAD 配置了用户 ID 和密码，因此允许想要注册的人“匿名”访问。注册后，用户将访问实际的银行应用程序，该程序有自己的 DAD。此类用户尝试访问银行应用程序时，会提示输入凭据。

银行站的 URL 类似于：

```
http://oracleserver/pls/register/reg.signup
http://oracleserver/pls/banking/account.welcome
```

由于 DAD 只是访问数据库的描述，可以通过替换 DAD 来绕过银行应用的认证：

```
http://oracleserver/pls/register/account.welcome
```

这种访问是被允许的，因为在“register”DAD 中配置的用户 ID 和密码已对用户进行了数据库身份验证。防御这种问题的方法：首先，应授予银行应用程序访问该应用程序使用的数据库表。访问注册应用程序的用户 ID 不应能够访问应用程序使用的表。防止此类问题的第二种方法是编辑 dwdbsvr.app 文件，并在 exclusion_list 条目中添加项：

```
exclusion_list= account*, sys.*, dbms_*, owa*
```

## PL/SQL 跨站脚本漏洞

默认情况下，允许访问 htp PL/SQL 包。该包导出了输出 HTML 和 HTML 标签的过程。许多过程可用于跨站脚本攻击。

