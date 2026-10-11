

## 表 13.13 *用于 BrowserMatch 变量的格式。*

| 格式 | 描述 |
| :--- | :--- |
| **变量** | 要激活的 Apache 变量的名称。 |
| **!变量** | 要停用的 Apache 变量的名称。 |
| **变量=值** | 分配给列出的 Apache 变量的值。 |

现在来看另一个模块：

```
<IfModule mod_perl.c>
  Alias /perl/ /home/httpd/perl/
  <Location /perl>
    SetHandler perl-script
    PerlHandler Apache::Registry
    Options +ExecCGI
  </Location>
</IfModule>
```

这个 **<IfModule>** 语句用于查找 Perl 模块。如果存在该模块，它首先通过 **Alias** 指令告诉 Apache，当有人请求 /perl 目录时，不要查看 DocumentRoot/perl，而应查看 /home/httpd/perl。然后，使用 **Location** 指令来定义 perl 目录及其内容的可接受行为。这里有两条新指令。第一条是 **SetHandler**，它强制将 perl 中的所有文件传递给列出的处理器。在这种情况下，该处理器是 **perl-script**。此处理器是 Perl 模块的一部分。

现在 Apache 知道对 perl 中文件的请求实际上是对 /home/httpd/perl 的请求，并且该目录的内容应被视为 Perl 脚本，Apache 需要知道如何处理 Perl 脚本。这就是 **PerlHandler** 语句发挥作用的地方。每当 Apache 需要运行 Perl 脚本时，它会转到 Apache::Registry 模块，该模块包含一个用于解释 Perl CGI 脚本的通用处理器。

现在是时候引入更多模块了：

```
#LoadModule put_module      modules/mod_put.so
#AddModule mod_put.c
```

这是另外两条新指令。**LoadModule** 访问文件系统并将模块添加到 Apache 的活动模块列表中。此指令的**使用**格式如下：

```
LoadModule module file
```

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_460_0.png)

另一方面，**AddModule** 将模块添加到 Apache 但不使其处于活动状态。使用方式有所不同：

```
AddModule module
```

