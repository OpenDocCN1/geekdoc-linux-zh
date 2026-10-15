
```
# Each directory to which Apache has access can be configured with respect
# to which services and features are allowed and/or disabled in that
# directory (and its subdirectories).
#
# First, we configure the "default" to be a very restrictive set of
# permissions.
#
<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>
```

### Options 指令

要配置 Apache 默认可用的配置选项，必须使用 `Options` 指令。`Options` 可以是 `None`；`All`；或 `Indexes`、`Includes`、`FollowSymLinks`、`ExecCGI` 和 `MultiViews` 的任意组合。`MultiViews` 未包含在 `All` 中，必须显式指定。这些选项在表 17.2 中进行了说明。

#### 表 17.2 Options 指令使用的开关

| Switch | Description |
|---|---|
| None | 此目录未启用任何可用选项。 |
| All | 此目录启用了除 `MultiViews` 外的所有可用选项。 |
| Indexes | 如果没有 `index.html` 文件或其他 `DirectoryIndex` 文件，则会生成目录中文件的列表作为 HTML 页面显示给用户。 |
| Includes | 此目录允许使用服务器端包含（SSIs）。如果您想允许包含但不想在其中允许 `exec` 选项，也可以写成 `IncludesNoExec`。出于安全原因，在您无法完全控制的目录中，例如 `UserDir` 目录，这通常是一个好主意。 |
| FollowSymLinks | 允许访问符号链接到文档目录的目录。您永远不应为整个服务器全局设置此选项，也只能在个别目录中很少设置。此选项存在潜在的安全风险，因为它允许 Web 用户从文档目录中逃逸，并且可能允许他们访问您文件系统中您真的不希望人们随意查看的部分。 |
| ExecCGI | 即使该目录未在 `ScriptAlias` 指令中定义，也允许在此目录中使用 CGI 程序。 |
| MultiViews | 这是 `mod_negotiation` 模块的一部分。当客户端请求找不到的文档时，服务器会尝试找出最符合客户端要求的文档。请参阅 `http://localhost/manuals/mod/_mod_negotiation.html` 获取您本地的 Apache 文档副本。 |

> NOTE
>
> 这些指令也会影响指定目录下的所有子目录。

### AllowOverrides 指令

`AllowOverrides` 指令指定 `.htaccess` 文件可以覆盖哪些配置选项。您可以为每个目录单独设置此指令。例如，您可以在主文档根目录和 `UserDir` 目录中对可以被覆盖的内容制定不同的标准。

此功能对于用户目录尤其有用，因为用户无法访问主服务器配置文件。

`AllowOverrides` 可以设置为 `All` 或 `Options`、`FileInfo`、`AuthConfig` 和 `Limit` 的任意组合。这些选项在表 17.3 中进行了说明。

#### 表 17.3 AllowOverrides 指令使用的开关

| Switch | Description |
|---|---|
| Options | `.htaccess` 文件可以添加 `Options` 指令中未列出的选项。 |
| FileInfo | `.htaccess` 文件可以包含用于修改文档类型信息的指令。 |
| AuthConfig | `.htaccess` 文件可能包含授权指令。 |
| Limit | `.htaccess` 文件可能包含 `allow`、`deny` 和 `order` 指令。 |

### 文件系统身份验证和访问控制

您很可能会在网站上包含不打算公开的材料。您必须能够将这些材料锁定以防止公众访问，并为指定用户提供解锁材料的方式。Apache 提供了两种实现此类访问的方法：身份验证和授权。您可以使用不同的标准来控制对网站各部分的访问，包括检查客户端的 IP 地址或主机名，或要求用户名和密码。本节简要介绍其中一些方法。

> CAUTION
>
> 允许单个用户将 Web 内容放在您的服务器上会带来几个重要的安全风险。如果您在 Internet 而非私有网络上运行 Web 服务器，您应该阅读 WWW 安全常见问题解答 `http://www.w3.org/Security/Faq/www-security-faq.html`。

### 使用 allow 和 deny 限制访问

