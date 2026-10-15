
`a2mod` 和 `a2dissmod` 工具简化了 Apache 管理。与其在 `httpd.conf` 中添加或注释掉模块，不如使用这些程序来启用或禁用模块。这种设置使其在安装后即可保持功能正常。

## 配置工具

`a2ensite`（启用站点）和 `a2dissite`（禁用站点）工具启用和禁用虚拟主机（第 937 页）。这些命令的操作与描述的命令类似。首先在 `/etc/apache2/sites-available` 目录中设计虚拟主机。然后使用 `a2ensite` 站点名称在 `/etc/apache2/sites-enabled` 目录中创建符号链接。`a2dissite` 移除符号链接，从而禁用虚拟主机。

## INCLUDE 指令

```
$ grep "Include" /etc/apache2/apache2.conf
Include /etc/apache2/mods-enabled/*.conf
Include /etc/apache2/mods-enabled/*.conf
Include /etc/apache2/httpd.conf
Include /etc/apache2/ports.conf
Include /etc/apache2/conf.d/
Include /etc/apache2/sites-enabled/
```

### 表 26-1 可以在 httpd.conf 中重写的的指令

| AccessFileName | MaxRequestsPerChild |

| :--- | :--- |

| DefaultType | MaxSpareThreads |

| ErrorLog | MinSpareThreads |

| Group | PidFile |

| HostNameLookups | ServerRoot |

| KeepAlive | StartServers |

| KeepAliveTimeout | ThreadsPerChild |

| LockFile | Timeout |

| LogLevel | TypesConfig |

| MaxClients | User |

| MaxKeepAliveRequests | |

在 `httpd.conf` 的 `Include` 指令之后，这些控制日志格式、索引选项、MIME 处理和浏览器 Bug 修复的指令，位于 `/etc/apache2/sites-enabled` 的 `Include` 指令之前（后者是 `apache2.conf` 的最后一行）。你可以通过将这些指令复制到 `sites-enabled` 目录下的各个站点文件并在其中进行修改，从而实现按站点重写这些指令。

如果你管理着多个 Ubuntu 服务器，将自定义的配置与主配置分开是很有用的。这样你就可以使用 `scp` 将文件复制到每个新服务器上。或者，你可以将自定义代码保存在版本控制系统中，并检出以配置新系统。这种技术比使用 `diff` 来查找不同系统之间的更改要容易得多。

# 文件系统布局

本节列出了配置 Apache 和 Web 页面时将用的文件位置和用途。

- Apache 服务器及相关二进制文件位于几个目录中：
  - `/usr/sbin/apache2`—Apache 服务器（守护进程）。
  - `/usr/bin/apache2ctl`—启动和停止 Apache。`apache2` 初始化脚本会调用 `apache2ctl`。
  - `/usr/bin/htpassswd`—创建并维护 Apache 认证模块使用的密码文件（第 945 页）。
  - `/usr/bin/rotateles`—轮 Apache 日志文件以防止这些文件过大。有关旋转日志文件的信息，请参阅 `logrotate`（第 622 页）。
  - `/etc/apache2/mods-available`—包含各个模块对应的 `LoadModule` 指令（第 928 页）的文件。此目录下的 `alias.conf` 文件默认启用。两个最常用的模块二进制文件是 `mod_perl`（属于 `libapache2-mod-perl2` 包）和 `mod_python`（属于 `libapache2-mod-python` 元软件包）。此目录下的 `*.load` 文件从 `/usr/lib/apache2/modules` 目录加载模块（第 941 页）。`.conf` 文件用于配置模块以供使用。有关使用 `aenmod` 启用模块的信息，请参阅第 905 页。
  - `/etc/apache2/mods-enabled`—存放指向 `mods-available` 中文件的链接。使用 `aenmod` 创建和删除这些链接（第 905 页）。

Apache 配置存储位于 `/etc/apache2/` 层级结构中：

`/etc/apache2/conf.enabled`—包含配置指令。该文件是 Apache 主配置文件。你通常不会修改此文件，而是将任何配置项放在 `httpd.conf` 和其他文件中。

- `/etc/apache2/envars`—包含修改 Apache 运行环境的变量。
- `/etc/apache2/ports.conf`—包含监听目录（第 910 页），控制 Apache 监听器的 IP 地址和端口。
- `/etc/apache2/sites-available`—包含创建虚拟主机代码的文件。有关使用 `azenite` 启用站点的信息，请参阅 906 页。
- `/etc/apache2/sites-enabled`—存放指向 `sites-available` 中文件的链接。使用 `azenite` 创建和删除这些链接（第 906 页）。
- `/etc/apache2/httpd.conf`—包含本地配置指令。该文件补充同目录下的 `apache2.conf` 文件。关于配置指令的讨论从第 909 页开始。
- `/etc/apache2/conf.d`—包含配置指令的文件。

配置文件

- `/var/log/apache2/access_log`—记录 Apache 的请求。
- `/var/log/apache2/error_log`—记录 Apache 的运行时错误。
- `/var/www/cgi-bin`—存放 CGI 脚本的目录。
- `/var/www/html`—默认 Web 根目录。
- `/var/www/`—存放 Web 内容的根目录。
- `/etc/apache2`—存放 Apache 配置文件的目录。
- `/usr/lib/apache2`—存放 Apache 模块的目录。
- `/usr/lib/apache2/modules`—存放 Apache 模块二进制文件的目录。
- `/run/apache2`—存放 Apache PID 文件的目录。

## 配置指令 911

默认：无（如果没有此指令，Apache 将不会启动）

Ubuntu: `Listen 80`

`Redirect`（重定向）告诉客户端从另一个指定的位置获取请求的资源。

`Redirect [status] requested-path [new-URI]`

其中 `status` 是 Apache 随同重定向一起返回的状态码。如果你省略了 `status`，Apache 会假设为临时的（temp）。该状态可以是 300–399 范围内的 Apache 错误代码，或者是以下之一：

| status | 描述 |

| :--- | :--- |

| permanent | 返回状态 301（资源已永久移动） |

| temp | 返回状态 302（资源已临时移动） |

| seeother | 返回状态 303（资源已被替换） |

| gone | 返回状态 410（资源已删除）——不接受 new-URI 参数 |

`requested-path` 是 Apache 重定向到的文件或目录的绝对路径名。所有以请求路径中由 `requested-path` 指定的绝对路径开头的请求都会被重定向。（见下例）如果你想在此参数中使用正则表达式，请使用 `RedirectMatch`（上文讨论）。

`new-URI` 是 Apache 重定向到的 URL。如果 `new-URI` 以斜杠（/）开头且没有合并（merge）一个类似的前缀，Apache 将使用它调用时使用的相同前缀。大多数 `Redirect` 指令都需要一个 `new-URI` 参数。

请求必须匹配 `requested-path` 参数的所有段。假设有以下指令：

```
Redirect /mom,example.com/pictures http://pictures.example.com/
```

Apache 将把对 http://www.example.com/pictures/mom.jpg 的请求重定向到 http://pictures.example.com/mom.jpg，但由于最后一段不匹配，它将不会重定向对 http://www.example.com/pictures_mom.jpg 的请求。

上下文：服务器配置、虚拟主机、目录、.htaccess

在 `sites-available/` 中指定