因此，通常不会同时注释掉这两项。要么加载它，要么添加它。不能两者兼得。mod_put 模块可从 [http://pwww.ec-lyon.fr/~/vincent/apache/mod_put.tgz](http://pwww.ec-lyon.fr/~/vincent/apache/mod_put.tgz) 获取，并用于实现表 13.9 中描述的 **HTTP PUT** 和 **DELETE** 方法。

在这些项之后是一个 HTTP 上传区域定义：

```
#Alias /upload /tmp
#<Location /upload>
# EnablePut On
# AuthType Basic
# AuthName Temporary
# AuthUserFile /etc/httpd/conf/passwd
# EnableDelete Off
# umask 007
# <Limit PUT>
#	require valid-user
# </Limit>
#</Location>
```

这个被注释掉的段落首先告诉 Apache，每当 HTTP 客户端请求 DocumentRoot/upload 中的任何内容时，服务器应转向 /tmp 目录的内容。然后，一个 **<Location>** 语句概述了 DocumentRoot/upload 允许的内容。

这里定义了几条新指令。第一条是 **EnablePut**。正如您可能猜到的，此指令使表 13.9 中描述的 PUT HTTP 方法可用于使用。**AuthType** 虽然不新，但之前未在上下文中定义。**AuthType** 指令设置访问目录所需的用户身份验证级别。这确保此代码段不会让随机人员访问 DocumentRoot/upload 目录。**AuthType** 有两个可用值，但目前仅实现了 **Basic**。此值要求客户端登录以使用您的网络空间中的此部分。

此代码段中需要另外三条指令才能完全实现身份验证方案。代码中的下一项 **AuthName** 就是其中之一。它为此特定的授权规则分配一个独特的字符串，因此当用户试图访问受保护的 URL 时，他们会收到将密码请求置于上下文中所需的信息。在这种情况下，文本“Temporary”将出现在身份验证对话框中。这里需要的另一条指令 **AuthUserFile** 设置了包含此文件系统段用户和密码信息的文件路径。使用户身份验证生效的最后一条必要指令是 **require**，它出现在此语句的末尾附近。您可以按以下方式使用 **require**：

- 使用以下语法明确列出可以登录到网站此部分的用户：
  ```
  require user user1 user2 ... userN
  ```
- 使用以下语法明确列出可以登录到网站此部分的组：
  ```
  require group group1 group2 ... groupN
  ```
- 使用以下语法允许任何有效用户进入该目录：
  ```
  require valid-user
  ```

此处提到的所有用户都必须存在于由 **AuthUserFile** 指令指定的文件中。

此语句中的下一条指令是 **EnableDelete**。正如您可能会猜测的，此指令激活表 13.9 中描述的 **DELETE** HTTP 方法。然后是 **umask**，它将此目录中新文件的默认掩码设置为 ------rxw。最后，使用 **PUT** 将文件添加到上传目录的所有权限仅限于正确登录的人。

> **警告！** 允许人们以这种方式上传文件基本上是一种允许 FTP 访问的方法。请仔细考虑安全影响！

下一个被注释掉的段落是：

```apache
#<Location /server-status>
#SetHandler server-status
#order deny,allow
#deny from all
#allow from .your_domain.com
#</Location>
```

虽然 `<Directory>` 指令根据项目在文件系统中的位置控制访问，但 `<Location>` 指令通过 URL 控制访问。这些是相对 URL，而不是完整路径，因此在默认的 Red Hat 设置中，**/server-status** 将位于 /home/httpd/html/server-status。此指令下列出的第一项是 **SetHandler**，它坚持指定的位置指向用于服务的特定 Apache 模块。默认处理器列表见表 13.14。

基本上，如果激活此部分，允许来自您指定的域或网络内的任何人获取 Web 服务器状态更新。下一个 **<Location>** 指令是：

```apache
#<Location /server-info>
#  SetHandler server-info
#  Order deny,allow
#  Deny from all
#  Allow from .your_domain.com
#</Location>
```

当正确配置时，此代码允许您选择的客户端访问 DocumentRoot/server-info 以了解您的 Apache 服务器是如何配置的。问题是，如果某人伪装成允许的地址，他们可以了解您的设置情况，然后利用这些信息造成一些损害。

在这组注释之后是：

```apache
Alias /doc /usr/doc
<Location /doc>
    order deny,allow
    deny from all
    allow from localhost
    Options Indexes FollowSymLinks
</Location>
```

## 表 13.14 SetHandler 指令的默认处理器。

| 处理器 | 用途 |
| :--- | :--- |
| cgi-script | 将此项作为 CGI 脚本运行 |
| imap-file | 查阅 imap 规则文件以确定如何处理此图像 |
| send-as-is | 将此项视为 .asis 文件，发送时不带 HTTP 头 |
| server-info | 显示服务器配置信息 |
| server-parsed | 在此文档中查找 SSI |
| server-status | 获取服务器状态报告 |
| type-map | 查阅类型映射以获取有关此文件的编码、语言、长度和其他值的信息 |

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_463_0.png)

此部分将 DocumentRoot/doc 设置为实际上指向 /usr/doc，并允许 Web 服务器上的人们通过 Web 浏览器查看 /usr/doc 的内容。然后是以下部分：

```
#<Location  /cgi-bin/php*>
#deny from all
#ErrorDocument 403 http://php.apache.org/php_abuse_log.cgi
#</Location>
```

这包含另一个 **<Location>** 指令。在这种情况下，它指的是任何试图访问 DocumentRoot/cgi-bin/php* 的人。这实际上指的是一个以前存在 bug 的脚本。此部分旨在捕捉任何试图利用此旧 bug 的人，并记录该实例。

现在我们到达代理部分：

```
#<IfModule mod_proxy.c>
#  ProxyRequests On
#  <Directory proxy:*
#    Order deny,allow
#    Deny from all
#    Allow from .your_domain.com
#  </Directory>
```

如果您不想麻烦使用第 14 章中讨论的 Squid 缓存代理服务器，您可以在此处激活 Apache 自己的代理模块。**ProxyRequests** 指令指的是 Apache 代理功能是否生效。如果您使用的是代理防火墙，如第 9 章中所述，则必须启用这些功能。除了激活代理外，您可以启用 Via: HTTP 头，通过以下方式帮助控制信息如何流经代理：

```
#  ProxyVia On
```

接下来是与缓存相关的指令：

```
#  CacheRoot  /var/cache/httpd
#  CacheSize  5
#  CacheGcInterval  4
#  CacheMaxExpire  24
#  CacheLastModifiedFactor  0.1
#  CacheDefaultExpire  1
#  NoCache  a_domain.com another_domain.edu  joes.garage_sale.com
#</IfModule>
```

这些指令在表 13.15 中进一步解释。

