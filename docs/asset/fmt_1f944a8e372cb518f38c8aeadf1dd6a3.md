
## 5.2 启动 Named

Oct 26 18:03:20 ns named: cache (IN) loaded (serial 42)

Oct 26 18:03:20 ns named: master "localhost" (IN) loaded (serial 4)

Oct 26 18:03:20 ns named: master "0.127.0.in-addr.arpa" (IN) loaded (serial 4)

Oct 26 18:03:20 ns named: master "snake-oil.com" (IN) loaded (serial 99)

Oct 26 18:03:20 ns named: master "99.168.192.IN-ADDR.ARPA" (IN) loaded (serial 9910011)

Oct 26 18:03:20 ns named: listening on 127.0.0.1:53 (lo)

Oct 26 18:03:20 ns named: listening on 9.24.106.15:53 (eth0)

Oct 26 18:03:20 ns named: Forwarding source address is 0.0.0.0:1)

Oct 26 18:03:20 ns named: Ready to answer queries.

## 5.3 配置技巧

在 `named.conf` 的 `options` 部分使用 `listen-on` 指令。对于域名服务器监听的每个接口，都会打开一对文件句柄。在繁忙的域名服务器上，节省每个文件句柄是一个巨大的优势。定期检查 `/var/log/messages` 文件以发现错误。`Named` 的消息非常详尽。如果你不断地添加、删除或修改你的区域记录，你可能想看一眼 `nsupdate` 工具，它也属于 `bind` 软件包。你的域名服务器也应该能正确地解析 `snake-oil` 域名的主机名。

# 第 6 章 DHCP - 动态配置协议

随着可用 IP 地址数量的不断减少，以及维护静态 IP 的苦恼，DHCP 已成为大多数 TCP/IP 环境的必需。

## 6.1 什么是 DHCP？

DHCP 代表动态主机配置协议。在使用 TCP/IP 时，计算机系统需要一个唯一的 IP 地址。没有 DHCP，必须为每个计算机系统输入 IP 地址。有了 DHCP，服务器分配 IP 地址。

## 6.2 我为什么应该使用 DHCP？

在过去，网络上的每个设备都必须有一个静态 IP 地址。随着访问互联网的计算机增加，可用地址池正在迅速减少。网络管理员可以使用 DHCP 大幅减少所需的 IP 地址。

即使对于较小的网络，跟踪单个 IP 地址也非常困难。有了 DHCP，服务器完成所有的维护工作，映射 IP 地址到 MAC 地址并跟踪租赁时间。

## 6.3 在 Linux 上实现

在本节中我们将讨论如何在 Linux 上实现 DHCP 服务器。

首先我们将安装 DHCP 服务器二进制文件。该软件包位于 Caldera OpenLinux 光盘上，并且默认安装。你可以按照我们在第 123 页“设置 Samba 服务器”中描述的方法验证这一点。`dhcpd` 软件包位于 Boot Session 中的 Server 部分。启动软件包后，你将看到一个类似于图 155 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b88_181_0.png)

图 155. 验证 `dhcpd` 软件包已安装

`dhcpd` 服务器配置文件通常位于 `/etc/dhcp/dhcpd.conf` 或 `/etc/dhcpd.conf`（取决于发行版）。以下是一个示例配置：

```
# DHCP 服务器配置文件。

# 请参阅 /usr/doc/dhcpd-1.0pl2 获取示例，

# 并查看 man 页 dhcpd.conf。

#

default-lease-time 600;

max-lease-time 7200;

option subnet-mask 255.255.255.0;

option broadcast-address 192.168.1.255;

option routers 192.168.1.254;

option domain-name-servers 192.168.1.1, 192.168.1.2;

option domain-name "ibm.com";

subnet 192.168.1.0 netmask 255.255.255.0 (

  range 192.168.1.100;

)
```

您并不局限于单个子网。您允许共享网络特定参数、多个子网特定参数、组参数以及主机特定参数。

您可以定义多个范围，根据客户端的硬件地址分配特定的 IP 地址，并在需要时指定 WINS 服务器。

