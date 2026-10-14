
例如，当用户请求页面 `http://www.example.com/this_directory/` 时，如果存在 `DirectoryIndex` 页面，他将获得该页面；如果不存在且指定了 `Indexes` 选项，则获得一个生成的目录列表；如果两者都不满足，则将显示“拒绝访问”（Permission Denied）。服务器将尝试寻找 `DirectoryIndex` 指令中列出的文件之一，并返回找到的第一个文件。如果没有找到任何这些文件，并且该目录设置了 `Options Indexes`，服务器将生成并返回一个 HTML 格式的目录下的子目录和文件列表。在 `/etc/apache2/mods-available/dir.conf` 中找到默认值为 `"index.html index.cgi index.pl index.php index.xhtml index.htm"`。因此，如果 Apache 在请求的目录中找到匹配任何名称的文件，它将显示该文件。

- `ErrorDocument` 允许你指定一个供 Apache2 用于特定错误事件的文件。例如，如果用户请求一个不存在的资源，将发生 404 错误代码。有关使用 `ErrorDocument` 的细节（包括示例文件的位置），请阅读 `/etc/apache2/conf-available/localized-pages.conf`。
- 某些选项是按目录指定的，而不是按服务器指定的。`Options` 是这些指令之一。`Directory` 块包含在类似 XML 的标签中，如下：

```
<Directory>
  /var/www/html/mymysite
</Directory>
```

`Directory` 块中的选项接受以下一个或多个值（此外还有其他值），并用空格分隔：

- `ExecCGI` - 允许执行 CGI 脚本。如果没有选择此选项，则不会执行 CGI 脚本。

## Caution 注意事项

大多数文件不应作为 CGI 脚本执行。这将非常危险。CGI 脚本应保留在你的 `DocumentRoot` 之外的独立目录中，并且只有该目录应该具有 `ExecCGI` 选项。这是默认设置，且 CGI 脚本的默认位置是 `/usr/lib/cgi-bin`。

- `Includes` - 允许服务器端包含。服务器端包含在 HTML 文件中包含其他文件。更多信息请参见 SSI 文档（Ubuntu 社区）。
- `IncludesNOEXEC` - 允许服务器端包含，但禁用 CGI 脚本中的 `#exec` 和 `#include` 命令。
- `Indexes` - 如果请求的目录中不存在 `DirectoryIndex`（如 `index.html`），则显示目录内容的列表。

## Caution 注意事项

出于安全考虑，通常不设置此项，且绝对不应在你的 `DocumentRoot` 上设置。只有当你确定想看到目录的全部内容时，才按目录谨慎地启用此选项。

- `Multiview` - 支持内容协商的多重视图；出于安全考虑，此选项默认禁用。请参见 Apache 2 关于此选项的文档。
- `SymLinksOwnerMatch` - 仅当目标文件或目录的所有者与链接相同时，才允许符号链接。

## apache2 Settings apache2 设置

本部分解释了一些 apache2 守护进程配置设置。

`LockFile` - `LockFile` 指令设置了服务器在带有 `USE_FCNTL_SERIALIZED_ACCEPT` 或 `USE_FLOCK_SERIALIZED_ACCEPT` 编译时使用的锁文件路径。它必须存储在本地磁盘上。除非日志目录位于 NFS 共享上，否则应保持默认值。

`PidFile` - `PidFile` 指令设置服务器记录进程 ID (pid) 的文件。该文件应仅对 `root` 可读。在大多数情况下，应保持默认值。

`User` - `User` 指令设置服务器响应请求的用户 ID。此设置决定了服务器的访问权限。任何该用户可以访问的文件对访问者都是可见的。`User` 的默认值为 `www-data`。

**Warning 警告**

除非你清楚自己在做什么，否则不要将 `User` 指令设置为 `root`。使用 `root` 作为用户会为你的 Web 服务器造成巨大的安全漏洞。

`Group` - `Group` 指令与 `User` 指令类似。`Group` 设置服务器响应请求的组。默认组为 `www-data`。

`mod_ssl` 模块可在 `apache-common` 包可用。在终端提示符下执行以下命令来启用 `mod_ssl` 模块：

