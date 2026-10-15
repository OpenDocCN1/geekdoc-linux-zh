
## 用于 HTTP 认证的 `httpd.conf` 安全使用

`.htaccess` 是在 `httpd.conf` 中配置 Web 服务器。这是一种更安全的 HTTP 认证实现方式，因为它不允许创建 `.htaccess` 文件。此外，授予此权限的控制完全取决于对 `http.conf` 写权限的用户（通常是 `root`）。

`httpd.conf` 中的以下指令将实现 HTTP 认证：

```
<directory /usr/local/apache/htdocs/my_private_dir>
AuthType Basic
AuthName "My Private Directory">
```

# 破解 Linux：Linux 安全机密与解决方案

```
AuthFile /usr/local/apache/misc/my_private_dir.htpasswd
require valid-user
<Directory>
```

当请求 URL `http://localhost/my_private_dir/` 时，用户将会被提示输入其用户名和密码。

注意：如上所述，HTTP 认证密码文件并不位于文档树内。

## 利用默认配置问题

| 流行度 | 5 |
| :--- | :--- |
| 简单性 | 6 |
| 影响 | 5 |
| 风险评分 | 5 |

当安装 Linux 发行版时，它有一个默认配置。黑客很清楚发行版的默认配置可能是不安全的。黑客知道如何获取有关 Web 服务器的信息——以及如何利用漏洞。配置 Apache 的第一步是检查默认配置，并关闭你不需要的功能。以下是来自几个不同发行版的配置示例，你的发行版很可能包含了所有这些。然而，建议将它们关闭。

## 移除离线手册

许多发行版的 Web 服务器在 Web 文档树中安装了手册。这可能是危险的，因为可以为黑客提供有关你安装情况的信息。例如，该配置是 SuSE 的默认配置：

```
Alias /hilfe/ /usr/doc/susehelp/
Alias /doc/ /usr/doc/
Alias /manual/ /usr/doc/packages/apache/manual/
```

```
<Directory /usr/doc>
Options FollowLinks
AllowOverride None
</Directory>
```

此配置的问题是，通过检查 `http://www.example.com/doc/` 可以查看文档树和手册的内容。这为黑客提供了有关机器上安装软件的大量信息。此外，由于 `/hilfe/` 的存在，黑客会知道这是 SuSE 发行版，因为只有它是这样。（`Hilfe` 在德语中是“帮助”的意思。）这种配置属于“信息过多”类别。

### 移除默认欢迎页

许多发行版（如 `RedHat`）在文档树根目录下提供默认的 `index.html`，欢迎访问者使用 `RedHat` 操作系统。此类欢迎页也属于信息过多，应当移除或更改。

### 移除基于文件名的 CGI 执行

如前所述，基于文件名执行文件是一个潜在的安全问题。用于配置此常见配置的指令是 `AddHandler cgi-script .cgi`

这应该被移除。

### 安全配置解析的 HTML 文件

解析 HTML 文件也称为服务器端包含（SSI），是预处理的 HTML 文件，允许 Web 服务器执行其他文件或外部程序生成 HTML 内容。配置 SSI 的指令是：

```
Type text/.shtml
AddHandler server-parsed .shtml
AddHandler server-parsed .html
```

由于 SSI 允许任何用户（包括无经验的用户）上传可以执行程序的 HTML 文件，请仅在必要时允许 SSI 配置；否则，请将其关闭。此外，SSI 通常限制以 `.shtml` 结尾的文件，但某些 Linux 发行版可能也解析 `.html` 文件。此类发行版会有如上所示的 `AddHandler`。我们建议配置服务器仅解析 `.shtml` 文件；因此不应包含 `AddHandler server-parsed .html`。

### 安全配置服务器状态和信息的显示

Apache 可以通过以下配置显示服务器状态和其他服务器信息：

```
<Location /server-status/
SetHandler server-status
Order deny
Deny from all
Allow from localhost
```

# 破解 Linux 暴露：Linux 安全秘密与解决方案

```apache
<Location /server-info>
SetHandler server-info
Order deny,allow
Deny from all
Allow from .example.com
</Location>
```

