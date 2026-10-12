

# . 在 SCO (ODT 3) 上，请使用 "User nouser" 和 "Group nogroup"。
# . 在 HPUX 上，你无法使用 nobody 用户来使用共享内存，
# 建议的变通方法是创建一个名为 www 的用户并使用该用户。
# 请注意，某些内核拒绝在 (unsigned)Group 的值高于 60000 时设置 setgid(Group) 或 semctl(IPC_SET)；
# 不要在这些系统上使用 Group #-1！
#

User apache
Group apache

默认情况下，apache 被定义为服务器的用户和组。如果你修改了 User 和 Group 指令，你应该指定一个非特权实体。这将最小化如果你的站点被入侵时的损害风险。启动的第一个守护进程以 root 身份运行。这是为了将服务器绑定到低编号端口并切换到由 User 和 Group 指令指定的用户和组所必需的。所有其他服务器都在由这些指令定义的用户 ID (UID) 和组 ID (GID) 下运行。

## 选择 HTTP 端口号

Apache 在特定端口上监听 HTTP 请求。使用的端口由 Port 条目如下设置：

```
#
# Port: 独立服务器监听的端口。对于
# 小于 1023 的端口，你需要先以 root 身份运行 httpd。
#
Port 80
```

Port 80 是 HTTP 流量的默认端口，这就是为什么 http://www.apache.org:80/ 与 http://www.apache.org/ 相同的原因。如果服务器绑定到不同的端口，则必须在 URL 中指定端口号。大多数 Web 服务器运行在 80 端口上，尽管它们可以接受任何未被特定服务绑定的端口（65536 以下）的连接（请参阅 /etc/services 文件以获取常用服务/协议及其使用端口的列表）。只有 root 才能运行在特权端口（1024 以下）上监听连接的程序。

## 设置电子邮件地址

你可以指定一个地址，以便用户在服务器出现问题时发送电子邮件。这是通过 ServerAdmin 指令完成的：

```
#
# ServerAdmin: 你的地址，服务器问题应
# 发送电子邮件至此。此地址会出现在一些服务器生成的页面上，例如
# 错误文档中。例如：admin@your-domain.com
#
ServerAdmin you@your.address
```

ServerAdmin 指令可以设置为任何有效的电子邮件地址。它可以将邮件重定向到用户账户（在同一台或其他机器上），或者将邮件重定向到一个别名（例如 Webmaster），该别名可以将邮件分发给多个人。默认值是 root@localhost。

## 设置服务器名称

如果你的服务器名称不是确切的已注册主机/域名，你应该在此处识别你的服务器名称。正如注释所指出的，ServerName 指令可以设置为与你机器的实际主机名不同的值。然而，如果服务器要成为公共 Internet 服务器，那么这个其他名称在 DNS 中仍应指代你的机器。通常，www 只是机器实际名称的一个别名（例如，一台机器可能响应 www.linuxtoys.net，但其实际名称可能是 al.linuxtoys.net）。

```
ServerName jukebox.linuxtoys.net
```

如果你没有输入有效的服务器名称，Apache 会尝试将你的主机名作为 ServerName 使用。建议在此处显式输入一个 ServerName。

## 设置规范名称

使用 UseCanonicalName 指令来自引用 URL，如下所示：

```
## UseCanonicalName: 确定 Apache 如何构建自引用
# URL 以及 SERVER_NAME 和 SERVER_PORT 变量。
# 当设置为 "Off" 时，Apache 将使用客户端提供的
# Hostname 和 Port。当设置为 "On" 时，Apache 将使用
# ServerName 指令的值。
#
UseCanonicalName Off
```

UseCanonicalName 指令提供了一种命名一致性。当它设置为 on 时，Apache 使用 ServerName 和 Port 指令创建引用同一台机器上文件的 URL（例如，http://www.linuxtoys.net/docs/）。当 UseCanonicalName 为 Off 时，URL 由客户端指定的任何内容组成（例如，如果客户端在同一域名内，URL 可以是 http://al.linuxtoys.net/docs/ 或 http://al/docs/）。

