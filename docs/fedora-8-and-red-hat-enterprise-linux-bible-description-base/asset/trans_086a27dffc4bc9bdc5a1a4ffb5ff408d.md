
## HTTP 模块表

| 模块 | 描述 |
| :--- | :--- |
| mod_negotiation | 根据 Content-Encoding、Content-Language、Content-Length 和 Content-Type HTTP 标头字段，提供基于条件的文档显示功能。 |
| mod_proxy | 实现 HTTP 1.1 代理/网关服务器。 |
| mod_proxy_ajp | 使用 mod_proxy 提供对 Apache JServ Protocol（版本 1.3）的支持。 |
| mod_proxy_balancer | 扩展 mod_proxy 以处理负载均衡。 |
| mod_proxy_connect | 扩展 mod_proxy 以处理 CONNECT 请求。 |
| mod_proxy_ftp | 扩展 mod_proxy 以处理 FTP 请求。 |
| mod_proxy_http | 扩展 mod_proxy 以处理 HTTP 请求。 |
| mod_rewrite | 提供一种灵活且可扩展的方法来重定向客户端请求，并将传入的 URL 映射到文件系统其他位置。 |
| mod_setenvif | 根据各种 HTTP 标头字段的内容有条件地设置环境变量。 |
| mod_speling | 尝试自动纠正请求 URL 中的拼写错误。 |
| mod_ssl | 使用 SSL 和 TLS 协议实现加密。 |
| mod_status | 提供每个 httpd 服务器进程活动摘要，包括 CPU 和带宽使用级别。 |
| mod_suexec | 允许 CGI 脚本以特定用户或组的权限运行。 |
| mod_unique_id | 为每个请求分配 UNIQUE_ID 环境变量以提供唯一标识符。 |
| mod_userdir | 指定可以包含各个用户 HTML 文档的位置。 |
| mod_usertrack | 使用 cookie 跟踪用户通过网站浏览的进度。 |
| mod_version | 允许您使用 `<IFVersion>` 容器来实现版本依赖的配置。 |
| mod_vhost_alias | 包含对动态配置的大规模虚拟主机的支持。 |

有关每个模块（以及其中可以定义的指令）的更多信息，可以在您的服务器上的 `http://localhost/manual/mod/` 找到。

### 包含模块特定的配置文件

以下行使 Apache 从 `/etc/httpd/conf.d` 目录加载配置文件。此目录包含与特定模块相关的配置文件。

```
#
# Load config files from the config directory "/etc/httpd/conf.d".
#
Include conf.d/*.conf
```

> **交叉引用：** 本章后面部分的“配置模块和相关服务 (\etc/httpd/conf.d/\*.conf\*)”一节描述了一些 `conf.d` 目录中您可能感兴趣的配置文件。

### 选择服务器的用户和组

`httpd` 守护进程不必作为 *root* 用户运行；默认情况下不作为 *root* 运行这一事实使您的系统更加安全。通过设置 *User* 和 *Group* 条目，您可以让 `httpd` 守护进程使用与不同用户和组相关的权限运行：

```
# If you wish httpd to run as a different user or group, you must run
# httpd as root initially and it will switch.
#
# User/Group: The name (or #number) of the user/group to run httpd as.
#  . On SCO (ODT 3) use "User nouser" and "Group nogroup".
#  . On HP-UX you may not be able to use shared memory as nobody, and
#    the suggested workaround is to create a user www and use that user.
# NOTE that some kernels refuse to setgid(Group) or setuid(IPC_SET)
# when the value of (unsigned)Group is above 60000;
# don't use Group #-1 on these systems!
#
User apache
Group apache
```

默认情况下，*apache* 被定义为服务器的用户和组。如果您更改 *User* 和 *Group* 指令，应该指定一个非特权实体。这可以将网站被入侵时造成损害的风险降到最低。启动的第一个守护进程以 *root* 身份运行。这是将服务器绑定到低编号端口以及切换到由 *User* 和 *Group* 指令指定的用户和组所必需的。所有其他进程都在由这些指令定义的用户 ID (UID) 和组 ID (GID) 下运行。

### 设置主服务器配置

`httpd.conf` 文件的第二部分涉及由您的主服务器（由 *ServerName* 指令定义的那个）处理的指令。换句话说，除非明确为虚拟主机更改，否则这些值用于默认服务器和所有虚拟主机。要为特定的虚拟主机更改相同的指令，请将这些指令添加到虚拟主机容器中。

