
## Inhosts 文件

Inhosts 文件内置于 Samba 并包含了 NetBIOS 名称到 IP 地址的映射，格式与 `/etc/hosts` 文件类似。该文件位于 `/etc/usr/local/samba/lib`。

## 管理 Samba 服务器

Samba 服务器有若干守护进程（特别是 `nmmbd` 和 `smbd`），它们需要启动，通常在自引导时启动，并读取 `smb.conf` 文件。一旦启动，可以通过命令行或图形界面管理服务器。

| 表 8.3 | smbstatus 选项 |
| :--- | --- |
| -b | 显示当前连接到 Samba 服务器的用户列表 |
| -s | 显示已连接的共享列表 |
| -L | 显示当前锁定的文件 |
| -u username | 显示用户用户名的信息 |
| -p | 显示 smbd 进程列表 |

界面（GUI）。命令行界面非常易使用，主命令是 `smbstatus`，它可以显示服务器和连接客户端的完整状态。表 8.3 所示了一些可用选项。

## 连接到 Samba 服务器

假设在名为 `syngress` 的服务器上有一个 Samba 服务器，并有一个名为 `rosie` 的共享目录；你可以通过命令行在 Windows 上映射驱动器到该目录：`net h: \syngress\rosie`。

Linux 拥有一个用于访问 Samba 服务器的客户端称为 `smclient`，语法为：`smclient://servername/sharename`。该客户端将向用户显示新提示符（通常为 `smb:>`），并且其功能与文件传输协议（FTP）会话非常相似，包含 `get`、`put`、`ls` 等操作。

## winbind

Linux 和微软 Windows 的集成可能非常耗时，因为没有真正的底层统一。Samba 的 `winbind` 组件尝试通过允许 Windows 域用户以 Linux 用户身份出现并操作来解决这个问题。Linux 和微软用户 ID 之间的映射由 `winbind` 存储。

## WEB 服务

后续章节将展示如何配置 Web 服务以及客户端如何访问它们。

## 快速事实

在 Linux 服务器上设置 Web 服务包括 FTP 服务器、代理服务器以及如 Java 服务器等插件。

- Web 服务器将使用超文本传输协议（HTTP）向请求者提供页面。
- FTP 服务器将使用 FTP 协议在远程客户端和服务器之间传输数据。
- 代理服务器将作为客户端与其他网络（通常是 互联网）之间的中间服务器，以减少连接的负载。

## 从命令行远程访问

常用的工具包括 `telnet`、`curl` 和 `wget`。`telnet` 是一种运行在端口 23 上的客户端-服务器协议，语法为 `telnet hostname | IP address`，它将连接到主机或 IP 地址处的 Telnet 服务器。

`curl` 和 `wget` 使用 HTTP、HTTPS 和 FTP 检索文件。`wget` 下载 URL 的语法为 `wget URL`，下载 FTP 的语法为 `wget ftp://URL`。

对于具有用户名和密码的站点，可以在命令行中指定，例如 `-ftp-user-user`。由于该命令不是交互式的，它可以被构建到脚本中以实现过程自动化。

`curl` 可以使用多种协议传输数据，并设计为无需用户交互即可工作，以便于在脚本中使用。语法为 `curl URL`。

## Apache (HTTP) 和 Tomcat

Apache 的默认安装路径为 `/usr/local/apache2`，大小为 50 MB。后续章节将展示如何配置服务器。

### APACHE 配置

服务器安装的实际目录在 `configure` 任务期间配置，并使用 `-prefix=PREFIX` 改变默认值，其中 `PREFIX` 将定义为安装目录。该目录被称为 `ServerRoot`。

```
apachectl
```

Apache 服务器作为 `http` 守护进程运行，应使用控制脚本 `apachectl` 来调用 `httpd`，以确保设置正确的环境变量。语法为 `apachectl [http-argument]`，主要参数为 `start`、`stop`、`restart` 和 `status`。

```
httpd
```

启动时，`httpd` 会读取其配置文件 `httpd.conf`，该文件相对于 `conf/httpd.conf` 中的 `ServerRoot`。一旦启动，它将创建一个进程池来处理服务器生成的所有请求。主要选项见表 8.4。

## Apache 模块

Apache 服务器可以通过模块进行自定义，模块可以为 Apache 服务器添加各种功能，如带宽管理、通用

# 第 8 章 安装、配置为服务器

| 表 8.4 | httpd 参数 |
| :--- | --- |
| -d ServerRoot | 如果 `ServerRoot` 与默认值不同，则设置其值 |
| -k start stop restart | 启动或停止守护进程 |
| -v | 显示当前版本 |
| -X | 在调试模式下运行 |

网关接口（CGI）或身份验证。可以使用以下命令列出当前加载的模块：

```
apache2 -l (显示编译在代码中的模块)
```

```
apache2 -t -D DUMP_MODULES (显示所有加载的模块)
```

可以使用 `a2enmod` 和 `a2dismod` 容器启用或禁用模块。

## Apache 容器

在 Apache 文件中，存在包含更改配置的指令的独立单元，称为 Apache 容器。`filesystem` 容器包含所有关于目录和文件的指令，例如 `location` 和访问权限。`Webspace` 容器包含所有关于你正在开发的 Web 站点的信息，例如 URL 名称。

例如，要为 `/var/web/dir` 目录启用目录索引，需要包含以下内容：

```
<Directory /var/web/dir>
Options +Indexes
</Directory>
```

当从同一台机器为多个主机服务时，可以使用虚拟主机（virtual host），允许为每个虚拟主机配置不同的配置选项。虚拟主机可以是基于 IP 的（每个网站一个 IP）或基于名称的（单个 IP 地址对应多个名称）。

> 考试警告
> 你应该知道 Apache Web

## .htaccess 文件

`.htaccess` 文件允许按目录进行配置。

## 超文本处理器

超文本处理器 (PHP) 是一种用于创建动态 Web 页面的通用语言。

## CGI 脚本

Apache 可以配置为运行 CGI 脚本。

## 配置服务器日志

Apache 日志由 `Log` 指令设置。

## TOMCAT 配置

Tomcat 是一个 servlet 和 JavaServer Pages (JSP) 容器。

## FTP

FTP 服务器用于从服务器上传和下载文件。

## Squid

Squid 可以配置为缓存 HTTP 和 FTP 流量，以减少通往互联网的流量。

## 应用服务

## SQUID 配置文件

配置文件为 `/etc/squid/squid.conf`，软件安装在 `/usr/local/squid`。Squid 可以配置为监听任何端口，当您尝试从常规浏览中隐藏某些服务器时，这通常非常有用。Squid 的默认端口为 3128，尽管有许多人将其更改为 80 端口。要允许 squid 监听 3128、80 和 8080 端口，请修改 `squid.conf`：

```
http_port 3128 80 8080
```