更多信息请参阅 `dhcpd.conf` man 页。

DHCP 服务器需要一个地方来跟踪租约。这是通过 `/var/state/dhcpd.leases` 文件完成的。

要启动 DHCP 服务器，请输入：

```
/etc/rc.d/init/dhcpd start
```

如需调试信息，请使用 `-d -f` 标志。

如果您希望 DHCP 服务器在服务器启动时自动启动，请遵循第 134 页 4.2.3 “将 Samba 作为启动服务启动”中的说明，但不要选择 SMB 服务器进程 (`samba`)，而是选择 DHCP 和 BOOTP 启动服务器。

# 第 7 章 Apache Web IBM HTTP 服务器

Apache Web 服务器是当今互联网上流行的 Web 服务器软件。根据 NetCraft 在 `http://www.netcraft.com/survey/` 上的 Web 服务器调查，所有调查的 Web 服务器中，超过 55%（超过 730 万个）运行着 Apache 版本（截至本文编写时）。Apache 是一个非常成功的协作开源项目。Apache 的网站是 `http://www.apache.org`。由于完整源代码免费提供，它是一个灵活且强大的 Web 服务器解决方案。此外还有许多额外的模块，可以与 Apache 主程序结合使用。一些流行的示例包括 PHP（PHP: 超文本预处理器，一种嵌入的 HTML 脚本语言）、`mod_perl`（一个嵌入的 perl 解释器）以及用于安全事务的 `mod_ssl`。可以从 Apache 模块库下载更多 Apache 模块：`http://modules.apache.org`。

Apache 的一些关键特性包括：

- 实现最新的协议，包括 HTTP/1.1 (RFC2068)。
- 具有高度配置性，并可以通过第三方模块进行扩展。
- 可以使用 Apache 模块 API 编写“模块”进行自定义。
- 提供完整的源代码并附带不受限制的许可。
- 可以在大多数版本的 UNIX（包括 Linux）上无需修改即可运行。
- 用于身份验证的 DBM 数据库，允许您设置具有大量授权用户的密码保护页面，而不会导致服务器缓慢。也可以使用多种 SQL 数据库进行身份验证（使用附加模块）。
- 对错误和问题的自定义响应，允许您设置文件甚至甚至是 CGI 脚本，由服务器在响应错误和问题时返回。例如，您可以设置一个脚本来拦截 500 服务器错误，并对用户和自己进行实时诊断。
- 多个 `DirectoryIndex` 指令，允许您设置 `DirectoryIndex index.html index.cgi`，这指示服务器在请求目录 URL 时返回 `index.html` 或运行 `index.cgi`，取决于它在目录中找到哪一个。
- 可以在文件中声明无限数量的 `alias`（别名）和 `redirect`（重定向）指令。

## 7.1 IBM HTTP 服务器

由 Apache IBM HTTP Server 基于 Apache HTTP Server。除了 Linux 之外，此 HTTP 服务器还运行在 AIX、Solaris 和 Windows NT 上。访问主页：

```
http://www-4.ibm.com/software/webservers/httpsservers/
```

Linux 版 IBM HTTP Server 提供以下额外功能：

- 远程配置：基于浏览器的配置工具，允许通过 GUI 操作服务器。
- SNMP 支持：简单网络管理协议 (SNMP) 是一种用于远程管理和收集服务器信息的成熟协议。此新支持允许 IBM HTTP Server 通过 SNMP 协议进行管理。
- LDAP：IBM HTTP Server 轻量级目录访问协议 (LDAP) 插件允许由 LDAP 服务器执行身份验证和授权（访问受保护资源时需要），从而大大减少了为每个 Web 服务器本地维护用户和组信息的管理开销。
- 机器翻译支持：此项新功能与可用的 IBM 机器翻译引擎配合使用时，允许 IBM HTTP Server 在无需人工干预的情况下将英文页面翻译成其他语言。这允许网站访问者以母语言阅读页面，有效地扩大了您的网站的影响范围。IBM 机器翻译引擎包含在 WebSphere Application Server 3.0 中，包括德语、简体中文和繁中文。未来将提供更多语言。
- 支持 SSL：IBM HTTP Server 支持安全连接。
- 快速响应：缓存可以显著提高服务器性能。

