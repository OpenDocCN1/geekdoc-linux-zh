
| `mod_usertrack` | 使用 cookie 跟踪用户通过网站浏览的进度。 |

| `mod_vhost_alias` | 包含对动态配置的大规模虚拟主机的支持。 |

有关每个模块（以及可以在其中定义的指令）的更多信息可以在我们位于 `http://localhost/manual/mod/` 的服务器上找到。

### 设置主服务器配置

`http.conf` 文件的第二部分涉及由主服务器处理的指令。换句话说，除非在虚拟主机定义中进行了更改，否则这些值在所有情况下都有效。要为特定的虚拟主机更改相同的指令，请将它们添加在虚拟主机容器内。

#### 选择服务器的用户和组

`httpd` 守护进程不必以 root 用户身份运行；实际上，如果它不以 root 身份运行，系统的安全性会更高。通过设置 `User` 和 `Group` 条目，您可以让 `httpd` 守护进程使用与不同用户和组关联的权限运行。

```
# 如果您希望 httpd 以不同的用户或组运行，您必须
# 最初以 root 身份运行 httpd，然后它会进行切换。
#
```

# 第四部分：Fedora 网络和服务器设置

```
# User/Group：以该用户/组运行 httpd 的名称（或 #数字）。
#       . 在 SCO (ODT 3) 上使用 "User nouser" 和 "Group nogroup"。
#       . 在 HP-UX 上，您可能无法以 nobody 身份使用共享内存，
#       建议的变通方法是创建一个用户 www 并使用该用户。
# 请注意，某些内核拒绝在 (unsigned)Group 的值超过 60000 时
# 设置 setgid(Group) 或 semctl(IPC_SET)；
# 在这些系统上不要使用 Group #-1！
#
User apache
Group apache
```

默认情况下，`apache` 被定义为服务器的用户和组。如果您更改 `User` 和 `Group` 指令，应指定一个非特权实体。这可以将站点被入侵时的损坏风险降至最低。启动的第一个守护进程以 root 身份运行。这是必要的，以便将服务器绑定到低编号端口，并切换到由 `User` 和 `Group` 指令指定的用户和组。所有其他进程都在这些指令定义的用户 ID `UID` 和组 ID `GID` 下运行。

#### 选择 HTTP 端口号

Apache 在特定端口上监听 HTTP 请求。使用的端口由 `Port` 条目设置如下：

```
# Port：独立服务器监听的端口。对于
# 端口 < 1023，您需要最初以 root 身份运行 httpd。
#
Port 80
```

端口 80 是 HTTP 流量的默认值，这就是为什么 `http://www.apache.org:80/` 与 `http://www.apache.org/` 相同的原因。如果服务器绑定到不同的端口，则必须在 URL 中指定端口号。大多数 Web 服务器运行在端口 80 上，尽管它们可以接受任何未绑定到特定服务的端口（最高 65535）的连接（有关常见服务和协议及其使用端口的列表，请参阅 `/etc/services` 文件）。只有 root 才能运行监听特权端口（1024 以下端口）上连接的程序。

#### 设置电子邮件地址

您可以指定一个地址，以便当服务器出现问题时用户可以创建电子邮件。这是通过 `ServerAdmin` 指令完成的：

```
# ServerAdmin：您的地址，服务器出现问题的电子邮件发送处。
# 该地址显示在服务器生成的某些页面上，例如
# 错误文档，例如 admin@your-domain.com
#
ServerAdmin you@your.address
```

## `ServerAdmin` 指令

`ServerAdmin` 指令可以设置为任何有效的电子邮件地址。默认值为 `root@localhost`。

#### 设置服务器名称

如果你的服务器名称不是确切的注册主机名或域名，你应该在此处指定你的服务器名称。正如注释所述，`ServerName` 指令可以设置为除机器实际主机名以外的值。但是，如果服务器要作为公共互联网服务器，该其他名称仍应在 DNS 中指向该机器。通常，`www` 只是机器真实名称的别名（例如，机器可能响应 `www.linuxtoys.net`，但其真实名称可能是 `al.linuxtoys.net`）。