`sudo aenmod ssl`

在 `/etc/apache2/sites-available/default-ssl.conf` 中有一个 HTTPS 配置文件。为了让 Apache 提供 HTTPS，还需要证书和密钥文件。默认的 HTTPS 配置将使用由 `ssl-cert` 包生成的证书和密钥。为了测试，应该将自动生成的证书和密钥替换为特定站点或服务器的证书。有关生成密钥和获取证书的信息，请参阅证书（Certificates）。

要为 Apache 配置 HTTPS，请输入以下内容：

`sudo a2ensite default-ssl`

### 注意

目录 `/etc/ssl/certs` 和 `/etc/ssl/private` 是默认位置。如果您将证书和密钥安装在任何其他目录，请确保相应地更改 `SSLCertificateFile` 和 `SSLCertificateKeyFile`。

现在 Apache 已配置为 HTTPS，请重启服务以启用新设置：

```
sudo systemctl restart apache2.service
```

### 注意

取决于您获取证书的方式，当 Apache2 启动时，您可能需要输入密码。

您可以通过在浏览器地址栏中输入 `https://your_hostname/url/` 来访问安全服务器页面。

# 共享写入权限

如果需要多个用户写入同一个目录，则有必要向他们共同的组授予写入权限。以下示例向 `webmasters` 组授予了 `/var/www/html` 的写入权限：

```
sudo chown -R webmasters /var/www/html
sudo chmod -R g=wx /var/www/html/
```

这些命令递归地设置 `/var/www/html` 中所有文件和目录的组权限，允许对目录进行读取、写入和搜索。许多管理员发现这对允许多个用户编辑目录树中的文件非常有用。

### 警告

Apache2 进程以 `www-data` 用户身份运行，该用户有一个相应的 `www-data` 组。不应授予文档根目录写入权限，因为这将导致 Apache 或其提供的应用程序中的漏洞允许攻击者覆盖所提供的内容。

### 参考文献

- Apache 文档包含有关 Apache 配置指令的详细信息。另请查看 `apache-2-doc` 包以获取官方 Apache 文档。
- 《O’Reilly’s Apache Cookbook》是实现特定 Apache2 配置的良好资源。
- 针对 Ubuntu 的特定 Apache2 问题，请在 freenode.net 的 `#ubuntu-server` IRC 频道提问。

# Web 服务器

Web 服务器的主要功能是向客户端存储、处理和交付 Web 页面。客户端通过发送 HTTP 请求与服务器通信。客户端主要通过浏览器请求特定资源，服务器响应该资源的内容或错误消息。响应通常是一个 Web 页面，因为 HTML 文档可能包含图像、样式表、脚本以及表单内容。

访问 Web 服务器时，收到的每个 HTTP 请求都会响应内容和一个 HTTP 状态码。HTTP 状态码为三位数，分为五类。可以通过状态码的第一位数字快速识别其类别：

- 1xx: 信息性 - 请求已接收，继续处理
- 2xx: 成功 - 操作已被成功接收、理解并接受
- 3xx: 重定向 - 必须采取后续操作以完成请求
- 4xx: 客户端错误 - 请求包含错误的语法或无法实现
- 5xx: 服务器错误 - 服务器未能执行看似有效的请求

有关状态码检查的更多信息，请查看 RFC 2016。

# 实现

Web 服务器在 Web 站部署中被广泛使用，在这种场景下我们可以使用两种不同的实现：

- 静态 Web 服务器：服务器响应的内容将是“原样”的文件。
- 动态 Web 服务器：由 Web 服务器加上额外的软件（通常是应用程序服务器和数据库）组成。例如，为了生成你在浏览器中看到的 Web 页面，应用程序服务器可能会用数据库的内容填充 HTML 模板。因此，我们说服务器响应的内容是动态生成的。

# 高可用性简介

来自维基百科对高可用集群的定义：

# 高可用集群

高可用性集群（也称为 HA 集群、故障转移集群或 Metroclusters Active/Active）是支持服务器应用程序的计算机组，这些应用程序可以以最少的停机时间可靠地运行。
