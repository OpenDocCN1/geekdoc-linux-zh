
`Options FollowSymLinks`

`AllowOverride None`

```
</Directory>
```

`UserDir` - 如果您启用了 `mod_user`，您可以允许系统用户在您的服务器上拥有自己的网站。默认情况下，只有在使用 `IfModule` 设置安装了 `mod_user` 模块时可以使用这些指令：

```
<IfModule mod_userdir.c>
UserDir public_html
</IfModule>
```

系统用户的示例如下：

```
http://www.yourdomain.com/~username
```

用户的网站文件将位于其家目录下的名为 `public_html` 的子目录中。

`DirectoryIndex files` - `DirectoryIndex` 指令定义了默认显示的页面。例如，目前被定义为如果存在 `index.html` 则加载 `index.html`。

这是我们认为 Apache 配置中默认经常配置不当的指令之一。每当我们设置 Apache Web 服务器时，都必须修改此设置。我们添加了 `index.htm`、`default` 以及其他。

```
<IfModule mod_dir.c>
DirectoryIndex index.html
</IfModule>
```

`AccessFileName .htaccess` - `AccessFileName` 是放置在目录内部的文件名，允许您控制对文件的访问。`AccessFileName` 必须以点（`.`）开头。

```
<Files ".ht">
Order allow,deny
Deny from all
Satisfy All
</Files>
```

`ServerSignature On` `ServerSignature` 设置允许在从外部源请求错误文档时，显示服务器类型、版本以及可能的某些配置选项。我们认为显示这些信息可能存在安全风险，因此将其关闭。

`Alias /icons/ /* /www/icons/*` `Alias` 指令允许你将文件和目录存储在 `DocumentRoot` 之外，然后将它们别名映射到网站中。

`ScriptAlias /cgi-bin/ /* /www/cgi-bin/*` `ScriptAlias` 与 `Alias` 非常相似，不同之处在于此处定义的目录被认为是是可执行的，例如 `cgi-bin`。

`IndexOptions FancyIndexing` `IndexOptions` 指令允许当 `DirectoryIndex` 中列出的文件不可用，以图标的形式显示目录内容。默认启用此选项不是一个好主意，应该在 `Directory` 选项中显式定义 `FancyIndexing`。

`NameVirtualHost *` `NameVirtualHost` 是一个用于允许基于名称的虚拟主机的指令。我们使用简单的 `*` 作为值来启用它。我们将在稍后的“配置 Apache 虚拟主机”部分中讨论这一点。

`VirtualHost` 虚拟主机允许你在单台机器和单个 IP 地址或多个 IP 地址上运行多个网站。我们将在稍后的“配置 Apache 虚拟主机”部分中讨论。

## 使用 Apache 虚拟主机

Apache 具有一个非常优秀的内置功能，称为虚拟主机。此功能允许你从同一服务器托管多个域名，并为所有虚拟主机使用单个 IP 地址，或者将一组主机分配给一个 IP 地址同时将另一组分配给不同的 IP 地址，以此此类推。这种灵活的功能的设计良好且可配置。事实上，虚拟主机使托管公司能够以很小的开销将许多客户端打包到一台机器上。

Apache 的虚拟主机功能非常广泛；事实上，在本章中无法列出所有功能。以下是你可能在书中用到的最重要功能列表：

- 基于 IP 或基于名称的虚拟主机
- 每个主机可以有自己的 `DocumentRoot`
- 每个主机都有独立的日志记录
- 能够使用 `ScriptAlias` 和 `Alias` 指令在虚拟主机之间共享目录
- 允许按目录或虚拟主机设置覆盖选项

## 使用 Apache 虚拟主机 229

当使用启用 SSL 的虚拟主机时，你必须考虑一些事情。首先，你必须为每个 SSL 虚拟主机准备一个独立的 IP 地址或每个 IP 地址一个 SSL 端口。如果你决定使用不同的端口，必须在 URL 中指定端口——例如，如果你使用备用端口 `444`，则为 `https://www.yoursite.com:444`。其次，你可以使用单个 IP 地址配合一个 SSL 虚拟主机和多个非 SSL 虚拟主机。SSL 虚拟主机超本书的范围，因此如果你想了解更多关于它们的信息，请检查 `httpd.conf` 示例或阅读 `mod_ssl` 文。

