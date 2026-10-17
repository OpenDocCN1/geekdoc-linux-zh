
To limit which server configurations the `.htaccess` files can override, use the `AllowOverride` directive. `AllowOverride` can be set globally or per directory. For example, in your `apache2.conf` file, you could use the following:

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

## Options Directives

To configure which configuration options are available to Apache by default, you must use the `Options` directive. `Options` can be `None`; `All`; or any combination of `Indexes`, `Includes`, `FollowSymLinks`, `ExecCGI`, and `MultiViews`. `MultiViews` isn't included in `All` and must be specified explicitly. These options are explained in Table 17.2.

### TABLE 17.2 Switches Used by the Options Directive

| Switch | Description |
|--------|-------------|
| None | None of the available options are enabled for this directory. |
| All | All the available options, except for MultiViews, are enabled for this directory. |

## 表 17.2 Options 指令使用的开关

| Switch | Description |
| --- | --- |
| Indexes | 如果没有 index.html 文件或其他 DirectoryIndex 文件，则会生成目录中文件的列表作为 HTML 页面显示给用户。 |
| Includes | 允许在此目录中使用服务器端包含（SSIs）。如果想允许包含但不允许其中的 exec 选项，也可以写成 IncludesNoExec。出于安全原因，在你无法完全控制的目录中，例如 UserDir 目录，通常这样做是明智的。 |
| FollowSymLinks | 允许访问符号链接到文档目录的目录。你永远不应为整个服务器全局设置此选项，并且也只应很少为单个目录设置。此选项存在潜在的安全风险，因为它允许 Web 用户从文档目录中逃逸，并可能使他们访问你文件系统中不希望人们随意查看的部分。 |
| ExecCGI | 允许在此目录中使用 CGI 程序，即使它不是 ScriptAlias 指令中定义的目录。 |
| MultiViews | 这是 mod_negotiation 模块的一部分。当客户端请求找不到的文档时，服务器会尝试找出最适合客户端需求的文档。有关本地 Apache 文档，请参阅 http://localhost/manuals/mod/mod_negotiation.html。 |

> NOTE
>
> 这些指令也会影响指定目录下的所有子目录。

## AllowOverrides 指令

`AllowOverrides` 指令指定 `.htaccess` 文件可以覆盖哪些配置选项。你可以为每个目录单独设置此指令。例如，你可以在主文档根目录和 UserDir 目录中对可被覆盖的内容制定不同的标准。

这种功能对于用户目录特别有用，因为用户无法访问主服务器配置文件。

`AllowOverrides` 可以设置为 `All` 或 `Options`、`FileInfo`、`AuthConfig` 和 `Limit` 的任意组合。这些选项在表 17.3 中进行了说明。

## 表 17.3 AllowOverrides 指令使用的开关

| Switch | Description |
| --- | --- |
| Options | `.htaccess` 文件可以添加在此目录 Options 指令中未列出的选项。 |
| FileInfo | `.htaccess` 文件可以包含用于修改文档类型信息的指令。 |
| AuthConfig | `.htaccess` 文件可能包含授权指令。 |
| Limit | `.htaccess` 文件可能包含 allow、deny 和 order 指令。 |

## 文件系统身份验证和访问控制

你很可能会在网站上包含不打算公开的材料。你必须能够将这些材料锁定以防止公众访问，并为指定用户提供解锁材料的手段。Apache 提供了两种实现此类访问的方法：身份验证和授权。你可以使用不同的标准来控制对网站各部分的访问，包括检查客户端的 IP 地址或主机名，或要求用户名和密码。本节简要介绍其中一些方法。

> CAUTION
>
> 允许个人用户将 Web 内容放在你的服务器上会带来几个重要的安全风险。如果你是在 Internet 而非私有网络上运行 Web 服务器，你应该阅读 WWW 安全常见问题解答 http://www.w3.org/Security/Faq/www-security-faq.html。

## 使用 allow 和 deny 限制访问

限制对网站材料的访问的最简单方法之一是根据 IP 地址或主机名限制对特定用户组的访问。Apache 使用 `allow` 和 `deny` 指令来实现这一点。

这两个指令都将地址表达式作为参数。以下列表提供了地址表达式的可能值和用法：

- `all` 可用于影响所有主机。
- 主机名或域名，可以是部分限定或完全限定域名；例如，`test.gnulix.org` 或 `gnulix.org`。
- IP 地址，可以是完整或部分；例如，`212.85.67` 或 `212.85.67.66`。
- 网络/网络掩码对，例如 `212.85.67.0/255.255.255.0`。
- 以无类别域间路由（CIDR）格式指定的网络地址；例如，`212.85.67.0/24`。这是前一个示例中使用的相同网络和网络掩码的 CIDR 表示法。

你也可以使用 `allow` 和 `deny` 来根据特定环境变量是否存在与否来提供或拒绝对网站材料的访问。例如，下面的语句拒绝包含名为 `NOACCESS` 的环境变量的上下文的请求访问：

```
deny from env=NOACCESS
```

Apache 的默认行为是先应用所有 `deny` 指令，然后再检查 `allow` 指令。如果你想改变这个顺序，可以使用 `order` 语句。Apache 可能以三种不同的方式解释此语句：

+   `Order deny,allow`—`deny` 指令在 `allow` 指令之前被评估。如果主机未被明确拒绝访问，则允许其访问资源。这是如果未指定其他内容时的默认排序。
+   `Order allow,deny`—所有 `allow` 指令在 `deny` 指令之前被评估。如果主机未被明确允许访问，则拒绝其访问资源。
+   `Order mutual-failure`—只有同时在 `allow` 指令中指定并且在同一时间未出现在 `deny` 指令中的主机才被允许访问。如果主机未出现在任一指令中，则不授予访问权限。

考虑这个例子。假设你只想允许来自你自己域内的人员访问你的网页上的 `server-status` 资源。如果你的域名为 `gnulix.org`，你可以在配置文件中添加以下行：

```
<Location /server-status>
SetHandler server-status
Order deny,allow
Deny from all
Allow from gnulix.org
</Location>
```

## Authentication

`Authentication` 是确保访客确实是他们声称的那个人身份的过程。你可以配置 Apache 仅允许能够验证其身份的客户端访问特定网页内容区域。Apache 中有几种身份验证方法；`Basic Authentication` 是最常见的方法，也是本章讨论的方法。
