

# 第4章：应用程序调查

```
...为了简洁删除了页头信息...
XML/XSL (G:\WebRoot\XML\tsr\main.xml) 无效。
错误: 系统无法找到指定的对象。
位置: 行 0，列 0 <font face="Arial" size=2>
<p>Microsoft VBScript runtime </font><font face="Arial" size=2>
error '800a01a8'</font>
<p><font face="Arial" size=2>
需要对象: <mlObj.document.Element></p>
已发送 29, 接收 688: NOTOCKSCK
[root@middle]# getit.sh www.victim.com /tsr/main.asp?x=mps&opening, 3
www.victim.com [192.168.129.100] 80 (http) open
..为了简洁删除了其余页头信息...
<!DOCTYPE HTML PUBLIC "%W3C//DTD HTML 4.0 Transitional//EN">
<html
<head>
<meta http-equiv="Content-Type" content="text/html">
<meta name="description" content="Piper at the Gates of Dawn">
<meta name="keywords" content="Wish You Were Here">
..页面的其余部分...
```

参数 "x-mps&opening,3" 是应用程序使用的一个硬编码链接。也许 "x" 代表 XML，用于指示 main.asp 如何找到显示代码。
对一个似乎在 URL 中不接受参数字符串的页面发送请求，甚至可以产生有趣的响应：

```
[root@middle]# getit.sh www.victim.com /default.asp
www.victim.com [192.168.129.100] 80 (http) open
HTTP/1.1 500 Internal Server Error
Server: Microsoft-IIS/5.0
Date: Thu, 31 Jan 2002 07:15:46 GMT
Connection: Keep-Alive
Content-Length: 283
Content-Type: text/html
Set-Cookie: ASPSESSIONIDGQQQKFC=GPNGIM0FLDEAINOHDLLJJBFA; path=/
Cache-control: private
```

```
<font face="Arial" size=2>
<p>Microsoft VBScript runtime </font><font face="Arial" size=2>
error '800a0009'</font>
<p><font face="Arial" size=2>
下标越界: [number: 0]</p>
<font face="Arial" size=2>/default.asp</font>, 行 38
已发送 28, 接收 546: NOTOCKSCK
```

像是输入测试的候选！

# 攻击 Web 

收集参数是一项复杂的任务，在两个应用程序之间很少相同。在收集变量名和值时，观察某些趋势：

- 用户识别（User Identification）：寻找代表用户的值。这可能是用户名、社会安全号码，或者另一个与用户相关的值。这些信息被用于伪装攻击。相关字符串有 userid, user, name, uid。
/login?userid=2460

- 会话识别（Session Identification）：寻找在整个会话期间保持不变的值。Cookie 也会执行会话处理。某些应用程序会在 URL 上传递会话信息。相关字符串有 sessionid, session, s。
/menu.asp?id=89

- 数据库查询（Database Queries）：检查可能传递到数据库的任何值。常见值有 name, address, preferences 或其他输入。这些是输入验证和 SQL 注入攻击的完美候选。匹配 URL 操作的注入。
/submit.php?Title=Me&iPhone=8

- 搜索查询（Search Queries）：应用程序搜索页面总是接受查询字符串。它可能隐藏如何执行搜索、返回多少匹配项或搜索哪些文件。搜索页面在应用程序中是明显的。
/search?q=*maxret=100&sort=true

- 文件访问（File Access）：使用模板或自定义页面的某处提取格式信息。我们喜欢的攻击手段之一是操作此类 URL。相关的参数名有 template, file, temp。
/open.pl?template=simple

最后，应用程序程序员可能留下了几个参数。对于布尔参数（如 "debug"），将它们设置为 TRUE, T 或 1。

- debug
- dbg
- admin
- show

# 第4章：应用程序调查

# 后端连接

最后要收集的信息是后端连接的证据。注意何时从数据库读取或写入（例如更新地址或更改密码）。突出与数据库或其他系统相关的页面或内容。

WebDAV 选项允许 Web 服务器的远程管理。配置错误的服务器允许任何人上传、删除或浏览 Web 目录。检查它们是否启用：

```
[root@meddle.victim.com] # echo -e "OPTIONS * HTTP/1.1\n\n> Host: localhost\n\n" | nc -vv www.victim.com 80 > index.html
www.victim.com [192.168.33.101] 80 (http) open
HTTP/1.1 200 OK
Server: Microsoft-IIS/5.0
Date: Fri, 01 Feb 2002 08:49:48 GMT
MS-Author: Dav
Content-Length: 0
Accept-Ranges: none
DASL: <DAV:sql>
Public: OPTIONS, TRACE, GET, HEAD, DELETE, PUT, POST, COPY, MOVE,
MKCOL, PROFFIND, PROPATCH, LOCK, UNLOCK, SEARCH
Allow: OPTIONS, TRACE, GET, HEAD, COPY, PROFFIND, SEARCH, LOCK,
UNLOCK
Cache-Control: private
sent 38, rcvd 32
```

# 服务器头部

服务器返回的 HTTP Header 还显示了操作系统、服务器版本和额外的模块。毕竟头部并不总是可靠，隐藏信息至关重要。但当头部包含 WebDAV 版本时，可以使用这些信息获取应用程序的画像。

# 自动化调查的工具

几个工具自动化了应用程序的基础工作。它们基本上是爬虫；一旦你指向一个 URL，你就可以休息创建站点镜像。这并不是应用程序中每个可用链接的完整集合。

# lynx

| | |
|---|---|
| 优点 | 灵活、命令行、支持 SSL |
| 缺点 | 镜像站点时很笨拙 |
| 最终分析 | 非常适合检查单个 URL |

lynx (lynx.browser) 是许多系统中自带文本浏览器。它提供了一种导航网站的快速方法，尽管大量的 JavaScript 会抑制它。发现它最好的用途之一是下载特定页面。

-dump 选项对于其“引用”部分很有用。基本上，这指示 lynx 直接将页面转储到屏幕。你可以将输出重定向到文件。起初看起来可能没用，但它包含了嵌入 HTML 中的所有链接列表。这对于枚举带有长字符串的链接很有用。

```
[root@mobile]# lynx -dump https://www.victim.com > homepage
[root@mobile]# cat homepage
...为了简洁删除了文本内容...
```

# 引用

- 1. http://www.victim.com/signup?lang=en
- 2. http://www.victim.com/help?lang=en
- 3. http://www.victim.com/faq?lang=en
- 4. http://www.victim.com/menu/
- 5. http://www.victim.com/preferences?anon
- 6. http://www.victim.com/languages
- 7. http://www.victim.com/images/