## 7.2 安装 Apache

Linux 通常默认安装 Apache HTTP 服务器。您可以通过运行第 72 页 2.5 “添加和删除软件”中描述的命令来检查是否安装了 Apache 包。启动、停止或重新加载 Apache，运行脚本：

```
/etc/rc.d/init/httpd (start|stop)
```

在 Caldera Linux 中，Apache 将从 `/home/httpd` 提供 HTML 文档，从 `/home/httpd/cgi-bin` 提供 CGI 脚本。如果您安装了 PHP 模块 (`mod_php`)，如果文件以 `.php` 结尾，它也将执行 PHP 代码。访问日志文件位于 `/var/log/httpd/access_log`，错误日志文件位于 `/var/log/httpd/error_log`。Apache 配置文件位于 `/etc/httpd/conf`。

如果您现在将浏览器指向服务器的 IP 地址，当 Apache 服务器运行时，您将看到以下页面 (`/home/httpd/html/index.html`)：

# 成功了！此网站已安装 Apache Web 服务器

如果您能看到此页面，该域的所有者刚刚成功安装了 Apache Web 服务器。他们现在必须在此目录添加内容并替换此占位页面，否则让服务器指向其真实内容。

> 如果您看到此页面而不是预期的网站，请联系该网站的管理员。（尝试向 `webmaster@domain.com` 发送邮件）尽管此网站运行 Apache 软件，但与 Apache 组没有联系，请勿就此网站或内容向 Apache 作者发送邮件。如果这样做，您的邮件将被忽略。

Apache 文档包含在此发行版中。

此网站的管理员管理员可在支持 Apache 的 Web 服务器上使用下方的图片。感谢使用 Apache！

![](img/2d69b129b41635ef36a3e6707d34b788_187_0.png)

图 156. Caldera Linux 上的 Apache 启动页面

## 7.3 IBM HTTP Server 安装

在 Caldera Linux 上安装 IBM HTTP Server，您需要执行以下步骤。

对于 IBM HTTP 服务器和远程管理功能，请从页面下载以下 tar 文件：

```
http://www-4.ibm.com/software/webservers/httpsservers/download.html
```

`HTTPServer.linux.glibc2.server.tar` 文件包含以下包：

- `IBM_HTTP_Server-1.3.6-2.i386.rpm` - IHS Web 服务器
- `IBM_Apache_Source-1.3.6-2.i386.rpm` - Apache 1.3.6 服务器
- `Readme.httpspserver` - 安装说明

`HTTPServer.linux.glibc21.admin.tar.file` 包含以下软件包：

- `IBM_Admin_Server-1.3.6-1.i386.rpm` - GUI 管理服务器
- `IBM_Admin_Server_Forms-1.3.6-1.i386.rpm` - 用于 GUI 的 Web 表单

还有一些额外的软件包（如 SNMP 和 SSL 模块）也可以安装。然而，本章节将不再涵盖这些。请参考下处的安装说明：

```
http://www-4.ibm.com/software/websservers/httpserver/doc/v136/readme_httpserver.htm
```

下载完“压缩包”（tarballs）后，将其移动到 `/tmp` 目录并使用以下命令解压：

```bash
tar xvf HttpServer.linux.glibc21.server.tar
tar xvf HttpServer.linux.glibc21.admin.tar
```

这会将上述的 RPM 文件从压缩包中提取到 `/tmp/IHS` 子目录中。你需要切换到 `root` 用户（如果你尚未切换的话）。为了避免资源冲突，你必须首先执行以下命令关闭当前运行的 Apache Web 服务器（如果已安装）：

```bash
/etc/rc.d/init/httpd stop
```

此外，请确保在下次重启后它不会再次启动，方法如我们在 2.9 节第 88 页“守护进程（服务）”中所描述的那样禁用 Web 服务器服务。

