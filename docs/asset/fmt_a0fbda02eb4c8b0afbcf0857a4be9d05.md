
现在你想使用 IP 计数规则来统计在 `192.168.1.0` 网络和互联网之间传输的数据包。需要的 IP 计数规则如下：

```
/sbin/iptables - FORWARD -i eth2 -d 192.168.1.0/24
/sbin/iptables - FORWARD -o eth2 -s 192.168.1.0/24
```

这里是在 `FORWARD` 链中添加 `(-A)` 的新规则，以便统计指向 `192.168.1.0` 的所有包通过网关机器的 `eth2` 接口时。记住，`eth2` 接口连接到 ISP 网络（可能通过路由器、DSL 设备或电缆调制解调器）。第二条规则规定在 `FORWARD` 链中添加另一个规则，以便统计源自 `192.168.1.0` 网络并通过 `eth2` 接口的任何 IP 包。这两条规则有效地统计了所有 IP

## 第4 章：网络性能

在 `192.168.1.0` 网络与互联网之间移动的数据包（无论是进入还是流出的）。对 `192.168.2.0` 网络执行相同的操作，请使用以下规则：

```
/sbin/iptables -A FORWARD -i eth2 -d 192.168.2.0/24
/sbin/iptables -A FORWARD -o eth2 -s 192.168.2.0/24
```

在设置好上述规则后，你可以通过 `/sbin/iptables -L -v` 命令随时查看结果。我通常会打开到网络网关的 SSH 会话并运行 `/usr/bin/watch -n 3600 /sbin/iptables -L -v -n` 以小时为单位监控流量。

如果你感兴趣了解与互联网交互的部门请求了什么类型的网络服务，也可以对此进行统计。例如，如果你想知道通过 `eth2` 接口的流量中有多少是 Web 流量，你可以实施如下规则：

```
/sbin/iptables -A FORWARD -o eth0 -m tcp -p tcp --dport www
```

这记录了指向端口 `80` 的流量（`/etc/services` 中的 `www` 端口）。你可以为 `/etc/services` 文件中找到其他网络服务添加类似的规则。

### 总结

你的网络性能状态是你的操作系统、网络设备、带宽以及你选择实施的整体网络设计的共同作用。

## 第5 章

### Web 服务器性能

本章内容

- 控制 Apache
- 加速 Web 性能

Red Hat Linux 的 Web 服务器软件是 Apache —— 它是世界上最流行的 Web 服务器。根据 Apache Group（其开发者）的，Apache 作为 HTTP 协议服务器的首要任务是第一；性能（本身）是其次。尽管如此，Apache 在现实情况下提供了良好的性能，并且在不断改进。通过许多技术手段，适当的调优可以使 Apache 服务器获得卓越的性能和灵活性。在本章中，我专注于 Apache 调优问题，并向你介绍新的内核级 HTTP 守护进程（适用于 2.4 及更高内核），它可以加速 Web 设计过程。

Apache 架构使得该产品极其灵活。几乎所有的处理——处理请求和响应的核心功能外——都是在各个模块中进行的。这种方法使得 Apache 易于编译和自定义。

![](img/177ab5b774eeb101e12de61f8616d71a_111_0.png)

> 在本书中（以及我的其他书中），贯穿所有重复建议的一个共同主线是：如果你可以访问源代码，请始终编译你的服务器。我相信运行 Apache 的最佳方式是自己编译并安装。因此，我在此部分的其他建议都假设你的系统中拥有最新版本的 Apache 源代码。

### 编译一个精简高效的 Apache

编译一个高效的服务器意味着你不需要某些功能，并且保留你希望 Apache 执行的功能。幸运的是，基于模块的 Apache 架构使得高效且高度定制的安装变得相对简单。方法如下：

1. 了解你当前拥有哪些 Apache 模块；决定你是否真的需要所有它们。要查看当前 Apache 二进制代码 (`httpd`) 中安装了哪些模块，请以 root 身份登录并运行以下命令：

```
/usr/local/apache/bin/httpd -
```

