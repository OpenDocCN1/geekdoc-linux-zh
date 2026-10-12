
```
<Directory "/var/www/html">
    Options Indexes FollowSymLinks
...
</Directory>
```

上下文：`directory`

默认值：All

Fedora/RHEL：Indexes FollowSymLinks

### ScriptAlias

将 URI 映射到目录或文件，并声明目标是一个服务器（CGI）脚本。

`ScriptAlias alias pathname`

其中 `alias` 必须匹配客户端请求以调用 ScriptAlias 的 URI 的一部分，而 `pathname` 是别名的目标的绝对路径名，通常是一个目录。类似于 `Alias` 指令，此指令指定目标是 CGI 脚本（第 877 页）。

Fedora/RHEL `httpd.conf` 文件中的以下 `ScriptAlias` 指令将包含 `/cgi-bin/` 的客户端请求映射到 `/var/www/cgi-bin` 目录（并指示这些请求将被视为 CGI 请求）：

```
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"
```

上下文：`server config`, `virtual host`

默认值：无

Fedora/RHEL：/cgi-bin/ "/var/www/cgi-bin"

### User

设置运行服务器的进程的 UID。

`User #userid | username`

其中 `userid` 是 UID 值，前面带有 # 号，而 `username` 是本地用户的名称。Apache 派生的进程（服务器）将以该指令指定的用户身份运行。

Apache 必须以 `root` 身份启动以监听特权端口。出于安全原因，Apache 的子进程（服务器）以非特权用户身份运行。默认 UID –1 在 Fedora/RHEL 下不对应用户。相反，Fedora/RHEL 的 `httpd` 包在安装期间创建一个名为 `apache` 的用户，并将 User 设置为该用户。

上下文：`server config`

默认值：#-1

Fedora/RHEL：apache

**请勿将 User 设置为 root 或 0**

`security` 为了获得更安全的系统，请勿将 User 设置为 `root` 或 `0`（零），并且不要允许 `apache` 用户对 DocumentRoot 目录层级具有写入权限（存储数据所需的除外），尤其是不要对配置文件具有写入权限。

## SECURITY DIRECTIVES

### Allow

指定哪些客户端可以访问指定内容。

`Allow from All | host [host ...] | env=var [env=var ...]`

必须将其写为 `Allow from` 的此指令，授予指定客户端访问目录层级的权限。目录层级由包含此指令的容器或 .htaccess 文件指定。

- `All`：向任何客户端提供内容。
- `host`：向由 `host` 指定的客户端提供内容，`host` 可以有多种形式：`host` 可以是 FQDN、部分域名（例如 `example.com`）、IP 地址、部分 IP 地址或网络/掩码对。
- `var`：当名为 `var` 的环境变量被设置时提供内容。您可以使用 `SetEnvIf` 指令设置变量。请参阅 `Order` 指令（第 870 页）获取示例。

上下文：`directory`, `.htaccess`

默认值：无；默认行为取决于 `Order` 指令

Fedora/RHEL：All

### AllowOverride

指定在 `.htaccess` 文件中允许使用的指令类别。

`AllowOverride All | None | directive-class [directive-class ...]`

此指令指定 Apache 是否读取由其容器指定的目录层级中的 `.htaccess` 文件。如果 Apache 确实读取 `.htaccess` 文件，则此指令指定在 `.htaccess` 文件内哪些类型的指令是有效的。

- `None`：忽略 `.htaccess` 文件。
- `All`：允许在 `.htaccess` 文件中使用所有类别的指令。

`directive-class` 是以下指令类别标识符之一：

- `AuthConfig`：控制授权（AuthName, AuthType, Require 等）的指令类别。此类主要用于 `.htaccess` 文件中，要求输入用户名和密码才能访问内容。有关更多信息，请参阅第 880 页的“Authentication Modules and `.htaccess`”。
- `FileInfo`：控制文档类型（DefaultType, ErrorDocument, SetHandler 等）的指令类别。
- `Indexes`：与目录索引（DirectoryIndex, FancyIndexing, IndexOptions 等）相关的指令类别。
- `Limit`：客户端访问指令（Allow, Deny 和 Order）的类别。
- `Options`：控制目录功能的指令类别。

上下文：`directory`

默认值：All

Fedora/RHEL：None

### Deny

指定哪些客户端不允许访问指定内容。

`Deny from All | host [host ...] | env=var [env=var ...]`

必须将其写为 `Deny from` 的此指令，拒绝指定客户端访问目录层级。目录层级由包含此指令的容器或 `.htaccess` 文件指定。请参阅 `Order` 指令（第 870 页）获取示例。

`All`：拒绝所有客户端访问内容。
`host`：拒绝由`host`指定的客户端访问内容。`host`可以是FQDN、部分域名（例如`example.com`）、IP地址、部分IP地址，或者网络/掩码对。
`var`：当名为`var`的环境变量被设置时，拒绝访问内容。你可以使用`SetEnvIf`指令设置变量。

- 上下文：`directory`、`.htaccess`
- 默认值：无
- Fedora/RHEL：无

`Order` 指定默认访问权限以及`Allow`和`Deny`指令的评估顺序。

```
Order Deny,Allow | Allow,Deny
```

`Deny,Allow`：默认允许访问；仅拒绝在`Deny`指令中指定的客户端访问。（先评估`Deny`指令，然后评估`Allow`指令。）

`Allow,Deny`：默认拒绝访问；仅允许在`Allow`指令中指定的客户端访问。（先评估`Allow`指令，然后评估`Deny`指令。）

通过此指令授予或拒绝的访问权限适用于该指令所在的容器或`.htaccess`文件中指定的目录层次结构。

逗号两侧不得有空格。尽管Fedora/RHEL的默认值为Allow,Deny，即拒绝所有未由Allow指令指定的客户端访问，但`httpd.conf`中的下一个指令`Allow from all`允许所有客户端访问：

```
Order allow,deny
Allow from all
```

通过指定Deny,Allow来拒绝所有访问，然后仅在Allow指令中指定你想要授予访问权限的客户端，从而限制访问。以下指令仅授予`example.net`域中客户端的访问权限，通常出现在`<Directory>`容器中（第855页）：

```
Order deny,allow
Deny from all
Allow from .example.net
```

- 上下文：`directory`、`.htaccess`
- 默认值：Deny,Allow
- Fedora/RHEL：Allow,Deny

## Fedora/RHEL httpd.conf 文件

本节重点介绍了Fedora/RHEL `httpd.conf`文件的一些重要功能，该文件基于Apache分发的`httpd.conf`文件。这个注释详尽的文件分为以下几个部分（本节也如此划分）：

- 1. 全局环境——控制Apache服务器的整体运行。
- 2. 主服务器配置——配置默认服务器（区别于虚拟主机），并为虚拟主机提供默认配置信息。
- 3. 虚拟主机——配置虚拟主机。更多信息请参阅第874页的“Virtual Hosts”。

### 第1节：全局环境

`ServerTokens` `ServerTokens`指令（第865页）设置为OS，这会导致Apache在受到查询时返回操作系统的名称和Apache的完整版本号：

```
ServerTokens OS
```

`ServerRoot` `ServerRoot`指令（第865页）设置为/etc/httpd，这是Apache在httpd.conf中相对路径名之前添加的路径。