这可能有问题，特别是当访问控制规则需要用户名/密码身份验证时：如果客户端针对主机 al.linuxtoys.net 进行了身份验证，但一个链接将其引导到 www.linuxtoys.net（物理上是同一台机器），客户端将再次被提示输入用户名和密码。建议将 UseCanonicalName 设置为 on。在上述情况下，无需重复身份验证，因为对同一服务器的任何引用始终被解释为 www.linuxtoys.net。

## 识别 HTTP 内容目录

有几个指令用于确定服务器 Web 内容的位置。你的 Web 内容的主位置由 DocumentRoot 指令设置为 /var/www/html。（注意，此位置在 Red Hat Linux 7 之前的版本中有所改变。以前该位置在 /home/http。）

```
# DocumentRoot: 你将从中提供
# 文档的目录。默认情况下，所有请求都取自该目录，但
# 可以使用符号链接和别名指向其他位置。
DocumentRoot "/var/www/html"
```

## 设置访问选项和重写权限

你可以为 Web 服务器目录结构中的每个目录设置单独的访问权限。默认设置相当严格。以下是默认设置：

```
<Directory />
    Options FollowSymLinks
        AllowOverride None
</Directory>
```

此段为 Options 和 AllowOverride 指令设置了默认的权限块。`<Directory />...</Directory>` 标签包围了应用于 / 目录（默认为 /var/www/html）的指令。

Options FollowSymLinks 指令指示服务器目录内的符号链接可以被跟踪，以允许位于计算机其他位置的内容。/ 目录或其下任何目录中的其他特殊服务器功能都不会激活，除非稍后明确指定。接下来，为你的 Web 服务器根目录（/var/www/html）专门设置了以下访问选项。（为了清晰起见，我在此处删除了注释。）

```
<Directory "/var/www/html">
    Options Indexes FollowSymLinks
    AllowOverride None
    Order allow,deny
    Allow from all
</Directory>
```

如果你在此文件中之前修改了 DocumentRoot 的值，你需要将 /var/www/html 更改为与该值匹配。目录的 Options 设置为 Indexes 和 FollowSymLinks。这些和其他特殊服务器功能在表 21-2 中有描述。AllowOverride None 指令指示服务器 .htaccess 文件（或 AccessFileName 的值）不能重写任何特殊访问功能。你可以将 None 替换为表 21-3 中描述的任何特殊访问功能。

> 注意：请记住，除非你明确启用表 21-2 和 21-3 中描述的功能，否则这些功能不会为你的服务器启用（Indexes 和 FollowSymLinks 除外）。

### 表 21-2：Options 指令的特殊服务器功能

| 功能 | 描述 |
| :--- | :--- |
| ExecCGI | 允许执行 CGI 脚本。 |
| FollowSymLinks | 服务器将遍历符号链接。 |
| Includes | 允许服务器端包含。 |
| IncludesNOEXEC | 允许服务器端包含，但不包括 #exec 和 #include 元素。 |
| Indexes | 如果 DirectoryIndex 指令指定的文件都不存在，将生成目录索引。 |
| MultiViews | 服务器允许基于内容的内容文件名模式匹配搜索。 |
| SymLinksIfOwnerMatch | 仅当目标的所有者与链接的所有者相同时，服务器才会遍历符号链接。 |
| None | 上述功能均未启用。 |
| All | 启用上述所有功能，但 MultiViews 除外。此功能必须显式启用。 |

### 表 21-3：AllowOverride 指令的特殊访问功能

| 功能 | 描述 |
| :--- | :--- |
| AuthConfig | 启用身份验证相关指令（AuthName、AuthType、AuthUserFile、AuthGroupFile、Require 等）。 |
| FileInfo | 启用 MIME 相关指令（AddType、AddEncoding、AddLanguage、LanguagePriority 等）。 |
| Indexes | 启用与目录索引相关的指令（FancyIndexing、DirectoryIndex、IndexOptions、IndexIgnore、HeaderName、ReadmeName、AddIcon、AddDescription 等）。 |
| Limit | 启用控制主机访问的指令（Allow、Deny 和 Order）。 |
| Options | 启用 Options 指令（如表 21-5 中所述）。 |
| None | 无法重写上述任何访问功能。 |
| All | 可以重写上述所有访问功能。 |

## 在根目录中禁用索引

以下指令禁用根目录（可能是 /var/www/html）的索引，因此当你访问该目录时