显示服务器状态和信息应仅在受信任的机器上进行；请确保上述指令 `Deny from all` 拒绝所有访问，并且仅在 `Allow from` 中允许受信任的机器。更好的做法是直接将其关闭。

## 配置 `public_html` 目录

可以配置 Apache，使得诸如 `http://www.example.com/~jdoe` 这样的 URL 指向此目录：`~jdoe/public_html`。这是通过以下指令进行配置的：

```apache
UserDir public_html
<Directory /home/**/public_html>
</Directory>
```

如果不需要此功能，应对上述指令进行注释或删除。更安全的方法是在 Web 文档树下创建一个目录，仅供需要存放 HTML 文件的用户或用户组。该目录应允许该用户或组写入。

## 利用默认代理配置

| 流行度 | 6 |
| :--- | 10 |
| 影响 | 5 |
| 风险评分 | 7 |

许多网络需要 HTTP 代理，以强制所有用户通过称为代理服务器的单机访问互联网内容。在这种情况下，网络浏览器被配置为所有请求都联系代理服务器，而不是连接到实际网站。代理服务器随后获取 `GET`/`HEAD`/`POST` 等请求，获取页面并将其返回给浏览器。

## 第 12 章：Web 服务器与动态内容

代理可能会缓存接收到的内容，这可以加快频繁访问网站的加载。它还可能实施用户名/密码认证，允许管理员跟踪网络使用情况。

Apache 可以同时作为 Web 服务器和 HTTP 代理运行。此功能应限于一组受信任的机器。否则，攻击者可以滥用代理，原因有二：

- **匿名浏览**：攻击者可以利用你的代理服务器发起 CGI 攻击，使得你的 Web 服务器看起来是违规方。
- **浏览无法访问的网站**：后者可能通过通过你的代理访问某些通常被其禁止访问的网站。这种限制在企业和某些国家很常见。

允许第三方通过你的机器进行代理会导致带宽降低，因为你正在检索和发送甚至与你的组织无关的数据。如果你缓存了非活动站点，你将导致磁盘空间被支持这些未经授权的流量。

## 安全代理服务器指令

你可以快速测试你的 Apache 服务器以查看它是否允许代理。从外部终端机器按如下所示连接到 Web 服务器的 80 端口：

```bash
nc webserver 80 << "GET http://www.hackinglinuxexposed.com/ HTTP/1.0"
```

如果你从我们的网页获取了 HTML，那么你的 Apache 服务器可能配置不当。如果不需要 Web 代理，请确保以下部分已注释或删除。

```apache
<Directory:*>
Order deny, allow
Deny from all
Allow from .example
</Directory>
```

## CGI 程序的问题

CGI 程序允许 Web 开发者创建提供 Web 内容的复杂程序。这提供了更强大、更灵活的方式来动态生成信息。然而，如果 CGI 程序编写得不好，它们就会受到安全漏洞的影响。在本节中，我们检查了黑客可能发起的某些攻击，并讨论了处理 CGI 的通用方法，以及 CGI 程序员可能会做出的导致程序漏洞的假设。

## 利用预装和可下载的 CGI

| 流行度 | 5 |
| :--- | :--- |
| 简单性 | 6 |
| 影响 | 7 |
| 风险评分 | 6 |

随 Web 服务器发布或从脚本存档下载的 CGI 通常编写得糟糕，使其成为安全漏洞的候选者。著名的安全专家 `Rain Forest Puppy` (`http://www.wiretrip.net/rfp/`) 编写了一个名为 `Whisper` 的 CGI 扫描器。`Whisper` 是一个扫描编写糟糕且包含安全问题的已知 CGI 工具。这类程序的数量很大。在 `Security Focus` (`http://www.securityfocus.com`) 上快速搜索就发现了近 100 个。黑客知道这些编写糟糕的程序，并知道如何利用它们。

预装 CGI 的一个完美例子是随 `NCSA` 和早期 `Apache`（版本 `1.1.3`）一起分发的 `nph-finger` CGI 程序。该程序的源码如下：
