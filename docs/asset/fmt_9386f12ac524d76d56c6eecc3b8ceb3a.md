
上下文：服务器配置，虚拟主机，目录，`.htaccess`
默认值：无；仅列出文件名
Fedora/RHEL：`FancyIndexing` `VersionSort` `NameWidth=*` `HTMLTable` `CharSet=UTF-8`

`ServerRoot` 指定服务器文件的根目录（不是容器）。

`ServerRoot directory`

其中 `directory` 指定了构成服务器文件的根目录路径。Apache 在 `httpd.conf` 中的相对路径前加上 `directory`。此指令不指定 Apache 服务的内容的位置；`DocumentRoot` 指令（第 928 页）执行该功能。除非移动了服务器文件，否则不要更改此值。

上下文：服务器配置
默认值：`/usr/local/apache`
Fedora/RHEL：`/etc/httpd`

## 942 第 26 章 APACHE (httpd): 设置 Web 服务器

`ServerTokens` 用于指定 Apache 返回给客户端的服务器信息。

`ServerTokens Prod | Major | Minor | Min | OS | Full`

- `Prod`: 返回产品名称：Apache；也返回 `ProductOnly`。
- `Major`: 返回服务器的主版本号：Apache/2。
- `Minor`: 返回服务器的主版本和次版本号：Apache/2.2。
- `Min`: 返回完整版本号：Apache/2.2.16；也返回 `Minimal`。
- `OS`: 返回操作系统的版本和完整版本号：Apache/2.2.16 (Fedora)。相比 `Full`，它提供的更少可能帮助恶意用户的信息。
- `Full`: 与 `OS` 相同，但 `Full` 还会发送非 ASF 模块的名称和版本：Apache/2.2.16 (Fedora) PHP/5.2.14。

除非你想了解正在运行的软件的细节，否则将 `ServerTokens` 设置为尽可能少泄露信息。

- 上下文：服务器配置 (server config)
- 默认值：`Full`
- Fedora/RHEL：`OS`

`ServerSignature` 在服务器生成的页面中添加一行。

`ServerSignature On | Off | EMail`

- `On`: 开启签名行。签名行包含由 `ServerTokens` 指令（上文）指定的服务器版本以及由 `<VirtualHost>` 容器（第 934 页）指定的名称。
- `Off`: 关闭签名行。
- `EMail`: 在签名行中添加指向服务器邮箱地址的 `mailto:` 链接。此选项产生的输出可能会吸引垃圾邮件。有关指定电子邮件地址的信息，请参阅 `ServerAdmin`（第 927 页）。

- 上下文：服务器配置 (server config), 虚拟主机 (virtual host), 目录 (directory), `.htaccess`
- 默认值：`Off`
- Fedora/RHEL：`On`

## 配置指令

`Group` 设置运行服务器的进程的 GID。

`Group #groupid | groupname`

其中 `groupid` 是 GID 值，前面带有 `#`，`groupname` 是组的名称。Apache 派生的进程（服务器）将以此指令指定的组组的身份运行。更多信息请参阅 `User` 指令（第 944 页）。

- 上下文：服务器配置 (server config)
- 默认值：`#1`
- Fedora/RHEL：`apache`

`Include` 从文件中加载指令。

`Include filename | directory`

其中 `filename` 是包含指令的文件的相对路径。Apache 在 `filename` 前面加上 `ServerRoot`（第 941 页）。`filename` 中的指令将被包含在持有此指令的文件中，位于指令所在的位置。由于 `filename` 可以包含通配符，它可以指定多个文件。

`directory` 是相对路径，用于指定包含指令文件的目录层次结构的根目录。Apache 在 `directory` 前加上 `ServerRoot`。普通文件中的指令将被包含在持有此指令的文件中，位于指令所在的位置。`directory` 可以包含通配符。

当你安装 Apache 及其模块时，rpm 将扩展名为 `.conf` 的配置文件放在 `ServerRoot` 目录下的 `conf.d` 目录中。在 Apache/RHEL/RHEL `httpd.conf` 文件中的 `Include` 指令包含了已安装模块的模块文件。

- 上下文：服务器配置 (server config), 虚拟主机 (virtual host), 目录 (directory)
- 默认值：none
- Fedora/RHEL：`conf.d/*.conf`

`LoadModule` 加载模块。

`LoadModule module filename`

其中 `module` 是外部 DSO 模块的名称，`filename` 是命名模块的相对路径。Apache 在 `filename` 前面加上 `ServerRoot`（第 941 页）并加载此指令指定的外部模块。更多信息请参阅第 957 页的“Modules”。

- 上下文：服务器配置 (server config)
- 默认值：none；如果省略此指令，默认不加载任何内容
- Fedora/RHEL：加载了 40 多个模块；列表请参阅 `httpd.conf`

`Options` 控制你目录的服务器功能。

`Options [|option [|option ...`

此指令控制为目录层次结构启用哪些服务器功能。该指令控制目录层次结构中启用了哪些服务器功能。

- `None`：该目录层次结构禁用了所有功能。
- `All`：该目录层次结构启用了所有功能。
- `ExecCGI`：允许执行 CGI 脚本。
- `FollowSymLinks`：允许跟踪符号链接。
- `Indexes`：生成目录列表。
- `MultiViews`：允许内容视图。

根据你的需求，将 `Options` 设置为以启用或禁用特定的功能。

