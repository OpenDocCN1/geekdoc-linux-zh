

提示：为了测试服务器或查看本地 Apache 机器上的文件，没有必要连接到网络（甚至不需要有网络连接）。与其在 URL 中指定服务器的真实名称，不如直接在同一台计算机的浏览器上使用“localhost”（即 http://localhost/）。事实上，在未受保护的网络上开放服务器之前，先进行配置测试是最好的。

“Test Page”实际上是一种错误状态，表示你尚未为你的网站添加任何内容。要开始操作，你可以在 `/var/html` 目录下添加一个包含你自己的主页内容的 `index.html` 文件。然后你就可以继续在该目录下添加你自己的内容。

现在你的 Web 服务器已经在运行（或至少，我希望它在运行），你应该阅读下一节。它将帮助你理解如何设置更复杂的服务器布局并保护你的服务器不受滥用。如果服务器无法运行，阅读该章节也将帮助你排查服务器故障。

提示：如果你的 Web 服务器可以从本地主机访问，但局域网（LAN）或其他用户无法访问，你可能需要更改防火墙规则以允许更大的访问。附录 B 解释了如何让你的 Web 或或其他服务器可访问。特别是，你需要打开 tcp 端口 80 和 443（如果你提供 https）。此外，如果启用了 SELinux，它可能会阻止你预期的 Web 服务器访问。要禁用 SELinux，请以 root 身份输入 `setforce 0`。或者输入 `http_selinux` 来学习如何在 http 中使用 SELinux。

## 配置 Apache 服务器

配置 Apache Web 服务器的主要文件是 `httpd.conf`（位于 `/etc/httpd/conf` 目录）。经过一段时间后，Apache 项目开始建议不要使用额外的配置文件（如 `rm.conf` 和 `access.conf`），而是简单将所有内容放在 `httpd.conf` 中。然而，在最近的发布中，趋势是让与 Apache 一的模块和其他组件拥有它们自己的配置文件（通常位于 `/etc/httpd/conf/` 目录）。

所有的 Apache 配置都是都是文本文件，可以使用你最喜欢的文本编辑器进行编辑`/etc/httpd/conf/httpd.conf` 文件在下节中完整重现，并在相关的选项块之后插入了合并内容（旨在补充每个文件的注释）。

与 Apache 相关的某些模块、脚本和其他服务（如 perl、php、ssl、webizer 和 mysql）都有你可能感兴趣的独立配置文件。这些文件包含 `/etc/httpd/conf.d/` 目录中。本章稍后的“配置模块和相关服务 (/etc/httpd/conf.d.*conf)”部分将讨论模块和相关功能。

## 第 21 章：设置 Web 服务器

交叉引用：你可以在自己的 Web 服务器上通过 http://localhost/manual/ 获取更多关于 Apache 的信息（如果安装了 `httpd-manual` 包）。

## 配置 Web 服务器 (httpd.conf)

`httpd.conf` 文件是 Apache 服务器的主要配置文件。它包含了与服务器常规运行相关的选项。默认文件名（`/etc/httpd/conf/httpd.conf`）可以通过传递给 httpd 守护进程 `-f filename` 参数或 `ServerConfig` 指令来覆盖。以下章节列出了 `httpd.conf` 文件的内容并描述了如何使用该文件。

第一部分包含关于 `httpd.conf` 文件的注释：

```
# 这是 Apache 主配置文件。它包含了
# 为服务器提供指令的配置指令。
# 详细信息请参阅 <URL:http://httpd.apache.org/docs/2.2/>。
# 特别是，请参阅
# <URL:http://httpd.apache.org/docs/2.2/mod/directives.html>
# 关于每条配置指令的讨论。

# 在不理解这些指令作用的情况下，不要执行
# 这里的指令。它们在这里作为提示或提醒。如果你
# 不确定，请查阅在线文档。你已经收到警告了。

# 配置指令被分为三个基本部分：
# 1. 控制 Apache 服务器进程整体运行的目录
#（“全局环境”）。
# 2. 定义主服务器或默认服务器参数的目录，
# 它响应未由虚拟主机处理的请求。
# 这些指令还为所有虚拟主设置
# 提供了默认值。
# 3. 虚拟主机的设置，允许 Web 请求发送到
# 不同的地址或主机名，并由 Apache 服务器进程进行处理。
# 配置和日志名称：如果你为许多服务器
# 控制文件指定的文件名以 "/" 或 Win32 的 "drive:" 开头，
# 服务器将使用该显式路径。如果文件名
# “没有”以 "/" 开头，则会在 ServerRoot 的值前面加上 -，
# 所以 "log.foo with ServerRoot set to "usr/local/apache"
# 将被服务器解释为 "usr/local/apache/logs/foo.log"。
```

