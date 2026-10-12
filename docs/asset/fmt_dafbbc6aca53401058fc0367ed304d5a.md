
# DIRB
`DIRB`自带了一组预配置的攻击字典以便方便使用，但你也可以使用自定义的字典。此外，`DIRB`有时可以作为经典的 CGI 扫描器使用，但记住——它是内容扫描器而非漏洞扫描器。

更多信息：http://dirb.sourceforge.net/faq.txt

**用法** `dirb <url> <你的字典文件>`

**示例** `/dirb http://www.site.com/directory1/ wordlist.txt`

**示例** `/dirb http://www.site.com/ wordlist.txt,dirnamefile.txt`

## dirbuster

**描述** `DirBuster`是一个多线程 Java 应用，用于强制破解 Web/应用程序服务器上的目录和文件名。通常当某些东西看起来像处于默认安装状态的 Web 服务器时，实际上——它并非如此，而是隐藏了页面和应用程序。`DirBuster`尝试寻找

更多信息：https://www.owasp.org/index.php/Category:OWASP_DirBuster_Project

**用法** n/a；GUI 工具

```
n/a; GUI 工具
```

## vega

**描述** `Vega`是一个测试 Web 应用安全的开源平台。`Vega`可以帮助你发现并验证 SQL 注入、跨站脚本 (`XSS`)、无意中泄的敏感信息以及其他漏洞。

特性：

- 自动化爬虫和漏洞扫描器
- 一致的 UI
- 网站爬虫
- 拦截代理
- SSL MITM
- 内容分析
- 通过强大的 Javascript 模块 API 实现扩展性
- 可自定义的告警
- 数据库和共享数据模型

**用法** n/a；GUI 工具

**示例** n/a；GUI 工具

## webscarab

**描述** `WebScarab`是一个分析使用 HTTP 和 HTTPS 协议通信的应用的框架。它用 Java 编写，因此可以移植到许多平台。`WebScarab`有多种操作模式，由许多插件实现。在最常用的用法中，`WebScarab`作为拦截代理运行，允许操作员在请求发送到服务器之前查看并修改浏览器创建的请求，并在浏览器接收到服务器返回的响应之前查看并修改这些响应。`WebScarab`能够拦截 HTTP 和 HTTPS 通信。操作员还可以查看通过 `WebScarab`的对话内容（请求和响应）。

**更多信息：https://www.owasp.org/index.php/WebScarab_Getting_Started

**用法** n/a；GUI 工具

**示例** n/a；GUI 工具

## webslayer

**描述** `WebSlayer`是为强制破解 Web 应用设计的工具，它可以发现未链接的资源（目录、servlet、脚本等），强制破解 GET 和 POST 参数。

该工具具有强大的负载生成器和灵活的结果分析器。

更多信息：https://www.owasp.org/index.php/Category:Webslayer

**用法** n/a；GUI 工具

**示例** n/a；GUI 工具

## zapro

**描述** OWASP Zed Attack Proxy (`ZAP`)是一个用于测试 Web 应用的集成平台。对于新接触渗透测试的人来说，它是一个易于使用的工具箱，用于发现漏洞。

更多信息：https://code.google.com/p/zapproxy

**用法** n/a；GUI 工具

**示例** n/a；GUI 工具

## [29] 漏洞扫描器 (继续)

- `burpsuite`
- `cadaver`
- `deblaze`
- `fimap`
- `grabber`
- `joomscan`
- `nikto`
- `padbuster`
- `proxystrike`
- `skipfish`
- `sqlmap`
- `vega`
- `w3af`
- `wapiti`
- `webscarab`
- `webshag`
- `webshui`
- `websploit`
- `wpscan`
- `xsser`

**描述** `Burp Suite`是用于测试应用程序的集成平台。其组件包括：

- 拦截代理：允许你拦截并修改流量。
- 蜘蛛：映射应用程序。
- 入侵者：执行自动化攻击。
- 重复：重新发送请求。
- 序列：分析随机性。
- 扩展性：允许你编写插件。
- 扫描器：寻找漏洞。

更多信息：https://portigger.net/burp

**用法** n/a；GUI 工具

## cadaver

**描述** `cadaver`是一个用于 Unix 的命令行 WebDAV 客户端。它支持文件上传、下载、命名空间操作（移动/复制）以及锁定。

**用法** `cadaver hostname[:port]/path`

**选项** http://linux.net/man/1

**示例** `cadaver http://example.com:8022/Users/`

**示例** `cadaver https://secure.com/`（使用 SSL）

## davtest

**描述** `DAVTest`通过上传测试文件来测试启用 WebDAV 的服务器，并可以对目标执行命令或其他操作。

特性：

- 自动发送漏洞文件
- 使用 MKCOL 随机目录
- 使用 MOVE 发送文本文件
- 基本和摘要认证
- 自动清理上传的文件
- 发送任意文件

**用法** `davtest.pl -url <url> [options]`

**选项** https://code.google.com/p/davtest/wiki/Usage

**示例** `davtest.pl -url http://localhost/davdir`（在此位置测试上传）

**示例** `davtest.pl -url http://localhost/davdir -sendbd auto`（发送后门）

**示例** `davtest.pl -url http://localhost/davdir -auth user:pass -uploadfile backdoors/perl_cmd.pl -uploadloc perl.pl`（使用认证上传 `perl_cmd.pl` 并通过 `perl.pl` 调用）

## deblaze

**描述** `deblaze`是一个针对 flex 服务器的远程方法枚举工具。该工具允许你对 flex 远程端进行方法枚举和询问。`Deblaze`提供以下功能：

- 服务和方法强制破解
- 询问
- Flex 技术指纹识别
- 参数检测
- 基本参数模糊测试
- 代理 AMF 请求/响应
- HTML 报告

**用法** `deblaze [option]`

**选项** http://deblaze-tool.appspot.com/usage

**示例** `deblaze.py -u http://192.168.153:8080/amfphp/gateway.php -s securityService -m sendEmail -p test@test.com`

**示例** `python2.5 deblaze-0.3.py -P 8080:targetIP:targetPort`

**示例** `python deblaze.py -u http://192.168.153:8080/amfphp/gateway.php -s Discoveryservice -m getServices`

## fimap

**DESCRIPTION** `fimap`是一个轻型的 Python 工具，可以针对 Web 应用中的本地和远程文件包含漏洞进行发现、准备、审计、利用甚至自动通过 Google 搜索。`fimap`应该类似于 `sqlmap`，但它是专门用于 LFI/RFI 漏洞，而不是 `sqlmap`。`fimap`的主要目标是提高您网站的质量安全性。

更多信息：https://code.google.com/p/fimap

**USAGE** `./fimap.py [options]`

**OPTIONS** https://code.google.com/p/fimap/wiki/FimapHelpPage

- **EXAMPLE** `fimap -u http://localhost/vulnerable.php?inc=index.php`
- **EXAMPLE** `./fimap.py -u 'http://localhost/test.php?file=bang&id=23'` (扫描单个 URL 的 FFI 错误)
- **EXAMPLE** `./fimap.py -m -l /tmp/urlist.txt` (扫描 URL 列表中的 FFI 错误)
- **EXAMPLE** `./fimap.py -g -q 'inurl:include.php'` (扫描 Google 搜索结果中的 FFI 错误)