（第 932 页）展示了如何防止 Apache 服务于 `.ht` 开头的文件内容。

`指令类（directive-class）` 是以下指令类标识符之一：

`AuthConfig`—控制授权的指令类（`AuthName`、`AuthType` 等）。此类指令主要用于 `.htaccess` 文件，要求使用用户名和密码才能访问内容。欲需更多信息，请参阅第 961 页的“身份验证模块与 .htaccess”。

`FileInfoN`—控制文档类型的指令类（`DefaultType`、`Error-Document`、`SetHandler` 等）。

`Indexes`—与目录索引相关的指令类（`DirectoryIndex`、`Fancy-Indexing`、`Options` 等）。

`Limit`—客户端访问指令类（`Allow`、`Deny` 和 `Order`）。

`Options`—控制目录特性的指令类。

上下文：目录
默认值：全部
Fedora/RHEL：无

`Deny` 指定哪些客户端不允许访问指定的内容。

`Deny from All | host [host ...] \ env=var [env=var ...]`

该指令必须写为 `Deny`，用于拒绝指定的客户端访问目录结构。该目录结构由该指令所在的容器或 `.htaccess` 文件指定。示例请参阅 `Order` 指令（下文）。

`All`—拒绝所有客户端访问内容。

`host`：拒绝由 `host` 指定客户端访问内容，`host` 可以采取多种形式：全限定域名 (FDN)、部分域名（例如 `example.com`）、IP 地址、部分 IP 地址或网络/子网掩码值对。

`var`：当环境变量 `var` 被设置时，拒绝访问内容。你可以使用 `SetEnvIf` 指令设置变量。

上下文：`.htaccess`
默认值：无
Fedora/RHEL：无

`Order` 指定默认的访问方式以及 `Allow` 和 `Deny` 指令的评估顺序。

`Order,Allow|Allow` 默认允许访问；仅拒绝在 `Deny` 指令中指定的客户端访问（首先评估 `Deny` 指令，然后评估 `Allow` 指令）。

# FEDORA/RHEL httpd.conf 文件 947

`Allow,Deny`—默认拒绝访问；仅允许在 `Allow` 指令中指定的客户端访问（首先评估 `Allow` 指令，然后评估 `Deny` 指令）。

逗号两侧不能有空格。如果没有匹配当前客户端的 `Allow from` 或 `Deny from` 指令，则访问默认为配对中的第二个项目（`Deny,Allow` 默认为 `Allow`）。如果只有一个 `Allow from` 或 `Deny from` 指令匹配客户端，则该指令将覆盖默认设置。如果有多个 `Allow` 和 `Deny from` 指令匹配客户端，Apache 将按照 `Order` 指令中的顺序评估指令；最后一个匹配的项具有优先级。

由此指令授予或拒绝的访问适用于该指令所在的容器或 `.htaccess` 文件指定的目录结构。Fedora/RHEL 默认设置为 `Allow,Deny`，这会拒绝所有未通过 `Allow` 指令指定的客户端访问，`httpd.conf` 中的下一条指令 `Allow from all` 则授予所有客户端访问权限：

```
Order allow,deny
Allow from all
```

你可以通过指定 `Deny,Allow` 来拒绝所有访问，然后仅对你想要授予访问权限的客户端指定 `Allow` 指令。以下指令授予了来自 `example.net` 域的客户端访问权限，且这些指令通常只出现在 `<Directory>` 容器内（第 931 页）：

```
Order deny,allow
Deny from all
Allow from .example.net
```

上下文：目录，`.htaccess`
默认值：`Deny,Allow`
Fedora/RHEL：`Allow,Deny`（针对 `/var/www/html`）

# FEDORA/RHEL httpd.conf 文件

本节重点介绍了 Fedora/RHEL `httpd.conf` 文件的一些重要特性，该文件基于 Apache 分发的 `httpd.conf` 文件。这个带有详尽注释的文件被分为以下部分（本节也是如此）：

- 1. 全局环境—控制 Apache 服务器的整体功能。
- 2. 主服务器配置—配置默认服务器（相对于虚拟主机），并为虚拟主机提供默认配置信息。
- 3. 虚拟主机—配置虚拟主机（第 953 页）。

# 第 1 own：全局环境

`ServerTokens` `ServerTokens` 指令（第 942 页）被设置为 `OS`，这导致 Apache 在被查询时返回操作系统的名称和 Apache 的完整版本：

```
ServerTokens OS
```

`ServerRoot` `ServerRoot` 指令（第 941 页）设置为 `/etc/httpd`，这是 Apache 附加到 `httpd.conf` 中相对路径后的路径名：

```
ServerRoot "/etc/httpd"
```

`<IfModule>` `<IfModule>` 容器（第 932 页）允许你在不同的多进程处理模块（MPMs，第 962 页）中使用相同的 `httpd.conf` 文件。只有在指定的模块被加载时，Apache 才会执行 `<IfModule>` 容器中的指令。`httpd.conf` 文件包含 `<IfModule>` 容器，根据加载了哪个模块（prefork 或 worker）来配置配置 Apache。Fedora/RHEL 自带了 prefork 模块；本节不讨论 worker 模块的 `<IfModule>` 容器。（worker 模块不兼容 PHP。如果你想加载 worker 模块，请查看 `/etc/sysconfig/httpd` 文件中的注释。）

# prefork MPM
