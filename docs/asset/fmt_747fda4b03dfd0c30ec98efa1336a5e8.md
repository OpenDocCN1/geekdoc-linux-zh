
ServerName 设置了服务器将返回的主机名。将其设置为完全限定域名名 (fqdn)。将其设置为 `www.rcowen.com` 而不是简单的 `www`。如果这台机器可以从互联网访问而不是从本地网络访问，这一点尤为重要。除非你想让返回一个与机器规范名称不同的名称，否则无需设置此项。如果未设置此值，服务器将自行确定名称并将其设置为其规范名称。然而，你可能希望服务器返回一个更友好的地址，例如 `www.yourdomain`。无论你怎么做，`serverName` 应该是你网络中的真实域名系统 (DNS) 名称。如果你在管理自己的 DNS，请记住为你的主机添加一个别名。如果由其他人为你管理 DNS，请要求他们为你设置此名称。

## DocumentRoot（文档根目录）

将此设置为文档树的绝对路径，即 Apache 提供服务的顶级目录。默认情况下，它设置为 `/home/http/html`，或者如果你自己编译了源码，设置为 `/usr/local/apache/htdocs`。在 1.3.4 版本之前，此指令出现在 `srm.conf` 中。

## UserDir（用户目录）

此指令定义了相对于本地用户主目录的目录，用户可以在其中发布 HTML 文档。它是相对的，因为每个用户将有他们自己的 HTML 目录。此指令的默认设置为 `public_html`。因此，每个用户都可以在其家目录下创建一个名为 `public_html` 的目录，放置在该目录中的 HTML 文档将可以通过 `http://servername/-username` 访问，其中 `username` 是特定用户的用户名。在 1.3.4 版本之前，此指令出现在 `srm.conf` 中。

## DirectoryIndex（目录索引）

`DirectoryIndex` 指令指示了哪个文件应该作为目录的索引提供，例如当请求 `http://www.server.com/Directory/` URL 时，应该提供哪个文件。在此处列出文件列表通常很有用，这样在未找到 `index.html`（默认值）时，可以提供另一个文件作为替代。这最有用的应用是让一个 CGI 程序作为目录中的默认操作运行。在这种情况下，该指令看起来像是 `DirectoryIndex index.html.cgi`。在 1.3.4 版本之前，此指令出现在 `srm.conf` 中。

# Configuring Services（配置服务）

第 II 部分

## Caution（注意事项）

允许单个用户在你的服务器上放置 Web 内容涉及若干个重要的安全考量。如果你在互联网上而非私有网络上运行 Web 服务器，你应该阅读 `http://www.mit.edu/cgi/faqs/security.html` 上的安全 FAQ。

## .htaccess Files and Access Restrictions（htaccess 文件与访问限制）

几乎任何出现在配置文件中的目录都可以出现在 `.htaccess` 文件中。该文件在 `httpd.conf` 中（1.3.4 之前为 `srm.conf`）指定，按目录设置配置。作为系统管理员，你可以指定此文件的名称以及哪些服务器配置可以被覆盖。要限制 `.htaccess` 文件可以覆盖的内容，你需要使用 `AllowOverride` 指令。

## Options Directives（选项指令）

`Options` 可以是 `None`、`All` 或 `Indexes`、`Includes`、`FollowSymLinks`、`ExecCGI` 或 `MultiViews` 的任意组合。`MultiViews` 不包含在 `All` 中，必须式指定。这些选项解释如下：

- `None`: 该目录禁用了所有可用选项。
- `All`: 该目录启用了除 `MultiViews` 之外的所有可用选项。
- `Indexes`: 在缺少 `index.html` 文件或其他 `DirectoryIndex` 文件的情况下，将生成目录列表作为 HTML 页面供用户显示。
- `Includes`: 此目录允许服务器包含 (SSI)。如果你想允许包含但不想在这些包含中使用 `exec` 选项，可以写成 `Includes+Exec`。出于安全考虑，这在你不具备控制权的目录（如 `UserDir` 目录）中通常是一个好主意。
- `FollowSymLinks`: 允许访问链接到文档目录的目录。这通常是一个坏主意，你不应该为整个服务器全局设置此项。你可能希望为单个目录设置此项，但仅在你有充分理由的情况下才这样做。该选项是一个潜在的安全风险，因为它允许 Web 用户离开文档目录，并可能允许他们访问文件系统中你极不希望人们窥探的部分。