现在，你需要使用以下命令安装软件包（假设软件包位于当前目录）：

```bash
rpm -Uhv IBM_HTTP_Server-1.3.6-1.i386.rpm
rpm -Uhv IBM_Admin_Server-1.3.6-1.i386.rpm
rpm -Uhv IBM_Admin_Server_Forms-1.3.6-1.i386.rpm
```

安装 HTTP Server 软件包时也会尝试自动启动服务器。如果它没有启动，可能还有另一个 HTTP 服务器在运行。请先停止那一个，然后使用以下命令尝试重启 IBM HTTP Server：

```bash
/etc/rc.d/init/ibmhttpd start
```

如果命令行或以下路径：

```
/opt/IBMHTTPServer/logs/error_log
```

中没有错误，

请尝试用浏览器打开新 HTTP 服务器的首页。你应该能看到以下页面：

![](img/2d69b129b41635ef36a3e6707d34b788_189_0.png)

图 157. IBM HTTP Server 启动页面

如果你仍然看到旧 Web 服务器的启动页面，请在 Netscape 浏览器上按 `Shift+Reload` 强制刷新此页面。

IBM HTTP Server 的基础安装已完成！在默认设置下，它从 `/opt/IBMHTTPD/htdocs` 目录提供 HTML 页面，并从 `/opt/IBMHTTPD/cgi-bin` 提供 CGI 脚本。日志文件位于 `/opt/IBMHTTPD/logs`。

172 Caldera OpenLinux 和 Netfinity 服务器集成指南

### 7.3.1 在系统启动时激活 IBM HTTPD

默认情况下，IBM HTTP Server 必须在系统重启后手动启动。如果你希望它自动启动，则必须将启动脚本添加到启动过程中。

如果你希望此服务器在启动时运行，你需要在 `/etc/rc.d/rc3.d` 目录（如果你在运行级别 3 启动系统，这是默认运行级别）或 `/etc/rc.d/rc5.d`（如果你在运行级别 5 启动系统）中创建正确的符号链接。你可以通过以下命令手动完成：

```bash
cd /etc/rc.d/rc3.d
ln -s ../init.d/ibmhttpd /etc/rc.d/rc3.d/S67ibmhttpd
ln -s ../init.d/ibmhttpd /etc/rc.d/rc3.d/K01ibmhttpd
```

```bash
cd /etc/rc.d/rc5.d
ln -s ../init.d/ibmhttpd /etc/rc.d/rc5.d/S67ibmhttpd
ln -s ../init.d/ibmhttpd /etc/rc.d/rc5.d/K01ibmhttpd
```

这将在运行级别 3 和运行级别 5 下启动 IBM HTTP 服务器，并确保在切换到其他运行级别（例如关机）时能够正常关闭。

### 7.3.2 设置管理服务器

在开始使用管理服务器之前，你必须执行一些准备步骤，以便远程修改 IBM HTTP Server 的配置文件。

管理服务器任务的基本意图是允许管理服务器对必要的配置文件具有读/写/执行权限。管理服务器应该通过创建的唯一用户 ID 和组来获取读/写权限。管理服务器配置文件中的 `User` 和 `Group` 指令应更改为唯一的用户 ID 和组。管理服务器配置文件的“组访问权限”应更改为允许读写“组访问”。此外，还有一个实用程序，它应该具有“组执行权限”和“设置用户 ID 为 Root 权限”。该可执行文件必须运行，以便请求重启 IBM HTTP Server 和管理服务器。

为了正确设置这些前提条件，可以通过执行脚本 `/opt/IBMHTTPServer/bin/setup` 来完成这些任务。调用后，它将向你提几个问题并提供每个执行步骤的详细信息。在 Caldera OpenLinux 上，脚本无法自动为管理服务器创建新的用户和组。解决方案是用 COAS 工具创建组和账户，然后在设置管理服务器时使用这些名称。在随后的屏幕中输入加粗标记的关键字：
