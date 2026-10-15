
`./fimap.py -H -u 'http://localhost' -d 3 -w /tmp/urlist`（获取深度为 3 的网页所有链接，并将 URL 写入 `/tmp/urlist`）

# Kali Linux 2013 工具列表

## grabber

特性

- 跨站脚本攻击 (Cross-Site Scripting)
- SQL 注入（还有一个特殊的盲 SQL 注入模块）
- 文件包含
- 备份文件检查
- 简单的 AJAX 检查（解析每个 JavaScript 和 Ajax 以获取 URL 并尝试获取参数）
- 使用 PHP-SAT 对 PHP 应用进行混合分析/水晶球测试
- JavaScript 源代码分析：评估 JavaScript 的质量/正确性
- 生成一个 `[session_id, time(0)]` 文件用于后续的统计分析。

`USAGE` `grabber.py [options]`

`OPTIONS` http://www.securitytube-tools.net/index.php?title=Grabber.html

- `EXAMPLE` 读取:`http://rgaucher.info/beta/grabber/`

## joomscan

`DESCRIPTION` `joomscan` 用于检测目标 Joomla! 网站的文件包含、SQL 注入和命令执行漏洞。

- 精确版本探测（扫描器可以告知目标是否正在运行 1.5.12 版本）
- 常见的基于 Joomla 的 Web 应用防火墙检测
- 搜索 Joomla! 及其组件的已知漏洞
- 报告输出文本和 HTML
- 通过扫描器或 svn 立即更新

`USAGE` `joomscan.pl -u <string> -x proxy:port`

`OPTIONS` https://www.owasp.org/index.php/OWASP_Joomla_Vulnerability_Scanner_Usage

- `EXAMPLE` `joomscan.pl -pv -victim.com -x localhost:8080`
- `EXAMPLE` `joomscan.pl read DOCFILE` (`DOCFILE` 为以下文件之一：`changelog`,`release_note`,`readme`,`credits`,`faq`,`owasp_project`)

## nikto

`DESCRIPTION` `Nikto` 是一个 Web 服务器扫描器，对 Web 服务器进行多项内容的全面测试，包括超过 6500 个潜在危险的文件/CGI、检查超过 1250 个服务器的过时版本，以及超过 270 个服务器的特定版本问题。它还会检查服务器配置项，如是否存在多个索引文件、HTTP 服务器选项，并尝试识别已安装的 Web 服务器和软件。扫描项目和插件会频繁更新，并可以自动更新。

`USAGE` `nikto.pl [host] [target] [options]`

`OPTIONS` http://cirt.net/nikto2-docs/options.html

```
**EXAMPLE** nikto.pl -h 192.168.0.1 -T 58 (扫描调优)
```

```
**EXAMPLE** nmap -p80 192.168.0.0/24 -oG - | nikto.pl -h - (多主机测试)
```

```
**EXAMPLE** nikto.pl -h 192.168.0.1 -p 80,88,443 (多端口测试)
```

```
**EXAMPLE** nikto.pl -h https://192.168.0.1:4443/ (使用完整 URL 语法进行基础测试和扫描)
```

```
**EXAMPLE** nikto.pl -h 192.168.0.1 -p 443 (检查特定端口)
```

## padbuster

`DESCRIPTION` `PadBuster` - 用于执行填充 Oracle攻击（Padding Oracle attacks）的自动化脚本。`PadBuster` 提供了解密任意密文、加密任意明文以及执行自动化响应分析以确定请求是否受到填充 攻击的能力。

更多信息和使用方法：http://blog.gdssecurity.com/labs/2010/9/14/automated-padding-oracle-attacks-with-padbuster.html 以及 http://howtohack.poly.edu/wiki/Padding_Oracle_Attack

`USAGE` `padBuster.pl <url> <encrypted sample> <block size> <encoding>`

```
**EXAMPLE** padBuster.pl
http://sampleapp/home.jsp?UID=7B216A639451170FF851D6CC68FC9537858795A28ED4AAC6
7B216A639451170FF851D6CC68FC9537858795A28ED4AAC6 8 -encoding 2
```

```
**EXAMPLE**
http://sampleapp/home.jsp?UID=7B216A639451170FF851D6CC68FC9537858795A28ED4AAC6 8 -encoding 2
7B216A639451170FF851D6CC68FC9537858795A28ED4AAC6 2 -plaintext "ENCRYPT TEST"
```

## w3af

**描述** `w3af` 是一个 Web 攻击与审计框架。该项目为 Web 应用程序提供了漏洞扫描器和利用工具。它提供了有关安全漏洞的信息，并协助渗透测试工作。`w3af` 使用超过 130 个插件来识别大多数 Web 应用程序漏洞。在识别之后，可以利用如（盲注）SQL 注入、操作系统命令执行、远程文件包含 (PHP)、跨站脚本 (XSS) 和不安全的文件上传等漏洞获取对远程系统的不同类型的访问。

更多信息：http://w3af.org/

**用法** 不适用；GUI 工具

**示例** 不适用；GUI 工具

## wapiti

**描述** `Wapiti` 允许你审计所的 Web 应用程序的安全性。它执行“黑盒”扫描，即它不研究应用程序的源代码，而是会扫描已部署的 Web 应用的网页，寻找可以注入数据的脚本和表单。一旦获取此列表，`Wapiti` 就会像一个模糊器（fuzzer）一样工作，通过注入有效负载来检查脚本是否存在漏洞。

`Wapiti` 可以检测以下漏洞：

- 文件处理错误（本地和远程包含/引入，`fopen`, `readfile`...）
- 数据库注入（PHP/JSP/ASP SQL 注入和 XPath 注入）
- XSS（跨站脚本）注入
- LDAP 注入
- 命令执行检测（`eval()`, `system()`, `passthru()`...）
- CRLF 注入（HTTP 响应分割，会话固定...）

**用法** `python wapiti.py http://server.com/base/url/ [options]`

**选项** http://wapiti.sourceforge.net/

**示例** `python wapiti.py http://127.0.0.1/vuln/ -c cookies.txt -x http://127.0.0.1/vuln/index.php?page=logout`

## webscarab

**描述** `WebScarab` 是一个分析使用 HTTP 和 HTTPS 协议通信的应用程序框架。它用 Java 编写，因此可以移植到许多平台。`WebScarab` 有多种由许多插件实现的运行模式。在最常用的用法中，`WebScarab` 作为拦截代理运行，允许操作员在请求发送到服务器之前查看并修改浏览器创建的请求，并在浏览器接收到从服务器返回的响应之前查看并修改响应。`WebScarab` 能够拦截 HTTP 和 HTTPS 通信。操作员还可以查看通过 `WebScarab` 的对话（请求和响应）。

更多信息：https://www.owasp.org/index.php/WebScarab_Getting_Started

**用法** 不适用；GUI 工具

**示例** 不适用；GUI 工具

## webshag-cli

**描述** `Webshag` 是一个多线程、多平台的 Web 服务器审计工具。它用 Python 编写，收集了 Web 服务器审计的常用功能，如网站爬虫、URL 扫描或文件模糊。

`Webshag` 可用于通过 HTTP 或 HTTPS 扫描 Web 服务器，支持通过代理并使用 HTTP 身份验证（Basic 和 Digest）。此外，它还提出了创新的 IDS 规避功能，旨在使请求之间的关联变得更加复杂（例如，为每个请求使用不同的随机 HTTP 代理服务器）。
