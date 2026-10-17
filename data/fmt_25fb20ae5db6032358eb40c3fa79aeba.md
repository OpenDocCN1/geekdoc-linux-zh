
| zero.webwebapp.com | 07:12 PM | GET `/login.php?service=Freebank&CaastAcce...` | |

| zero.webwebapp.com | 07:12 PM | GET `/favicon.ico HTTP/1.1` | |

| zero.webwebapp.com | 07:29 PM | POST `/login.php HTTP/1.1` | |

查看 | 信息 信息 浏览器

| 请求 |

| --- |

| POST `/login.php HTTP/1.1` |

| Host: zero.webwebapp.com |

| User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36 |

| Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/weif,image/apng/*; |

| Accept-Encoding: gzip |

| Referer: http://zero.webwebapp.com/login.php |

| Connection: keep-alive |

| Content-Length: 31 |

| Content-Type: application/x-www-form-urlencoded |

| Search: 0 |

| Found: 4 |

| Requests: 1 |

图 15-3：使用 Firefox 开发者工具重置表单长度。

# 代码注入与 SQL 注入

与 URL 操控一样，利用的可能性存在，因此保持关注是有价值的。使用隐藏字段进行身份验证（登录）机制可能是危险的。我曾遇到过一个多因素身份验证入侵者锁定过程，它依赖隐藏字段来跟踪用户尝试登录的次数。该变量可以在每次登录尝试时重置为零，从而有助于脚本字典或暴力破解攻击。设计用于防止入侵攻击的安全控制措施容易受到入侵攻击的侵害，这有些讽刺。多个工具（例如商用漏洞扫描器自带的代理和 Burp Proxy）可以轻松地操控隐藏字段。图 15–3 显示了 WebInspect SPI 代理界面和网页的隐藏字段。如果你发现了隐藏字段，可以尝试操控它们来查看可以做什么。就这么简单。

## 第 15 章 Web 应用程序与移动应用 285

![](img/6f4b05e27c5ed3644d5304cc1cefc73c_300_0.png)

如果你闲得没命，你可能会手动发现这些类型的漏洞。然而，为了准确性（稳妥），此类攻击最好通过运行 Web 漏洞扫描器来实现，它可以快速地向 Web 系统发送数百次 URL 迭代来检测弱点。

## 隐藏字段操控

某些网站和应用程序在网页中嵌入隐藏字段，以便在 Web 服务器和浏览器之间传递状态信息。隐藏字段在 Web 表单中表示为 `<input type="hidden">`。由于编码实践不佳，隐藏字段通常包含机密信息（例如电子商务网站上的产品），这些信息应该仅存储在后端数据库中。用户不应该相信隐藏字段（名称），但好奇的攻击者可以发现并利用它们。要做到这一点，请遵循以下步骤：

- 1. 查看 HTML 源代码。

要在 Explorer 和 Firefox 中查看源代码，请右键点击页面并从上下文菜单中选择“查看源代码”或“查看页面源代码”。

![](img/6f4b05e27c5ed3644d5304cc1cefc73c_300_1.png)

- 2. 修改存储在这些字段中的信息。

例如，恶意用户可能会价格从 $100 改为 $10。

- 3. 将页面重新到服务器。

此步骤允许攻击者获得非法收益，例如在网上购买时获得更低的价格。

此类漏洞正变得稀少，但与 URL 操控一样，利用的可能性存在，因此保持关注是有价值的。

使用隐藏字段进行身份验证（登录）机制可能是危险的。我曾遇到过一个多因素身份验证入侵者锁定过程，它依赖隐藏字段来跟踪用户尝试登录的次数。该变量可以在每次登录尝试时重置为零，从而有助于脚本字典或暴力破解登录攻击。设计用于防止入侵攻击的安全控制措施容易受到入侵攻击的侵害，这有些讽刺。

![](img/6f4b05e27c5ed3644d5304cc1cefc73c_300_2.png)

多个工具（例如商用漏洞扫描器自带的代理和 Burp Proxy）可以轻松地操控隐藏字段。图 15–3 显示了 WebInspect SPI 代理界面和网页的隐藏字段。

如果你发现了隐藏字段，可以尝试操控它们来查看可以做什么。就这么简单。

## 未标题 - SPI 代理

| 主机 | 时间 | 请求 | 状态 |

| --- | --- | --- | --- |

| zero.webwebapp.com | 07:11 PM | GET `/HTTP/1.1` | |

| zero.webwebapp.com | 07:12 PM | GET `/login.php?service=Freebank&CaastAcce...` | |

| zero.webwebapp.com | 07:12 PM | GET `/favicon.ico HTTP/1.1` | |

| zero.webwebapp.com | 07:29 PM | POST `/login.php HTTP/1.1` | |

查看 | 信息 信息 浏览器

| 请求 |

| --- |

| POST `/login.php HTTP/1.1` |

| Host: zero.webwebapp.com |

| User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36 |

| Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/weif,image/apng/*; |

| Accept-Encoding: gzip |

| Referer: http://zero.webwebapp.com/login.php |

| Connection: keep-alive |

| Content-Length: 31 |

| Content-Type: application/x-www-form-urlencoded |

| Search: 0 |

| Found: 4 |

| Requests: 1 |

图 15-3：使用 Firefox 开发者工具重置表单长度。

# 代码注入与 SQL 注入

与 URL 操控一样，利用的可能性存在，因此保持关注是有价值的。

使用隐藏字段进行身份验证（登录）机制可能是危险的。我曾遇到过一个多因素身份验证入侵者锁定过程，它依赖隐藏字段来跟踪用户尝试登录的次数。该变量可以在每次登录尝试时重置为零，从而有助于脚本字典或暴力破解登录攻击。设计用于防止入侵攻击的安全控制措施容易受到入侵攻击的侵害，这有些讽刺。

## 第 15 章 Web 应用程序与移动应用 285

![](img/6f4b05e27c5ed3644d5304cc1cefc73c_300_0.png)

如果你闲得没命，你可能会手动发现这些类型的漏洞。然而，为了准确性（稳妥），此类攻击最好通过运行 Web 漏洞扫描器来实现，它可以快速地向 Web 系统发送数百次 URL 迭代来检测弱点。

# 盲注 SQL 注入

漏洞详情

| 参数 | 值 |

| --- | --- |

| 参数类型 | int |

| 参数名称 | id |

当攻击由查询触发，该查询被解释为 SQL 命令而不是数据库查询的普通数据时，就会发生盲注 SQL 注入。

攻击者可以通过观察应用程序响应（例如响应时间）从数据库中推断信息。

影响

- 攻击者可以从数据库、操作系统中提取敏感数据，并获取数据库服务器的控制权。

应采取的措施

- 使用参数化查询防止 SQL 注入。

| CWE | 评分 |

| --- | -- |

| PCI 3.1 | 7.5 |

| CWE-89 | 9.8 |

| CWE-20 | 6.1 |

| CWE-943 | 7.5 |

| CWE-50 | 5.9 |

| CAPEC | - |

| CVSS:3.1 | 9.8 (严重) |

![](img/6f4b05e27c5ed3644d5304cc1cefc73c_303_0.png)

在发现 SQL 漏洞时，你可能会在不尝试利用漏洞的情况下停止。这没关系。但为了看看我能进入数据库系统多深，我建议尽可能使用漏洞扫描器内置的 SQL 注入功能，以便你可以向管理层演示整个流程。
