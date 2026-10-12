

## 注意

在镜像他人的网站之前，你必须获得他们的许可，因为这可能涉及版权问题。

## 创建反向代理服务器

当真实的 HTTP/FTP 服务器位于防火墙之后，或者需要某种负载均衡方案来加速或分发内容交付时，就需要使用反向代理服务器。使用 Apache 1.3.x 中最新的代理模块创建反向代理服务器非常容易。假设你有一个主机名为 realserver.yourcompany.com 的 Web 服务器，你希望所有人都通过名为 www.yourcompany.com（11.22.33.44）的反向代理服务器来访问它。你可以在 yourcompany.com 服务器上创建以下虚拟主机：

```
<VirtualHost 11.22.33.44>
ServerName www.yourcompany.com
ProxyPass / realserver.yourcompany.com/
ProxyPassReverse / realserver.yourcompany.com/
CacheRoot /www/cache
CacheDefaultExpire 24
</VirtualHost>
```

这使得代理服务器成为 realserver.yourcompany.com 的反向代理。对于你的访问者来说，看起来他们正在访问 www.yourcompany.com。

## 身份验证 Web 用户

知道如何创建密码保护的受限区域是每个 Web 管理员的必备技能。默认情况下，Apache 支持主机基础身份验证和基本 HTTP 身份验证等方案。

### 使用主机基础身份验证

在此身份验证方案中，访问权限由主机名或主机的 IP 地址控制。当请求某个资源时，Web 服务器首先检查请求主机是否允许访问该资源，然后根据检查结果采取行动。标准的 Apache 发行版包含一个名为 mod_access 的模块，该模块通过 Allow、Deny、Order、Allow from env=variablename 和 Deny from env=variablename 等指令提供此访问控制支持。

`Allow from host1 host2 host3 ...`

该指令允许你定义一个主机列表（包含一个或多个主机或 IP 地址），这些主机被允许访问某个目录。当指定多个主机或 IP 地址时，它们之间应使用空格字符分隔。表 12-3 展示了该指令的可能取值。

**表 12-3 allow 指令的可能取值**

| 取值 | 示例 | 描述 |
| ----- | ------- | ----------- |
| All | allow from all | 该保留字允许所有主机访问。示例展示了如何使用此选项。 |
| 主机的完全限定域名 (FQDN) | allow from wormhole.nitec.com | 只有拥有指定 FQDN 的主机才被允许访问。示例中的 allow 指令仅允许 wormhole.nitec.com 访问。请注意，这是逐部分比较的；因此，toys.com 不会匹配 o Toys.com。 |
| 主机的部分域名 | allow from .mainoffice.nitetc.com | 只有匹配部分主机名的主机才被允许访问。示例允许 .mainoffice.nitetc.com 网络中的所有主机访问该站点。例如，developer1.mainoffice.nitetc.com 和 developer2.mainoffice.nitetc.com 可以访问该站点，但 developer3.baoﬃce.nitetc.com 不被允许访问。 |
| 主机的完整 IP 地址 | allow from 206.171.50.50 | 只有指定的 IP 地址被允许访问。示例显示了一个完整的 IP 地址（包含 IP 地址的所有四个八位组），即 206.171.50.50，因此允许访问。 |
| 部分 IP 地址 | 示例 1: allow from 206.171.50<br>示例 2: allow from 130.86 | 当 allow 指令中未包含 IP 地址的所有四个八位组时，部分 IP 地址将从左向右进行匹配，拥有匹配 IP 地址模式（即属于同一子网）的主机将被允许访问。在第一个示例中，所有 IP 地址在 206.171.50.1 到 206.171.50.255 范围内的主机都有访问权限。在第二个示例中，130.86 网络中的所有主机都被允许访问。 |
| 网络/子网掩码对 | Allow from 206.171.50.0/255.255.255.0 | 这允许你使用网络地址和子网掩码地址来指定 IP 地址范围。示例仅允许 IP 地址在 206.171.50.1 到 206.171.50.255 范围内的主机进行访问。此功能在 Apache 1.3 或更高版本中可用。 |
| 网络/nnn CIDR 规范 | Allow 206.171.50.0/24 | 与上一条类似，只是网络由 nnn 位高位 1 组成。示例等同于 allow from 206.171.50.0/255.255.255.0。此功能在 Apache 1.3 或更高版本中可用。 |

