
> Apache 配置了一个别名，允许你通过浏览器访问 `localhost/manual` 查看安装在 `/usr/share/doc` 中的文档。在安装并启动 Apache 后，你可以在 `https://localhost/manual/mod/directives.html` 找到指令索引。

## 编辑 apache2.conf

配置文件中的大多数默认设置都可以保留，特别是如果你在默认位置安装了服务器，并且没有在服务器上进行任何不寻常的操作。该文件包含了描述大多数设置的注释。通常情况下，如果你不理解特定指令的用途，请将其保留为默认值。

以下章节描述了你可能想要根据服务器运行情况而更改的一些配置文件设置。

### ServerRoot

`ServerRoot` 指令设置服务器目录的绝对路径。此指令告诉服务器在何处查找所有资源和配置文件。许多此类资源在配置文件中是相对于 `ServerRoot` 指令指定的。

如果你安装的是 Ubuntu 软件包，你的 `ServerRoot` 指令应设置为 `/etc/apache2`；如果是从源码安装的，则设置为 `/etc/local/apache`（取决于你使用 Apache 时选择的任何目录）。这在文件中已有注释，但 `apache2 -V` 显示此默认值已编译到包中。

### Listen

`Listen` 指令实际上位于名为 `ports.conf` 的文件中，该文件由 `apache2.conf` 包含，它指示了你希望服务器在哪个端口上运行。默认情况下，它设置为 80，即标准的 HTTP 端口号。你可能希望在另一个端口上运行服务器——例如，运行一个你不希望人们意外发现的测试服务器。不要将此与真正的安全混淆！请参阅本章后面的“文件系统认证与访问控制”章节，获取有关如何保护 Web 服务器部分的更多信息。

### User and Group

`User` 和 `Group` 指令应设置为服务器处理请求时使用的 UID 和 GID。

在 Ubuntu 中，将这些配置设置为一个权限很少或没有权限的用户。在这种情况下，它们被设置为用户 `www-data`（专门为运行 Apache 而定义的用户）和组 `www-data`。如果你想使用不同的 UID 或 GID（root 以外），服务器将以此处设置的用户和组的权限运行。这意味着，一旦发生安全违规（无论是在服务器上还是在你的组中，更有可能是在你自己的 CGI 程序中），这些程序都将以分配的 UID 运行。如果服务器以 root 或其他特权用户运行，

### ServerAdmin

`ServerAdmin` 指令应该是 Web 管理员地址。该地址应该是一个有效的电子邮件地址，例如 `webmaster@example.com`。

### ServerName

`ServerName` 指令设置服务器的主机。它应该是一个完全限定域名（FQDN），例如 `www.example.com`。无论你如何设置，`ServerName` 应该是一个真实的名称。

### DocumentRoot

`DocumentRoot` 指令设置你的文档树的绝对路径，即 Apache 提供服务的顶级目录。默认情况下，它设置为 `/var/www/`。如果你构建了源码且没有选择编译 Apache 的其他目录，则 `DocumentRoot` 被设置为 `/usr/local/apache/htdocs`。

### UserDir

`UserDir` 指令启用或定义目录（相对于用户的 `/home/username` 目录），该用户可以在其中放置 HTML 文档。该指令的默认设置为 `public_html`。

### DirectoryIndex

`DirectoryIndex` 指令指示哪个文件应该作为目录的索引提供，例如当请求 `http://servername/SomeDirectory/` URL 时，应该提供哪个文件。

在此列出文件列表通常很有用，因为如果找不到 `index.html`（默认值），就可以提供另一个文件。此项最有用的应用程序是将 CGI 程序作为目录的默认操作。如果你使用的用户在 Windows 上制作网页，你可能可能也想添加 `index.html`。在这种情况下，指令看起来如 `DirectoryIndex index.html .cgi index.htm`。

与 Linux 相关的内部 MPM 模块包括：

- `mpm_common`—一组所有 MPM 模块通用的 20 条指令
- `prefork`—一个多线程、预取型的 Web 服务器，其工作方式与 Apache 早期 (1.3) 版本非常相似
- `worker`—一个混合多进程多线程的服务器