### 设置电子邮件地址

您可以识别一个地址，以便用户在服务器出现问题时发送电子邮件。这是通过 `ServerAdmin` 指令完成的：

```
# ServerAdmin: your address, where problems with the server should be
# e-mailed.  This address appears on some server-generated pages, such
# as error documents. e.g. admin@your-domain.com
#
ServerAdmin you@your.address
```

`ServerAdmin` 指令可以设置为任何有效的电子邮件地址。默认值是 `root@localhost`。

### 设置服务器名称

如果您的服务器名称不是确切的已注册主机或域名，您应该在此处标识您的服务器名称。正如注释所指出的，`ServerName` 指令可以设置为机器实际主机名以外的值。但是，如果服务器要是公共互联网服务器，则此其他名称在 DNS 中仍应指向您的机器。通常，www 只是机器真实名称的别名（例如，机器可能响应 `www.linuxtoys.net`，但其真实名称可能是 `al.linuxtoys.net`）。

```
ServerName jukebox.linuxtoys.net
```

如果您没有输入有效的服务器名称，Apache 会尝试使用您的主机名作为 `ServerName`。建议在此处显式输入一个 `ServerName`。

### 设置规范名称

使用 `UseCanonicalName` 指令来创建自引用 URL，如下所示：

```
# UseCanonicalName: Determines how Apache constructs self-referencing
# URLs and the SERVER_NAME and SERVER_PORT variables.
# When set "Off", Apache will use the Hostname and Port supplied
# by the client.  When set "On", Apache will use the value of the
# ServerName directive.
#
UseCanonicalName Off
```

`UseCanonicalName` 指令提供了一致性命名形式。当设置为 On 时，Apache 使用 `ServerName` 和 `Port` 指令创建引用同一台机器上文件的 URL（例如，`http://www.linuxtoys.net/docs/`）。当 `UseCanonicalName` 为 `Off` 时，URL 由客户端指定的任何内容组成（例如，如果客户端在同一域内，URL 可以是 `http://al.linuxtoys.net/docs/` 或 `http://al/docs/`）。

这可能有问题，特别是当访问控制规则需要用户名和密码身份验证时：如果客户端针对主机 `al.linuxtoys.net` 进行了身份验证，但链接将其引导到 `www.linuxtoys.net`（物理上是同一台机器），客户端将再次被提示输入用户名和密码。建议将 `UseCanonicalName` 设置为 `On`。在前述情况下，由于对同一服务器的任何引用始终被解释为 `www.linuxtoys.net`，因此无需重复身份验证。

### 标识 HTTP 内容目录

有几个指令用于确定服务器 Web 内容的位置。您的 Web 内容的主位置由 `DocumentRoot` 指令设置为 `/var/www/html`。（注意此位置已从 Red Hat Linux 的早期版本中更改。位置以前在 `/home/httpd` 中。）

```
# DocumentRoot: The directory out of which you will serve your
# documents. By default, all requests are taken from the directory, but
# symbolic links and aliases may be used to point to other locations.
DocumentRoot "/var/www/html"
```

### 设置访问选项和覆盖

您可以为 Web 服务器目录结构中的每个目录设置单独的访问权限。默认值相当严格。以下是默认设置：

```
<Directory />
   Options FollowSymLinks
        AllowOverride None
</Directory>
```

此段设置了 `Options` 和 `AllowOverride` 指令的默认权限块。`<Directory />` … `</Directory>` 标签包裹了将应用于 `/` 目录的指令（默认情况下是 `/var/www/html`，由 `DocumentRoot` 定义）。

`Options FollowSymLinks` 指令指示服务器可以跟踪目录中的符号链接，以允许访问位于计算机其他位置的内容。如果没有明确指定，`/` 目录或该目录下的任何目录中都不会激活其他特殊服务器功能。接下来，以下访问选项专门为您的 Web 服务器根目录 (`/var/www/html`) 设置。（此处去除了注释以提高清晰度。）

```
<Directory "/var/www/html">
   Options Indexes FollowSymLinks
        AllowOverride None
        Order allow,deny
        Allow from all
</Directory>
```

如果在此文件中之前更改了 `DocumentRoot` 的值，您需要将 `/var/www/html` 更改为与该值匹配。目录的 `Options` 设置为 `Indexes` 和 `FollowSymLinks`。这些以及其他特殊服务器功能在表 21-2 中有描述。