### deny from host1 ...

该指令是 allow 指令的完全相反操作。它允许你定义一个被拒绝访问指定目录的主机列表。与 allow 指令一样，它可以接受表 12-3 中显示的所有取值。

### order deny, allow | allow, deny | mutual-failure

该指令控制 Apache 如何评估 allow 和 deny 指令。例如，以下内容拒绝了主机 myboss.mycompany.com 的访问，并允许所有其他主机访问该目录：

```
<Directory "/my site/myboss/rants">
order deny, allow
deny from myboss.mycompany.com
allow from all
</Directory>
```

order 指令的取值是一个逗号分隔的列表，指示哪个指令具有优先级。通常，影响所有主机的指令被赋予最低的优先级。在上面的示例中，由于 allow 指令影响所有主机，因此被赋予最低的优先级。当此指令设置为 mutual-failure 时，只有出现在 allow 列表中但未出现在 deny 列表中的主机才获得访问权限。在所有情况下，每个 allow 和 deny 指令都会被评估。

### allow from env=variable

该指令是 allow 指令的一个变体，当指定的环境变量被设置时，允许访问。这仅在你使用其他指令（例如 *BrowserMatch*）来设置环境变量时才有用。例如：

```
BrowserMatch "MSIE" ms_browser
<Directory "/path/to/Vbscript_directory">
    order deny,allow
    deny from all
    allow from env=ms_browser
</Directory>
```

在此处，Apache 服务器将为所有在 *User-Agent* 头文件中提供 MSIE 字符串作为部分内容的浏览器设置 *ms_browser* 环境变量。allow 指令将仅允许已设置 *ms_browser* 变量的浏览器进行访问。

### deny from env=variable

该指令是 deny 指令的一个变体，对于设置了指定环境变量的所有主机，拒绝其访问能力。例如，

```
BrowserMatch "MSIE" ms_browser
<Directory "/path/to/Vbscript_directory">
    order deny,allow
    allow from all
    deny from env=ms_browser
</Directory>
```

阻止了所有在请求的 *User-Agent* 头文件中发送 MSIE 字符串作为部分内容的 Web 浏览器的访问。

## 使用 HTTP 指定的基本身份验证

Apache 对 HTTP 指定的基本身份验证的支持已经存在相当长的时间了。默认情况下，Apache 使用 mod_auth_c 模块提供身份验证支持。

该模块在标准发行版中默认被编译。标准的基于 mod_auth 的基本 HTTP 身份验证使用存储在文本文件中的用户名、组和密码来确认身份验证。这在处理少量用户时工作得很好。但是，如果你有很多用户（数千名或更多），使用 mod_auth 可能会带来性能上的损失。在这种情况下，你可以使用更高级的东西，例如 DBM 文件、Berkeley DB 文件，甚至 SQL 数据库。默认的身份验证模块提供以下指令：

`AuthUserFile filename`

该指令设置包含基本 HTTP 身份验证中使用的用户名和密码的文本文件的名称。你必须提供要使用的文件的完全限定路径。例如：

`AuthUserFile /www/ntec/secrets/.htpasswd`

该文件通常使用名为 htpasswd 的支持实用程序创建。该文件的格式非常简单。每一行包含一个用户名和一个加密的密码。为了增强安全性，请将 AuthUserFile 指定的文件保存在网站文档树之外。

`AuthGroupFile filename`

该指令指定用于基本 HTTP 身份验证用户组列表的文本文件。filename 是组文件的绝对路径。你可以使用任何文本编辑器创建此文件。该文件的格式如下：

`groupname: username1 username2 username3 ...`

为了增强安全性，请确保 AuthGroupFile 指定的文件位于网站文档树之外。

`AuthAuthoritative on | off`

