
在 Apache 网站上可以找到更详细的 `mod_proxy` 指令列表：http://httpd.apache.org/doc/mod/mod_proxy.html。

修改 `httpd.conf` 后，必须重启 Web 服务器以使配置生效。

表 VII.1 `mod_proxy` 指令

| 指令 | 说明 |
| :--- | :--- |
| `ProxyRequests` | 决定 Apache 是否将作为代理运行 |
| `ProxyRemote` | 指定 Apache 使用的代理 |
| `ProxyPass` | 将本地数据请求转换为代理请求 |
| `ProxyBlock` | 阻止到指定站的代理连接 |
| `NoProxy` | 指示 Apache 直接提供服务，而不是代理 |
| `ProxyDomain` | 在内网中附加域名 |
| `CacheRoot` | 设置写入缓存文件的目录 |
| `CacheSize` | 设置以千字节为单位的缓存大小 |
| `NoCache` | 指定不进行缓存的位置 |

# 配置客户端

一旦代理服务器设置妥，任何想要使用代理服务器的客户端都必须配置使用该服务器。这是通过更改客户端的 Web 浏览器设置来实现的。为了本实验的目的，假设客户端运行的是 Netscape Navigator 进行 HTTP 连接。更改设置后，客户端应该能够通过新配置的代理建立 HTTP 连接。

# 实验练习

以下练习将引导你完成安装 `mod_proxy`、配置 `httpd` 和配置客户端的步骤。

## 安装 mod_proxy

Apache 在代理服务器上运行需要 `mod_proxy` 模块。以下步骤向你展示如何安装 `mod_proxy`。

- 确保 Apache 已经编译了可加载模块支持。从命令提示符输入：

```bash
httpd -l
```

- 这将列出所有当前加载的模块。如果没有列出 `mod_so`，则必须重新编译 Apache 以包含它。如果列出了 `mod_proxy`，则无需完成本节的其余部分。跳到下一节。

- 根据 Apache 发行版附带的说明编译 `mod_proxy` 模块。`mod_proxy` 是 Apache 发行版的一部分，并包含在 Apache 源码中。

- 要在每次启动 Apache 时都加载 `mod_proxy`，请使用 `LoadModule` 指令。首先，用文本编辑器打开 `httpd.conf`，并在全局环境中添加以下内容：

```httpd
LoadModule mod_proxy path/to/mod_proxy.so
```

## 配置 httpd

本节向你展示如何启用代理服务器。

- 1. 在 Apache 自带的 `httpd.conf` 文件找到代理指令。取消配置代理的行，并添加任何特定的站点配置。为了让 Apache 进行代理，`ProxyRequests On` 指令必须出现在其他 `mod_proxy` 指令之前。`ProxyPass` 是唯一不需要 `ProxyRequests` 的指令。

- 2. 使用 `CacheRoot` 和 `CacheSize` 指令实现 `mod_proxy` 的缓存功能。在 Apache 缓存 HTTP 数据之前，必须设置 `CacheRoot` 的值：

`CacheRoot=/var/cache/http/*`

同时，确保 `httpd` 对此目录具有写入权限。

- 3. 重启 `httpd`。

## 配置客户端

使用以下步骤配置用户端客户端 (Netscape) 使用代理服务器。

- 1. 在客户端机器上，打开 Netscape。

- 2. 从 Edit>Preferences，选择 Advanced>Proxies。

- 3. 点击 Manual proxy configuration，然后点击 view。

- 4. 在 HTTP proxy 字段中，输入代理使用的主机名和端口号。

# 问题

- 1. 如果一家公司运行内网并使用内网服务器作为代理防火墙，应该使用哪个指令使服务器不代理内网请求？

- 2. 如何将模块集成到 Apache 中？

- 3. 如果 `httpd.conf` 中同时存在 `ProxyRequests Off` 和 `ProxyPass` 指，会发生什么？

# 答案