## 虚拟主机支持的指令

我们已经提到 Apache 虚拟主机是高度可配置的；因此，在本节中，我们将提供一个可以在虚拟主机使用的指令列表。如果你感兴趣了解更多这些指令，请阅读开头的“配置 Apache 虚拟主机”部分，并参考本章前面的“Apache 1.3 功能”部分。

以下是 Apache 虚拟主机中记录可用指令列表：

- `AccessConfig`
- `AccessFileName`
- `ContentDigest`
- `<Directory>`
- `<DirectoryMatch>`
- `DocumentRoot`
- `EBCDICConvert`
- `EBCDICConvertByType`
- `EBCICludge`
- `ErrorDocument`
- `ErrorLog`
- `FileTag`
- `<Files>`
- `<FilesMatch>`
- `<Group>` (需要安装 `suEXEC`)
- `HostnameLookups`
- `IdentityCheck`
- `LimitInternalRecursion`

## 第 8 章 • Apache Web 服务器：安装与配置

- `LimitRequestBody`
- `<Location>`
- `<LocationMatch>`
- `LogLevel`
- `Options`
- `ResourceConfig`
- `RLimitCPU`
- `RLimitMEM`
- `RLimitNPROC`
- `ServerAdmin`
- `ServerAlias`
- `ServerName`
- `ServerPath`
- `ServerSignature`
- `UseCanonicalName`
- `User` (需要安装 `suEXEC`)
- 让在配置 Apache 虚拟主机时使用这些指令。

## 配置 Apache 虚拟主机

现在是时候计划和配置你的虚拟主机了。到本节结束时，你将非常熟悉 Apache Web 服务器的设计有多精良且灵活。

### 有 DNS 吗？

在这个示例中，我们假设你有两个域名，并且 DNS 已设置到你服务器的 IP 地址。如果你没有设置 DNS 或者你不拥有任何域名，你可以简单地编辑系统的 `hosts` 文件，欺骗你的系统为你的服务器 IP 地址解析一个虚假名称。

在 Linux 上，`HOSTS` 文件位于 `/etc/hosts`，你需要向其中添加以下行，假设你服务器的 IP 地址是 `123.456.789.1`。

> 此处使用的 IP 地址是虚构的，在真实服务器上无效。你必须用 `123.456.789.1` 替换为你真实的 IP 地址！

```
123.456.789.1 yourdomain.com www.yourdomain.com
123.456.789.1 yourotherdomain.com www.yourotherdomain.com
```

在 Windows 系统上，你应该在 `C:\Windows` 目录中搜索名为 `hosts` 的文件。它通常位于 `C:\Windows\System32\Drivers\etc\hosts`。在此文件中，你将添加以下行：

```
123.456.789.1 yourdomain.com www.yourdomain.com
123.456.789.1 yourotherdomain.com www.yourotherdomain.com
```

（注：后续重复的 Windows 路径说明已在翻译中简化，保持逻辑一致）

### 准备工作

在开始深入配置之前，你需要准备系统。遵循以下步骤：

1. 创建目录：

```
mkdir /www/conf/vhosts
```

2. 现在你创建了：

```
mkdir -p /home/www/yourdomain.com/public_html
mkdir -p /home/www/yourdomain.com/logs
mkdir -p /home/www/yourotherdomain.com/public_html
mkdir -p /home/www/yourotherdomain.com/logs
```

3. 修改 `httpd.conf` 文件以包含你将创建的目录；向其中添加以下行：

```
include conf/vhosts
```

4. 因为你正在编辑 `httpd.conf` 文件，你需要为你的虚拟主机启用另一个设置。找到 `NameVirtualHost` 行并移除注释符号 `#`，将其改为：

```
NameVirtualHost *
```