如果你将 Apache 安装在其他位置，请更改路径 (`/usr/local/apache`)。此命令显示了在 `httpd` 二进制文件中编译的所有 Apache 模块。例如，默认的 Apache 安装编译了以下模块：

- `mod_core.c`
- `mod_env.c`
- `mod_log_config.c`
- `mod_mime.c`
- `mod_negotiation.c`
- `mod_status.c`
- `mod_include.c`
- `mod_autoindex.c`
- `mod_dir.c`
- `mod_cgi.c`
- `mod_asis.c`
- `mod_imap.c`
- `mod_actions.c`
- `mod_userid.c`
- `mod_alias.c`
- `mod_access.c`
- `mod_auth.c`
- `mod_setenvif.c`
- `suex: disabled; invalid wrapper /workspace/h1/bin/suex`

如果你安装了默认的 Apache 二进制文件，可以通过以下命令运行配置脚本来查找默认安装了哪些模块：

```
--help
```

此命令显示命令行帮助，其详细解释见表 5-1。

| 选项 | 含义 |
|---|---|
| --cache-file=FILE | 将测试结果缓存在 FILE 中 |
| --help | 打印此消息 |

## 第5 章：Web 服务器性能

| 选项 | 含义 |
|---|---|
| --no-create | 不创建输出文件 |
| --quiet or --silent | 不打印 'checking...' 消息 |
| --version | 打印创建 configure 的 autoconf 版本 |

目录和文件名：

| --prefix=PREFIX | 将架构无关的文件安装在 PREFIX 中 [/usr/local/apache2] |
| --exec-prefix=EPREFIX | 将架构无关的文件安装在 PREFIX 中（与 prefix 相同） |
| --bindir=DIR | 将用户可执行文件放在 DIR 中 [EPREFIX/bin] |

### 表 5-1: 配置脚本的选项（续）

| 选项 | 含义 |
|---|---|
| --disable-status | 进程/线程监控 |
| --disable-autoindex | 目录列表显示 |
| --disable-asis | 原样输出 |
| --enable-info | 服务器信息 |
| --enable-suex | 为派生进程设置 UID 和 GID |
| --disable-cgi | CGI 脚本 |
| --enable-cgi | CGI 脚本 |
| --enable-shared=[PKGS] | 构建共享库 [默认=no] |
| --enable-static=[PKGS] | 构建静态库 [默认=yes] |
| --enable-fast=[PKGS] | 为快速安装进行优化 [默认=yes] |
| --with-gnu-id | 假设编译器使用 GNU ID [默认=no] |
| --disable-libtool-lock | 避免锁定（可能会破坏并行构建） |
| --with-program-name | 备用可执行文件名称 |
| --with-suexec-caller | 允许调用 SuExec 的用户 |
| --with-suexx-userdir | 用户子目录 |
| --with-suexec-docroot | SuExec 根目录 |
| --with-suexec-uidmin | 最小允许 UID |
| --with-suexec-gidmin | 最小允许 GID |
| --with-suexec-logfile | 设置日志文件 |
| --with-suexec-safepath | 设置安全路径 |
| --with-suexec-umask | suexec 进程的掩码 |

2. 确定你是否需要已经在 Apache 二进制文件 (`httpd`) 中编译的模块。通过移除不必要的模块，你可以提升性能（因为二进制文件体积减小），并且可能至少获得更高的安全性。

# 第 5 章：Web 服务器性能

> 例如，如果你计划从不运行 CGI 程序或脚本，可以移除 `mod_cgi` 模块——这会缩小二进制文件的大小并防止潜在的 CGI 攻击，创建一个更安全的 Apache 环境。如果从没有 CGI 请求，所有的 CGI 风险都降为零。要了解保留哪些模块、移除哪些模块，以及每个模块如何运作；你可以在 `www.apache.org` 网站获取这些信息。阅读每个模块的 Apache 文档可以帮助你确定你所使用的任何模块。

列出你不需要的模块列表，并继续下一步。
