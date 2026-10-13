
ErrorLog `logs/example-error_log`

CustomLog `logs/example-access_log` combined

`<Directory /var/example.com/www>`

Options Indexes FollowSymLinks ExecCGI

`</Directory>`

`</VirtualHost>`

`<VirtualHost www.example.net>`

ServerName `www.example.net`

ServerAdmin `aghhori@example.net`

DocumentRoot `/var/example.com/www`

DirectoryIndex `index.html`

ErrorLog `logs/example-error_log`

CustomLog `logs/example-access_log` combined

`<Directory /var/example.com/www>`

Options Indexes FollowSymLinks ExecCGI

`</Directory>`

`</VirtualHost>`

```
- 4. 执行以下命令以检查 httpd.conf 的语法。
```

```
# httpd -t

Syntax OK
```

获取更详细的输出，请运行任一命令：

```
# httpd -S

# service httpd configtest

# apachectl configtest
```

- 5. 如果 DocumentRoot 目录不存在，请创建：

```
# mkdir -p /var/example.com/www

# mkdir -p /var/example.com/www
```

- 6. 在两个 DocumentRoot 目录中创建 index 文件并向它们添加一些文本：

```
# vi /var/example.com/www/index.html

This is a test website for example.com.

# vi /var/example.net/www/index.html

This is a test website for example.net.
```

- 7. 按照“防火墙级安全”子节描述修改防火墙设置以开启端口 80。

- 8. 按照“SELinux 安全”子节描述修改 SELinux 设置。

- 9. 按照“SELinux 文件上下文”子节描述递归修改两个 DocumentRoot 目录的 SELinux 上文。

- 10. 执行“配置非安全虚拟主机”中的步骤 9 和 10。

- 11. 按照“配置 Apache Web 服务器”节中的说明，从本地和远程系统的文本及图形浏览器中加载端口 80 上的 `www.example.com/index` 和 `www.example.net/index` 来测试配置。

在访问网站时，对两个 DocumentRoot 目录下的 `example-access_log` 文件运行带 `-f`（跟随）的 `tail` 命令以查看情况。例如：

```
# tail -f/var/example.com/www/example-access-log
```

## HTTP 配置器概述

Red Hat HTTP 配置器是配置虚拟主机和修改其他指令的图形化界面。提供的内容将覆盖 `http.conf` 文件中的指令。要启动该工具，在 X 终端中执行 `system-config-httpd` 命令，或选择 (GNOME) 系统 → 管理 → 服务器 → HTTP 或 (KDE) 主菜单 → 系统工具 → HTTP。图 29-3 显示了界面。请参考本章早前的表格。

### 图 29-5 HTTP 配置器 – 服务选项卡

“性能调整”选项卡允许你定义每个服务器的最大连接数、每个连接的最大请求数、连接超时值以及每个连接请求的设置。

### 图 29-6 HTTP 配置器 – 性能调整选项卡

## Squid 缓存代理服务器

Squid 是一种缓存服务器，它将经常访问的信息缓存在本地磁盘上，从而提高整体互联网的访问速度。Squid 还作为 HTTP 和 FTP 等协议的代理服务器，并代表客户端代理 Web 页面。简而言，Squid 同时提供了缓存和代理服务，并能对访问的网站进行跟踪以及限制对特定站点的访问。

Squid 可以对网络上的组系统以父/兄弟配置模式进行配置，这允许组内的每个系统在访问互联网之前，首先咨询自己的缓存，然后在其他系统中查找缓存以获取请求的信息。Squid 使用缓存间协议 (ICP) 在组内系统之间进行数据传输。

Squid 不依赖 TCP Wrappers 进行访问控制，而是有其内置的机制来实现此目的。

## Squid 守护进程、以及启动和配置文件

Squid 守护进程名为 `squid`，位于 `/usr/sbin` 目录。Squid 的启动和配置文件在表 29-10 中列出并解释。

### 文件描述

| 文件 | 描述 |
| :--- | :--- |
| `/etc/sysconfig/squid` | 启动配置文件。 |
| `/etc/rc.d/init.d/squid` | 启动和停止脚本。 |
| `/etc/squid` | 配置文件的所在目录位置。 |
| `/etc/config/squid/squid.conf` | 主配置文件。 |
| `/var/log/squid` | 日志文件的目录位置。`access.log`（记录请求客户端信息的日志）、`cache.log`（记录启动/停止等日志）和 `store.log`（记录缓存信息添加和删除的日志）文件通常位于此处。 |
| `/var/spool/squid` | 缓存的目录位置。 |

### 表 29-10 Squid 启动和配置文件

Squid 的启动配置为 `/etc/sysconfig/squid`，它包含几条指令：

```bash
# cat /etc/sysconfig/squid

# default squid options

# -D 禁用 init 检查。如果你在运行 squid 时很可能没有

# 网络连接，请取消此注释

SQUID_OPTS="-D"

# 当要求 Squid 关闭时等待其关闭的时间。通常不需要这么长时间。

SQUID_SHUTDOWN_TIMEOUT=100
```