```
ServerName juicebox.linuxtoys.net
```

如果你没有输入有效的服务器名称，Apache 会尝试使用你的主机名作为 `ServerName`。建议在此处显式输入 `ServerName`。

#### 设置规范名称

使用 `UseCanonicalName` 指令创建自引用 URL，如下所示：

```
# UseCanonicalName: 确定 Apache 如何构造自引用
# URL 以及 SERVER_NAME 和 SERVER_PORT 变量。
# 当设置为 "Off" 时，Apache 将使用客户端提供的
# 主机名和端口。当设置为 "On" 时，Apache 将使用
# ServerName 指令的值。
#
UseCanonicalName Off
```

`UseCanonicalName` 指令提供了一致性的命名方式。当设置为 `On` 时，Apache 使用 `ServerName` 和 `Port` 指令创建引用同一机器上文件的 URL（例如，`http://www.linuxtoys.net/docs/`）。当 `UseCanonicalName` 为 `Off` 时，URL 由客户端指定的任何内容组成（例如，如果客户端在同一域名内，URL 可以是 `http://al.linuxtoys.net/docs/` 或 `http://al/docs/`）。

这可能存在问题，特别是在访问控制规则要求用户名和密码验证时：如果客户端已获得主机 `al.linuxtoys.net` 的验证，但链接将其发送到 `www.linuxtoys.net`（物理上是同一台机器），客户端将被提示再次输入用户名和密码。建议将 `UseCanonicalName` 设置为 `On`。在前述情况下，无需重复验证，因为对同一服务器的任何引用始终会被解释为 `www.linuxtoys.net`。

#### 标识 HTTP 内容目录

有几个指令用于确定服务器 Web 内容的位置。主要 Web 内容位置由 `DocumentRoot` 指令设置为 `/var/www/html`。（注意，此位置自 Red Hat Linux 7 之前的版本起已更改。以前的位置在 `/home/http`。）

```
# DocumentRoot: 你将从该目录提供文档。
# 默认情况下，所有请求都来自该目录，但
# 可以使用符号链接和别名指向其他位置。
DocumentRoot "/var/www/html"
```

#### 设置访问选项和覆盖

你可以为 Web 服务器目录结构中的每个目录设置单独的访问权限。默认值相当严格。以下是默认设置：

```
<Directory />
  Options FollowSymLinks
  AllowOverride None
</Directory>
```

此部分为 `Options` 和 `AllowOverride` 指令设置了一组默认的权限块。`<Directory />…</Directory>` 标签包围了应用于 `/` 目录（默认为 `/var/www/html`，由 `DocumentRoot` 定义）的指令。

`Options FollowSymLinks` 指令指示服务器该目录内的符号链接可以被跟踪，以允许位于计算机其他位置的内容。如果没有在后续明确指定，`/ `目录或其下的任何目录中的其他特殊服务器功能都将处于非活动状态。接下来，为你的 Web 服务器根目录（`/var/www/html`）具体设置了以下访问选项。（为了清晰起见，我去掉了这里的注释。）

```
<Directory "/var/www/html">
  Options Indexes FollowSymLinks
  AllowOverride None
  Order allow,deny
  Allow from all
</Directory>
```

如果你在此文件中较早的位置更改了 `DocumentRoot` 的值，你需要将 `/var/www/html` 更改为与那个值匹配。该目录设置的 `Options` 为 `Indexes` 和 `FollowSymLinks`。这些以及其他特殊服务器功能在表 21-2 中有描述。`AllowOverride None` 指令指示服务器 `.htaccess` 文件（或 `AccessFileName` 的值）不能覆盖任何特殊访问功能。你可以用表 21-3 中描述的任何特殊访问功能替换 `None`。

> 注意：请记住，除非你明确启用了表 21-2 和 21-3 中描述的功能，否则该功能在你的服务器上未启用（`Indexes` 和 `FollowSymLinks` 除外）。
