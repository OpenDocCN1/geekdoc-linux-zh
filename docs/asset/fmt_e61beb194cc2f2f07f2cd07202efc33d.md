
Apache 2 的默认配置启用基于名称的虚拟主机。此外，默认虚拟主机定义在 `/etc/apache2/sites-enabled/000-default.conf` 文件中；如果未找到匹配客户端发送请求的主机，将使用此虚拟主机。

> **重要**
>
> 涉及未知虚拟主机的请求总是由第一个定义的虚拟主机处理，这就是为什么软件包附带了一个 `000-default.conf` 配置文件，它在你可能创建的所有其他文件中排在第一位。

然后，每个额外的虚拟主机由存储在 `/etc/apache2/sites-available/` 中的文件描述。该文件通常以网站的域名加上 `.conf` 后缀命名（例如：`www.example.com.conf`）。然后你可以使用 `a2ensite www.example.com` 启用新的虚拟主机。这是一个针对文件存储在 `/srv/www.example.com/www/` 的网站的最小 virtualhost 配置（使用 *DocumentRoot* 选项定义）：

```apache
<VirtualHost *:80>
    ServerName www.example.com
    ServerAlias example.com
</VirtualHost>
```

```
DocumentRoot /srv/www.example.com/www
</VirtualHost>
```

你可能还需要考虑添加 `CustomLog` 和 `ErrorLog` 指令，以配置 Apache 将日志输出到专门用于该虚拟主机的文件中。

### 常用指令

本节简要回顾了一些常用的 Apache 配置指令。主配置文件通常包含多个 `Directory` 块；它们允许根据所服务文件的位置为服务器指定不同的行为。这样的块通常包含 `Options` 和 `AllowOverride` 指令：

```
<Directory /var/www>
Options Includes FollowSymlinks
AllowOverride All
DirectoryIndex index.php index.html index.htm
</Directory>
```

`DirectoryIndex` 指令包含一个文件列表，当客户端请求匹配一个目录时，会依次尝试这些文件。列表中第一个存在的文件将被使用并作为响应发送。

`Options` 指令后面跟着一个要启用的选项列表。`None` 值禁用所有选项；相应地，`All` 启用除 `MultiViews` 之外的所有选项。可用的选项包括：

- `ExecCGI`——指示可以执行 CGI 脚本。
- `FollowSymlinks`——告知服务器可以跟随符号链接，并且响应应包含此类链接目标的内容。
- `SymLinksIfOwnerMatch`——也告知服务器跟随符号链接，但仅当链接及其目标具有相同的拥有者时。
- `Includes`——启用服务器端包含（SSI）。这些是嵌入在 HTML 页面中的指令，并为每个请求即时执行。
- `Indexes`——告知服务器，如果客户端发送的 HTTP 请求指向一个没有索引文件的目录（即，当此目录中不存在 `DirectoryIndex` 指令中提到的文件时），则列出该目录的内容。
- `MultiViews`——启用内容协商；服务器可以使用此功能返回与浏览器中配置的偏好语言匹配的网页。

### 要求身份验证

在某些情况下，需要限制对网站部分内容的访问，因此仅授予提供了用户名和密码的合法用户访问内容的权限。

`.htaccess` 文件包含 Apache 配置指令，每次请求涉及存储 `.htaccess` 文件所在的目录中的元素时，这些指令都会强制执行。这些指令是递归的，将作用域扩展到所有子目录。

`Directory` 块中可出现的大多数指令在 `.htaccess` 文件中也是合法的。`AllowOverride` 指令列出了所有可以通过 `.htaccess` 启用或禁用的选项。此选项的一个常见用途是限制 `ExecCGI`，以便管理员选择允许哪些用户在 web 服务器的身份（`www-data` 用户）下运行程序。

#### 示例 5.3 要求身份验证的 `.htaccess` 文件

```
Require valid-user
AuthName "Private directory"
AuthType Basic
AuthUserFile /etc/apache2/authfiles/htpasswd-private
```

| **基本身份验证不提供安全性** | 上述示例中使用的身份验证系统（基本身份验证）安全性极低，因为密码是以明文形式发送的（它只是被编码为 base64，这是一种简单的编码方法，而非加密方法）。还应注意，通过此机制保护的文件在网络传输时也是明文的。如果安全性很重要，整个 HTTP 会话应使用传输层安全性（TLS）进行加密。 |

|---|---|

`/etc/apache2/authfiles/htpasswd-private` 文件包含一个用户和密码列表；它通常使用 `htpasswd` 命令进行操作。例如，以下命令用于添加用户或更改其密码：

```
##### htpasswd /etc/apache2/authfiles/htpasswd-private user
New password:
Re-type new password:
Adding password for user user
```

### 限制访问

`Require` 指令控制目录（及其子目录，递归地）的访问限制。

它可以用于根据许多标准限制访问；我们将仅描述基于客户端 IP 地址的访问限制，但它可以更强大，特别是当多个 `Require` 指令在 `RequireAll` 块中组合使用时。

例如，你可以使用以下指令将访问限制在本地网络：

```
Require ip 192.168.0.0/16
```

## 5.4. 管理服务

Kali 使用 `systemd` 作为其 init 系统，它不仅负责启动序列，还永久地充当全功能的服务管理器，启动并监控服务。`systemd` 可以通过 `systemctl` 进行查询和控制。不带任何参数时，它运行 `systemctl list-units` 命令，输出活动单元列表。如果你运行 `systemctl status`，输出将显示正在运行的服务的层次概览。比较这两个输出，你会立即发现有多种类型的单元，而服务只是其中之一。

每个服务由一个 *服务单元* 表示，该单元由服务文件描述，通常放置在 `/lib/systemd/system/` 中（或 `/run/systemd/system/`，或 `/etc/systemd/system/`；它们按重要性递增顺序列出，最后一个优先）。每个服务单元可能通过同一组目录中的其他 `service-name.service.d/*.conf` 文件进行修改。这些单元文件是纯文本文件，其格式借鉴了众所周知的 Microsoft Windows 的 `*.ini` 文件，在 `[section]` 头之间分组 `key = value` 对。在这里，我们看到了 `/lib/systemd/system/ssh.service` 的一个示例服务文件：

```
[Unit]
Description=OpenBSD Secure Shell server
After=network.target auditd.service
ConditionPathExists=!/etc/ssh/sshd_not_to_be_run

[Service]
EnvironmentFile=-/etc/default/ssh
ExecStart=/usr/sbin/sshd -D $SSH_OPTS
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=on-failure
RestartPreventExitStatus=255
Type=notify

[Install]
WantedBy=multi-user.target
Alias=sshd.service
```

目标单元是 systemd 设计的另一部分。它们表示你想在激活单元方面达到的期望状态（对于服务单元而言，这意味着正在运行的服务）。它们主要作为对其他单元依赖性的分组方式而存在。当系统启动时，它会启用达到 `default.target` 所需的单元（`default.target` 是指向 `graphical.target` 的符号链接，而后者依赖于 `multi-user.target`）。因此，这些目标的所有依赖项都会在启动过程中被激活。
