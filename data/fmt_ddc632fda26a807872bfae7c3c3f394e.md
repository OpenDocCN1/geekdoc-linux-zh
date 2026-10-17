
Cookie: `wordpress_test_cookie[]check=action_survey_answer&spcm=save=%58%7B%22%3A%2253%22%7Bid%3A%22id%22%3A%2221550849657%22%5C%22aid%22%3A%223%3A%2270%5D```

图 321：从调查捕获的请求

# 使用 Kali Linux 进行渗透测试 2.0

# 攻击性安全
www.offensive-security.com

现在当我们刷新页面时，我们注意到漏洞利用程序提到的 cookie 是存在漏洞的![](img/f99f528ca9845f4c256ce54e882b1345_753_0.png)图 322：带有漏洞的 Cookie

使用此 cookie 我们可以开始尝试利用漏洞。

# 使用 Kali Linux 进行渗透测试 2.0

## 2 SQL 注入利用

现在我们已经捕获了一个带有漏洞的请求，可以使用 Burp 的 `Repeater` 来尝试 SQL 注入。要这样做，我们在 Burp 的 `HTTP History` 中找到包含 cookie 的请求，右键点击它并选择 `Send to Repeater`。

| Dashboard | Target | Intruder | Repeater | Decoder | Extender | Project options | User options |
| Intercept | HTTP history | Websockets history | Options | | | | |
| | Host | URL | Params | Edited | Status | Length | |
| 38 | http://sandbox.local | GET | /wp-content/plugins/element... | ✓ | 200 | 12490 | |
| 39 | http://sandbox.local | GET | /wp-content/plugins/element... | ✓ | 200 | 125872 | |
| 40 | http://sandbox.local | GET | /wp-content/plugins/element... | ✓ | 200 | 47443 | |
| 41 | http://sandbox.local | GET | /wp-content/plugins/element... | ✓ | 200 | 93582 | |
| 45 | http://sandbox.local | GET | /wp-content/plugins/element... | ✓ | 200 | 9382 | |
| 51 | http://detectopalx.com | POST | /success.php?admin=ajax.php | | 200 | 531 | |
| 54 | http://sandbox.local | GET | /wp-content/js/query-migrate... | | 200 | 84220 | |
| 70 | http://sandbox.local | GET | /wp-includes/js/query... | ✓ | 200 | 10348 | |
| 71 | http://sandbox.local | GET | /wp-includes/js/query... | ✓ | 200 | 97166 | |
| 72 | http://sandbox.local | GET | /wp-content/embed.min.js?ver... | ✓ | 200 | 1689 | |
| 73 | http://sandbox.local | GET | /wp-content/plugins/elementassets... | ✓ | 200 | 124594 | |
| 74 | http://sandbox.local | GET | /wp-content/plugins/elementassets... | ✓ | 200 | 47443 | |
| 75 | http://sandbox.local | GET | /wp-includes/js/query/core.min?... | ✓ | 200 | 4221 | |

过滤：隐藏图像和通用内容

```
GET /index.php HTTP/1.1

Host: sandbox.local

User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:68.0) Gecko/2010101 Firefox/68.0

Accept: text/html,application/xml,application/xml;q=0.9/*;q=0.8

Accept-Encoding: gzip, deflate

Connection: keep-alive

Cookie: wordpress_test_cookie=WP+Cookie+check= 
```

![](img/f99f528ca9845f4c256ce54e882b1345_754_1.png)

# 使用 Kali Linux 进行渗透测试 2.0

![](img/f99f528ca9845f4c256ce54e882b1345_755_0.png)

然后我们点击 `Repeater` 标签页以原始形式查看 cookie。

![](img/f99f528ca9845f4c256ce54e882b1345_755_1.png)

图 34：在 Repeater 中查看请求

让我们从原始漏洞利用程序获取载荷，将其放入 cookie 中并将请求发送到服务器。载荷可以在列表 865 中找到。

```
GET /HTTP/1.1

Host: sandbox.test.local

User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv/68.0) Gecko/2010101 Firefox/68.0

Accept: text/html,application/xml,application/xml;q=0.9/*;q=0.8

Accept-Encoding: gzip, deflate

Connection: close

Cookie: wordpress_test_cookie=WP+Cookie+check; wp_sap=1

124

Content-Type: application/x-form-urlencoded; charset=UTF-8

X-Requested: XMLHttpRequest

Content-Length: 124
```

列表 865 - 原始 SQL 注入载荷

# 使用 Kali Linux 2.0 进行渗透测试

根据利用程序，负载可以被插入到 `wp_sap` cookie 变量值中。cookie 变量的值从 `"` 之后开始，以分号结束。

![](img/f99f528ca9845f4c256ce54e882b1345_756_0.png)

利用程序代码提到，SQL 注入的结果将放置在 sss 内部的 `sss_params` 变量中。搜索气泡将带我们到达 SQL 注入输出的位置。

图 325：使用 Payload 发送请求

我们还可以设置 `自动滚动` 到此位置，以便于利用，这样我们就不需要每次都滚动查找输出。