该部分由有趣的注释组成。它告诉你是信息在该文件中是如何分组的，以及 httpd 守护进程如何访问此文件。默认情况下，日志文件位于 `/var/log/httpd` 目录。

## 设置全局环境

在 `httpd.conf` 文件的“第 1 部分：全局环境”中，你设置了影响 Apache 服务器常规运行的指令。以下是不同指令的用途：

```
### Section 1: Global Environment
# 此部分中的指令影响 Apache 的整体运行，
# 例如它可以处理的并发请求数，或者它
# 在哪里寻找它的配置文件。
```

## 显示子组件

`ServerTokens` 指令让你防止远程计算机发现你的 Apache 服务器上运行着哪些子组件。如果你不想暴露信息，请注释掉此行。为了防止暴露，`ServerTokens` 设置如下：

```
# 不要关于我们运行的所有子组件提供
# 太多信息。如果你不在意远程站点
# 发现你运行哪些主要的可选模块，请注释掉此行
ServerTokens OS
```

将 `ServerTokens` 设置为 `ProductOnly` 将最大限度地减少潜在破解者可能看到的连接信息。

## 设置服务器根目录

`ServerRoot` 指令指定包含配置文件、日志文件目录链接以及模块目录链接的目录。可以使用传递给 `httpd` 的 `-d` 命令行参数指定备选的 `ServerRoot` 路径。

```
# ServerRoot: 目录树的顶端，服务器的
# 配置、错误和日志文件都保在此处。
```

```
# 注意：如果你打算将此放置在 NFS（或其他网络）挂载的
# 文件系统上，请阅读 LockFile 文档（可用）
# <URL:http.apache.org/docs/2.2/mod/core.html#lockfile>（注：此处为示例链接，保持格式）
# 你将自己省去很多麻烦。
```

```
# 不要在此路径末尾添加斜杠。
```

```
ServerRoot "etc/httpd"
```

## 存储服务器的 PID 文件

Apache Web 服务器跟踪运行服务器进程的 PID。你可以通过下面的条目找到此文件的位置：

```
# PidFile: 服务器在启动时应记录其进程
# 标识码的文件
PidFile run/httpd.pid
```

Apache 使用 `PidFile` 来存储第一个（root 所有的）主守护进程的进程 ID。此信息由 `/etc/init.d/httpd` 脚本在关闭服务器时使用，并由 `server-status` 处理程序（后文所述）使用。

## 配置超时值

你可以设置几个与超时相关的值。其中一些值在代码后的正文中进行了描述：

```
# Timeout: 接收和发送超时前的秒数。
#
Timeout 120

# KeepAlive: 是否允许持久连接（每个连接处理
# 多个请求）。设置为 "Off" 以禁用。
#
KeepAlive Off

# MaxKeepAliveRequests: 在持久连接期间允许
# 的最大请求数。设置为 0 以允许无限数量。
# 我们建议将此值调大以获得最佳性能。

MaxKeepAliveRequests 100

# KeepAliveTimeout: 在同一连接上等待同一客户端
# 下一个请求的秒数。
#
KeepAliveTimeout 15
```

`Timeout` 指令决定了 Apache 在接收数据包之间、接收响应确认之间或接收传入请求时保持连接打开的秒数。默认值为2 分钟（120 秒），如果你发现机器上有过多的空闲连接，可以降低该值。

`KeepAlive` 指令指示 Apache 在处理完请求后保持连接一段时间。这使得来自同一客户端的后续请求可以处理得更快，因为不需要为每个请求创建新连接。

