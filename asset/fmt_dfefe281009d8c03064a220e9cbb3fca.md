
# ServerName dummy-host.example.com

# ErrorLog logs/dummy-host.example.com-error_log

# CustomLog logs/dummy-host.example.com-access_log

#</VirtualHost>

```

该示例列出了虚拟主机指令，允许您在同一台计算机上托管 `handsonhistory.com` 和 `linuxtoys.net` 域名：

`NameVirtualHost *:80`

```apache
<VirtualHost *:80>

DocumentRoot /var/www/handsonhistory

ServerName www.handsonhistory.com

ServerAlias handsonhistory.com

ServerAdmin webmaster@handsonhistory.com

ErrorLog logs/handsonhistory.com-error_log

CustomLog logs/handsonhistory.com-access_log

</VirtualHost>
```

```apache
<VirtualHost *:80>

DocumentRoot /var/www/linuxtoys

ServerName www.linuxtoys.net

ServerAlias linuxtoys.net

ServerAdmin webmaster@linuxtoys.net

ErrorLog logs/linuxtoys.net-error_log

CustomLog logs/linuxtoys.net-access_log

</VirtualHost>
```

为了测试虚拟主机，你可以将新主机名添加到本地的 `/etc/hosts` 文件中，并指向你的本地 IP 地址。例如：

```
127.0.0.1        www.linuxtoys.net
```

如果你看到了你为虚拟主机设置的内容，而不是 Fedora 错误页面或你设置的默认内容，那么你可能已经正确设置了虚拟主机。

## 配置模块及相关服务
(`/etc/httpd/conf.d/*.conf`)

任何需要特殊配置的模块通常会在 `/etc/httpd/conf.d/` 目录下有一个配置文件（`.conf`）。该目录下可能包含一些模块化配置文件，以及使用这些文件和相关包的某些方法（使用 `yum install package` 安装你需要的每个包）：

- `auth_kerb.conf` — 在 Web（HTTP）连接上配置 Kerberos 身份验证。该文件中的示例建议在 SSL 连接上使用 Kerberos 认证。（安装 `mod_auth_kerb` 包）。
- `auth_mysql.conf` — 根据你用于 MySQL 数据库的数据配置身份验证。文件中的注释描述了如何设置数据库并在允许客户端访问你的 Web 内容之前使用它进行用户或组身份验证。（安装 `mod_auth_mysql` 包）。
- `auth_pgsql.conf` — 基于 PostgreSQL 配置认证。（安装 `mod_auth_pgsql` 包）。
- `auth_ldap.conf` — 基于 LDAP 配置认证。（安装 `mod_auth_ldap` 包）。
- `htidig.conf` — 配置认证文件的位置。（安装 `mod_auth_htidig` 包）。
- `mailman.conf` — 设置邮件列表。（安装 `mod_auth_mailman` 包）。
- `manual.conf` — 定义手册的位置。（安装 `mod_auth_manual` 包）。
- `mrtg.conf` — 跟踪流量。（安装 `mod_auth_mrtg` 包）。
- `perl.conf` — 允许 Perl 脚本。（安装 `mod_auth_perl` 包）。
- `php.conf` — 配置 PHP。（安装 `mod_auth_php` 包）。
- `python.conf` — 加载 Python 模块。（安装 `mod_auth_python` 包）。

## 启动和停止服务器

启动和停止 Apache 服务器的过程与其他许多守护进程相同。你可以使用 `chkconfig` 命令设置 `httpd` 服务器在启动时运行。

> **交叉引用：** 请参第 12 章获取有关控制启动和停止守护进程的脚本的详细信息。

`/etc/init.d/httpd` 脚本接受以下命令行参数。如果使用 `start` 参数调用，`httpd` 脚本将运行一个主守护进程（由 root 所有），该进程将产生由 `StartServers` 指令指定的数量的其他守护进程（由 apache 用户所有，取决于 `User` 和 `Group` 指令）。这些进程负责响应传入的 HTTP 请求。如果使用 `stop` 调用，由于所有 `httpd` 进程被终止，服务器将关闭。

给定命令行参数 `restart`，脚本将按顺序执行停止和启动程序。使用 `reload` 参数将向主 `httpd` 守护进程发送挂起信号（`-HUP`），导致使其重新读取配置文件并重启所有其他 `httpd` 守护进程。该脚本还支持 `status` 参数，它将报告守护进程是否运行，如果正在运行，则显示运行的 PID。

进程。所有其他命令行参数都将导致错误并打印用法信息。

Apache 的实际二进制文件 `/usr/sbin/httpd` 支持多个命令行参数，尽管通常会使用默认值。可能的命令行参数如表 21-7 所示。

### 表 21-7：httpd 的命令行参数

| 参数 | 说明 |
| --- | --- |
| `-c` 指令 | 读取配置文件，然后处理该指令。这可能会覆盖配置文件中对该指令的定义。 |
| `-C` 指令 | 处理该指令，然后读取配置文件。该指令可能会更改配置文件的评估，但可能被配置文件中的另一个定义所覆盖。 |
| `-d` 目录 | 使用目录作为 `ServerRoot` 指令，指定模块、配置和日志文件目录的位置。 |
| `-D` 参数 | 定义在 `IfDefine` 指令中用于条件评估的参数。 |
| `-f` 文件 | 使用文件作为 `ServerConfigFile` 指令，而不是默认的 `/etc/httpd/conf/httpd.conf`。 |
| `-h` | 显示可能的命令行参数列表。 |
| `-l` | 列出编译时链接到可执行文件的模块。 |
| `-L` | 打印可以在配置文件中使用的指令详细列表，并附带简短描述以及包含每个指令的模块。 |
| `-S` | 列出虚拟主机的配置设置。 |
| `-t` | 对配置文件进行语法检查。结果将是：`Syntax OK` 或错误通知；例如：`/etc/httpd/conf/httpd.conf` 第 118 行语法错误。 |
| `-T` | 与 `-t` 相同，不同之处是不对 `DocumentRoot` 的值进行检查。 |
| `-v` | 打印版本信息：Server version: Apache/2.2.8 (Unix) Server built: Feb 25 2008 07:05:32 |
| `-V` | 列出版本信息以及编译期间定义的任何值：Server version: Apache/2.2.8 (Unix) Server built: Feb 25 2008 07:05:32 Server's Module Magic Number: 20051115:11 Architecture: 32-bit .... Server compiled with.... -D APACHE_MPM_DIR="server/mpm/prefork" -D APR_HAS_MMAP -D APR_HAS_IPV6 (IPv4-mapped addresses enabled) -D SERVER_CONFIG_FILE="conf/httpd.conf" |
| `-X` | 仅启动单个守护进程，不会产生其他 httpd 进程。这应该仅用于直接从命令行进行测试的目的。 |

## 监控服务器活动

Apache Web 服务器对于想要劫持计算机以进行恶意目的的人来说是一个非常有吸引力的目标。你可以使用许多技术来保护你的服务器（在第 14 章中涵盖），从 SELinux 到使用证书控制脚本的运行方式。然而，这里描述的是监控你的 Apache Web 服务器性能和安全的技术。仔细观察你的服务器通常可以在攻击发生前将其阻止。

Apache 提供了两个独特的内置方法来检查 Web 服务器的性能和状态。`server-status` 处理器可以配置为显示有关服务器进程的信息。`server-info` 处理器可以配置为显示 Web 服务器配置的详细摘要。你可以通过向 `/etc/httpd/conf/httpd.conf` 文件中添加以下行来激活这些服务：

```
<Location /server-status>

  SetHandler server-status

  Order deny,allow

  Deny from all

  Allow from 127.0.0.1
```