# 配置服务

第二部分

此目录允许执行 `ExecCGI` CGI 程序，即使该目录不是一个配置了 `ScriptAlias` 的目录也是如此。

`MultiViews`（多视图）这是 `mod_negotiation` 模块的一部分。当客户端请求的文档未找到时，服务器会尝试确定哪个文档最符合客户端的需求。请参阅 `http://www.apache.org/docs/mod/mod_negotiation.html` 或您本地 Apache 文档副本中的相同文档。

> 注意

这些指令也会影响所指定目录的所有子目录。

# AllowOverrides 指令

`AllowOverrides` 指令指定了 `.htaccess` 文件可以覆盖哪些选项。您可以针对每个目录设置此项。例如，您可以对主文档根目录和 `UserDir` 目录中“可以被覆盖的内容”设置不同的标准。

此功能对于用户目录特别有用，因为用户没有访问主服务器配置文件的访问权限。

`AllowOverrides` 可以设置为 `All`（全部）或 `Options`、`FileInfo`、`AuthConfig` 和 `Limit` 的任意组合。这些选项在下表中进行了解释。

- `Options`：`.htaccess` 文件可以添加该目录 `Options` 指令中 `Options` 指令中未列出的选项。
- `FileInfo`：`.htaccess` 文件可以包含修改文档类型信息的指令。
- `AuthConfig`：`.htaccess` 文件可能包含授权指令。
- `Limit`：`.htaccess` 文件可能包含 `allow`（允许）、`deny`（拒绝）和 `order`（排序）指令。

# 虚拟主机

Web 服务器提供的常用服务之一是托管虚拟域名，也称为虚拟主机。这是一个拥有自己域名的完整网站，就像一台独立的机器一样，但它与其它网站一起被托管在同一台机器上。Apache 通过 `http.conf` 配置文件中的指令以简单的方式实现了这一功能。

# Apache 服务器

第 9 章

在 Apache 服务器上托管虚拟主机有两种方法。您可以使用一个 IP 地址对应多个 CNAME，或者使用多个 IP 地址对应一个名称地址。Apache 具有不同的指令集来处理这每种选项。

> 注意

有关如何为您的 Linux 机器配置多个 IP 地址或为您的 Linux 机器提供多个 CNAME 的信息，请参阅第 11 章“DNS”。

# 基于地址的虚拟主机

一旦您为 Linux 机器配置了多个 IP 地址，设置 Apache 将它们作为不同的网站提供就非常简单。您只需要在 `httpd.conf` 文件中为您想要作为独立网站的地址放置一个 `virtualHost` 指令：

```
<VirtualHost www.virtual.com>
ServerName www.virtual.com
DocumentRoot /home/virtual/public/html
TransferLog /home/virtual/logs/access_log
ErrorLog /home/virtual/logs/error_log
</VirtualHost>
```

建议在 `VirtualHost` 标签中使用 IP 地址，而不是主机名。

您可以在 `<VirtualHost>` 标签内指定任何配置指令。例如，您可能想直接为虚拟主机设置 `AllowOverrides` 指令，而不是为主服务器设置。任何不设认为主服务器默认设置的指令都可以单独设置。

在 `VirtualHost` 节中不能设置的指令包括：`ServerType`、`StartServers`、`MaxSpareServers`、`MinSpareServers`、`MaxRequestsPerChild`、`BindAddress`、`Listen`、`PidFile`、`TypesConfig`、`ServerRoot` 和 `NameVirtualHost`。

# 基于名称的虚拟主机

基于名称的虚拟主机允许您在同一个 IP 地址上运行多个主机。您需要向 DNS 中添加额外的名称作为该机器的 CNAME。当 HTTP 客户端（浏览器）从您的服务器请求文档时，它会在请求中发送一个变量，指示其请求文档的服务器名称。根据此变量，服务器将决定从哪个虚拟主机提供内容。

![](img/fbfff30e42d507bc7531108a281d6cf4_302_0.png)

# 配置服务

第二部分

> 注意