- 1. 如果一家公司运行内网并使用内网服务器作为代理防火墙，应该使用哪个指令使服务器不代理内网请求？

- 2. 如何将模块集成到 Apache 中？

- 3. 如果 `httpd.conf` 中同时存在 `ProxyRequests Off` 和 `ProxyPass` 指，会发生什么？

# 高级问题

- 1. 如何将模块集成到 Apache 中？

- 2. 如何向 `RewriteRule` 附加标志？

- 3. 如何配置 Apache 代理？

| FLAG | DESCRIPTION |
| --- | --- |
| F | 返回 http 403 forbidden（禁止）错误 |
| G | 返回 http 410 gone（已失效）错误 |
| P | 通过 `ProxyPass` 指令对替换执行内部代理请求 |
| R | 执行外部重定向 |
| NC | 匹配模式时不区分大小写 |
| C | 将当前规则与下一个规则链联 |
| L | 不再应用任何重写规则 |

`RewriteCond` 也常用于在执行 `RewriteRule` 指令之前测试条件，这类似于编程中的 `if` 语句。`RewriteCond` 的语法如下：

```
RewriteCond testpattern condpattern [flags]
```

其中，`testpattern` 会与 `condpattern` 进行比对，`flags` 是可选的修饰符。可以将其记忆为：“如果 testpattern 匹配 condpattern，则执行后续代码”。`RewriteRule` 的语法包括服务器变量的使用（指定为 `%{variable}`）以及对括号分组文本的反向引用，如 `RewriteRule` 所示。

`RewriteCond` 支持的一些服务器变量包括：

| `REMOTE_ADDR` | `REMOTE_HOST` | `DOCUMENT_ROOT` |
| `SERVER_NAME` | `SERVER_USER` | `SERVER_PORT` | `SERVER_PROTOCOL` |
| `TIME_YEAR` | `TIME_MON` | `TIME_DAY` | `TIME_HOUR` | `TIME_MIN` | `TIME_SEC` |
| `HTTP_USER_AGENT` | `HTTP_REFERER` | `HTTP_HOST` | `HTTP_ACCEPT` |

完整列表可以在 Apache 网站上的 `RewriteCond` 文档中找到：http://http.apache.org/docs/mod/mod_rewrite.html。

## RewriteCond 的基本示例如下：

```
RewriteCond %(REMOTE_HOST) ^theserver.com
RewriteRule ^$ /theserverpage.html
```

只有当变量 `REMOTE_HOST` 匹配 `theserver.com` 时，才会将所有 URL 重写为 `DocumentRoot/theserverpage.html`。

此外，`RewriteCond` 支持两个可选标志：`[OR]` 和 `[NC]`。`[OR]` 用于测试多个条件，而 `[NC]` 用于禁用 `testpattern` 和 `condpattern` 的大小写敏感性。例如：

```
RewriteCond %{REMOTE_HOST} 192.168.3.14 [OR]
RewriteCond %{REMOTE_HOST} ^thatserver.com [NC]
RewriteRule ^$ /theserverpage.html
```

这将匹配主机 `192.168.3.14`、`thatserver.com` 或 `That-SERver.com`。

关于构建正则表达式的额外帮助，请参阅 regex 手页。

# 实验练习

在本实验中，假设用户已运行 Apache 并安装了 `mod_rewrite`。`mod_rewrite` 将用于两种不同情况重写 URL：从一个服务器重定向到新服务器，以及根据访问服务器的 Web 浏览器将用户重定向到特定的页面。

使用 `RewriteCond` 条件语句搜索用户的客户端类型，然后使用 `RewriteRule` 将用户重定向到特定的客户端页面。

- 1. 用文本编辑器打开 `httpd.conf`。

- 2. 使用 `mod_rewrite` 将主目录从一个位置重定向到另一个位置。

## URL 重写 237

使用 `mod_rewrite` 将所有带有 `/theuser/somepath/` 的 URL 重定向到 `http://newserver/~theuser/somepath/`，如下：