限制对网站材料的访问的最简单方法之一是根据 IP 地址或主机名限制对特定用户组的访问。Apache 使用 `allow` 和 `deny` 指令来实现此目的。

这两个指令都以地址表达式作为参数。以下列表提供了地址表达式的可能值和用法：

- `all` 可用于影响所有主机。
- 主机名或域名，可以是部分或完全限定的域名；例如，`test.gnuix.org` 或 `gnuix.org`。
- IP 地址，可以是完整或部分的；例如，`212.85.67` 或 `212.85.67.66`。
- 一个网络/子网掩码对，例如 `212.85.67.0/255.255.255.0`。
- 以无类别域间路由（CIDR）格式指定的网络地址；例如，`212.85.67.0/24`。这是前一个示例中使用的相同网络和子网掩码的 CIDR 表示法。

如果可以选用的话，最好基于 IP 地址而不是主机名来设置访问控制。这样做可以获得更快的性能，因为不需要名称查找——客户端的 IP 地址包含在每个请求中。

你也可以使用 `allow` 和 `deny` 来根据特定环境变量是否存在与否来提供或拒绝对网站内容的访问。例如，下面的语句拒绝包含名为 `NOACCESS` 的环境变量的上下文的请求访问：

```
deny from env=NOACCESS
```

Apache 的默认行为是先应用所有 `deny` 指令，然后再检查 `allow` 指令。如果你想更改此顺序，可以使用 `order` 语句。Apache 可能以三种不同的方式解释此语句：

- `Order deny,allow`—`deny` 指令在 `allow` 指令之前被评估。如果主机未被明确拒绝访问，则允许其访问资源。这是如果未指定其他内容时的默认排序。
- `Order allow,deny`—所有 `allow` 指令在 `deny` 指令之前被评估。如果主机未被明确允许访问，则拒绝其访问资源。
- `Order mutual-failure`—只有同时在 `allow` 指令中指定并且在同一时间未出现在 `deny` 指令中的主机才被允许访问。如果主机未出现在任一指令中，则不授予访问权限。

考虑这个例子。假设你只想允许来自你自己域内的人员访问你的网站上的 `server-status` 资源。如果你的域名为 `gnulix.org`，你可以在配置文件中添加以下几行：

```
<Location /server-status>
SetHandler server-status
Order deny,allow
Deny from all
Allow from gnulix.org
</Location>
```

### Authentication

身份验证是确保访客确实是他们声称的人的过程。你可以配置 Apache 仅允许能够验证其身份的客户端访问特定 Web 内容区域。Apache 中有几种身份验证方法；基本身份验证是最常见的（也是本章讨论的方法）。

在基本身份验证下，Apache 要求用户提供用户名和密码以访问受保护的资源。然后 Apache 验证用户是否被允许访问相关资源。如果用户名可接受，Apache 会验证密码。如果密码也通过检查，用户将被授权，Apache 将提供请求。

HTTP 是一种无状态协议；发送到服务器的每个请求和每个响应都是单独处理的，而不是以智能方式处理。因此，身份验证信息必须包含在每个请求中。这意味着对受密码保护区域的每个请求都更大，因此会稍慢一些。为了避免不必要的系统使用和延迟，只保护绝对需要保护的网站区域。

要使用基本身份验证，你需要一个列出哪些用户被允许访问资源的文件。该文件由包含名称和密码对的纯文本列表组成。它看起来非常像你的 Linux 系统的 `/etc/passwd` 用户文件。

> CAUTION
>
> 不要使用 `/etc/passwd` 作为身份验证的用户列表。当你使用基本身份验证时，密码和用户名以 base64 编码文本的形式从客户端发送到服务器——这与纯文本一样可读。用户名和密码包含在发送到服务器的每个请求中。因此，任何可能在网络流量中窃听的人都能够获取这些信息！

要为 Apache 创建用户文件，请使用 `htpasswd` 命令。它包含在 Apache 软件包中。如果你使用软件包安装，它位于 `/usr/bin`。运行不带任何选项的 `htpasswd` 会产生以下输出：