MPM 使得 Apache 能够运行在资源较少的设备上，同时仍能处理海量访问并提供稳定的服务。`worker` 模块提供了指令，用于控制您的服务器可以同时处理多少连接。

> 注意
>
> Apache 还提供了适用于其他平台的其他 MPM，例如用于 NetWare 的 `mpm_network` 和用于 NT 平台的 `mpm_winnt`。一个名为 `perchild` 的 MPM 正在开发中，它提供为选定的守护进程分配用户 ID的功能。如需更多信息，请访问 Apache 软件基金会主页：www.apache.org。

# 使用 .htaccess 配置文件

Apache 支持特殊的配置文件，称为 `.htaccess` 文件。几乎任何出现在 `apache2.conf` 中的直接层级指令（direct directive）都可以出现在 `.htaccess` 文件中。该文件由 `apache2.conf` 中的 `AccessFileName` 指令指定，基于目录（通常是用户目录）设置配置。作为系统管理员，您可以指定此文件的名称，以及服务器配置中的哪些内容可以被该文件的覆盖。这对于拥有多个内容提供者的站点特别有用，因为您想要控制这些人在其空间内可以的操作。

要限制哪些服务器文件可以被覆盖，请使用 `AllowOverride` 指令。`AllowOverride` 可以全局设置，也可以按目录设置。例如，在您的 `apache2.conf` 文件中，可以使用以下内容：

```
# Apache 能够访问的每个目录都可以根据该
# 目录中允许或禁用的服务和功能进行配置
#（以及该目录（及其子目录）。
#
# 首先，我们将“默认”值配置为一组非常严格的权限。
#
<Directory />
  Options FollowSymLinks
  AllowOverride None
</Directory>
```

# 运行时服务器配置设置

## Options 指令

为了配置 Apache 默认提供的配置选项，您必须使用 `Options` 指令。`Options` 可以是 `None`；`All`；或者 `Indexes`、`Includes`、`FollowSymLinks`、`ExecCGI` 和 `MultiViews` 的任意组合（`All` 不包含这些，必须显式指定）。这些选项在表 25.2 中解释。

表 25.2 `Options` 指令使用的开关

| 开关 | 描述 |
| --- | --- |
| None | 此目录未启用任何可用选项。 |
| Indexes | 在缺少 `index.html` 文件或另一个 `DirectoryIndex` 文件的情况下，将生成目录下的文件列表并作为 HTML 页面显示给用户。 |
| Includes | 此目录允许服务器端包含 (SSI)。如果您想允许包含但不想允许 `exec` 选项，也可以写为 `IncludesNoExec`。出于安全考虑，在您没有完全控制权的目录中（如 `UserDir`）这样做这是一个好主意。 |
| FollowSymLinks | 此选项允许访问链接到文档目录的目录。您不应为服务器全局设置此选项，且极少为单个目录设置。此选项存在潜在的安全风险，因为它允许 Web 用户逃离文档目录，并可能允许访问您不希望被窥探的文件系统的部分。 |
| ExecCGI | 此目录允许运行 CGI 程序，即使它不是由 `Script` 指令定义的目录。 |
| MultiViews | 这是 `mod_negotiation` 模块的一部分。当客户端请求一个找不到文档时，服务器会尝试找出最符合客户端要求的文档。 |

> 注意
>
> 这些指令也会影响指定目录的所有子目录。

## AllowOverrides 指令

`AllowOverrides` 指令指定了 `.htaccess` 文件可以覆盖哪些配置选项。您可以为每个目录单独设置 `AllowOverrides`。例如，您可以对主文档根目录和 `UserDir` 目录中可以被覆盖的内容设置不同的标准。这种功能对于用户目录特别有用，因为用户没有权限访问主服务器配置文件。

`AllowOverrides` 可以设置为 `All` 或 `Options`、`FileInfo`、`AuthConfig` 和 `Limit` 的任意组合。这些选项在表 25.3 中解释。

# 表 25.3 `AllowOverrides` 指令使用的开关

| 开关 | 描述 |
| --- | --- |
