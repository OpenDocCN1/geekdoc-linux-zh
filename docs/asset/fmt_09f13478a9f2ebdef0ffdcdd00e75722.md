
这里的`mydbpwd`是更新组表所需的数据库密码。

## 使用 Cookie 保护身份验证会话

正如本章前面提到的，`基本 HTTP`身份验证要求 Web 浏览器每次请求受限部分下的页面时，始终传递用户名和编码（非加密）的密码。这使得`中间人`攻击变得过于容易。这种攻击涉及黑客利用基本 HTTP 身份验证在 Web 服务器和 Web 浏览器之间拦截数据包，从而确定密码。

中间人攻击的解决方案是使用安全套接字层（SSL）连接和基于会话的身份验证方案，其中用户通过`基本 HTTP`身份验证进行一次认证，随后对受限资源的所有请求都使用安全的（加密的）会话 Cookie 而不是编码密码进行授权。

本节讨论了一种使用 MySQL 数据库（当然，您也可以使用其他任何 RDBMS）和 CPAN 上的`mod_perl`模块的解决方案。以下是如何实现该解决方案。

-   如果尚未安装，请按照第 16 章的说明安装`mod_perl`模块。

-   使用以下命令以 root 身份为 Apache 安装两个 CPAN 模块：

```perl
perl -MCPAN -e 'install Apache::AuthCookie'
perl -MCPAN -e 'install Apache::AuthTicket'
```

-   安装上述模块后，您需要创建本章前面“在 `mysql server` 中创建用户身份验证数据库”部分讨论的 auth 数据库和 wwwuser 表。您还需要添加以下两个表。

```sql
CREATE TABLE tickets (
    ticket_hash CHAR(32) NOT NULL,
    ts INT NOT NULL,
    PRIMARY KEY (ticket_hash)
);

CREATE TABLE ticketsecrets (
    sec_version BIGINT,
    sec_data TEXT NOT NULL
);
```

按照本章前面“在 `mysql server` 中创建用户身份验证数据库”部分给出的说明，在 auth 数据库中添加这些表。

-   创建上述表后，您必须在 ticketsecrets 表中添加一个密钥。添加密钥最简单的方法是登录到数据库服务器，连接到 auth 数据库，并执行以下插入语句：

```sql
insert into ticketsecrets (sec_version, sec_data) values ('number', 'random_data');
```

-   确定您要限制访问并发放会话 Cookie 的 Web 目录位置。在本示例中，我将此位置称为 `/protected`。将以下配置添加到您的 `httpd.conf` 文件中：

```apache
PerlModule Apache::AuthTicket

PerlSetVar ProtectedTicketDB
DBI:mysql:database=auth:host=localhost

PerlSetVar ProtectedTicketDBUser httpd
PerlSetVar ProtectedTicketDBPassword secret1

PerlSetVar ProtectedTicketTable tickets:ticket_hash:ts

PerlSetVar ProtectedTicketUserTable wwwusers:username:passwd

PerlSetVar ProtectedTicketSecretTable
ticketsecrets:sec_data:sec_version

PerlSetVar ProtectedTicketPasswordStyle crypt
```

以下列表说明了上述配置中的各项内容：

-   这里的`PerlModule`指令告诉 Apache，您希望使用`Apache::AuthTicket`模块。

-   `PerlSetVar`指令用于设置该模块所需的各个键值对。

-   `ProtectedTicketDB`键设置数据库的数据源名称（DSN）。

-   示例值`DBI:mysql:database=auth:host=localhost`告诉`AuthTicket`模块，我们想使用 MySQL 数据库驱动（`mysql`）并连接到名为`auth`的数据库，该数据库位于本地主机（与 Web 服务器相同的机器）上。如果您未在与 Apache Web 服务器相同的机器上运行 MySQL 数据库服务器，请确保将此更改为适当的主机名。

-   `ProtectedTicketDBUser`和`ProtectedTicketDBPassword`指令告诉`AuthTicket`模块访问数据库服务器所需的数据库用户名和密码。

-   `ProtectedTicketTable`、`ProtectedTicketUserTable`和`ProtectedTicketSecretTable`键用于告诉模块在数据库中使用哪些票据和用户表以及需要哪些字段。
-   `ProtectedTicketPasswordStyle`设置加密类型。您有三种选择：传统的 Unix 风格单向哈希加密（即`crypt()`）、明文（不推荐）或 MD5。

6.  接下来添加以下配置行：

```apache
PerlSetVar ProtectedTicketExpires 30

PerlSetVar ProtectedTicketLogoutURI /protected/index.html

PerlSetVar ProtectedTicketLoginHandler /protected/login

PerlSetVar ProtectedTicketIdleTimeout 15

PerlSetVar ProtectedPath /

PerlSetVar ProtectedDomain .domain_name

PerlSetVar ProtectedSecure 1

PerlSetVar ProtectedLoginScript /protected/loginform
```

以下列表说明了上述配置的作用：

-   `ProtectedTicketExpires`键设置会话（票据）的过期时间（以分钟为单位）。
-   `ProtectedTicketLogoutURI`键设置用户注销后显示的 URL。
-   `ProtectedTicketLoginHandler`设置登录处理程序的路径，该路径必须对应于一个`<Location>`容器，如后文所述。
-   `ProtectedTicketIdleTimeout`设置会话允许空闲的分钟数。
-   `ProtectedPath`设置 cookie 的路径。默认值`/`确保 cookie 随所有请求返回。您可以通过将`/`更改为`/protected`（或您正在保护的任何位置）来限制 cookie 仅用于受保护区域。
-   `ProtectedDomain`设置 cookie 的域名。前面的点号确保 cookie 发送到同一域名中的所有 Web 主机。例如，将此设置为`.mobilac.com`将允许在`web1.Mobilac.com`或`web2.Mobilac.com`中查看该 cookie。您也可以通过在此处指定完全限定主机名来将 cookie 限制为单个主机。
-   `ProtectedSecure`设置为 1 以确保 cookie 的安全性。
-   `ProtectedLoginScript`设置登录表单的位置，该表单由模块生成。

7.  现在，您需要按照以下方式为`/protected`目录创建一个`<Location>`容器：

```apache
<Location /protected>
    AuthType Apache::AuthTicket
    AuthName Protected
    PerlAuthHandler Apache::AuthTicket->authenticate
    PerlAuthzHandler Apache::AuthTicket->authorize
    require valid-user
</Location>
```

在此，Apache 被要求需要有效的用户凭证，这些凭证将由`Apache::AuthTicket`模块进行身份验证。

8.  现在，您需要按照以下方式为模块的登录屏幕、登录脚本和注销功能设置处理程序：

```apache
<Location /protectedloginform>
    AuthType Apache::AuthTicket
    AuthName Protected
    SetHandler perl-script
    PerlHandler Apache::AuthTicket->login_screen
</Location>

<Location /protectedlogin>
    AuthType Apache::AuthTicket
