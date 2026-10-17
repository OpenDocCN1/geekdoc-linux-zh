
| 11 | atmail | GET | `/js` |
| 10 | atmail | GET | `/browsersearch.js` |
| 9 | atmail | GET | `/js/Query-1.7.2.custom.m...` |
| 8 | atmail | GET | `/js/Query-1.3.2.js` |
| 7 | atmail | GET | `success.txt` |
| 6 | detectportal.com | GET | `/` |
| 5 | detectportal.com | GET | `success.txt` |
| 4 | detectportal.com | GET | `success.txt` |

图 8：Burp history 标签页

# Scope（范围）

浏览现代 Web 应用意味着我们的代理历史将包含许多我们不感兴趣的网站请求，例如第三方统计、广告网络等。为了简化我们感兴趣的请求的收集，BurpSuite 允许我们设置范围。此功能使得遍历收集请求变得更容易。在示例中，我们可以右键点击任何以斜杠结尾的请求并选择 `Add to scope`。注意，这将整个域名添加到范围。或者，在 Web 应用更特定的页面上执行此操作将仅将该页面添加到范围。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_21_0.png)

| # | Target | Method | URL | Edited |
|---|---|---|---|---|
| 24 | detectportal.com | GET | `success.txt` | |
| 23 | detectportal.com | GET | `success.txt` | |
| 22 | detectportal.com | GET | `success.txt` | |
| 21 | detectportal.com | GET | `/url/atmail/` | |
| 20 | detectportal.com | GET | `/scope/ Add to scope` | |
| 15 | atmail | GET | `/scope/ from here` | |
| 14 | atmail | GET | `/url/ Do not scan` | |
| 12 | atmail | GET | `/url/ Disable scan` | |
| 11 | atmail | GET | `/scope/ Send to intruder` | Ctrl+1 |
| 10 | atmail | GET | `/scope/ Send to Repeater` | Ctrl+R |
| 9 | atmail | GET | `/scope/ Send to Sequencer` | Ctrl+R |
| 8 | atmail | GET | | |

图 9：BurpSuite "Add to scope" 功能

一旦设置了范围，图 10 显示的提示告诉我们是否要停止捕不在范围的项目。我们选择 Yes。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_21_1.png)

图 10：BurpSuite 范围警告

# 高级 Web 攻击与利用

现在我们已经将 atmail 添加到范围，可以更改 HTTP history 过滤器设置为仅显示范围内的项目。通过点击过滤器框、选择 `Show only in-scope items` 并点击过滤器框以外来实现。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_22_0.png)

图 11：BurpSuite 显示范围内的项目

# Burp Suite 社区版 v1.7.33 - Temporary 项目

| # | Host | Method | URL | Params | Edited | Status | Length | MIME type |
|---|---|---|---|---|---|---|---|
| 14 | http:// | GET | `/images/favicon.ico` | | | 200 | 1415 | text |
| 12 | http:// | GET | `/js/rememberme.js` | | | 200 | 4451 | script |
| 11 | http:// | GET | `/wp-admin/` | | | 200 | 7548 | |
| 10 | http:// | GET | `/js/browsercheck.js` | | | 200 | 9508 | script |
| 9 | http:// | GET | `/js/query/query-ui-1.7.2.custom.m...` | | | 200 | 193036 | script |
| 8 | http:// | GET | `/js/query/query-1.2.min.js` | | | 200 | 57613 | script |
| 3 | http:// | GET | `/index.html` | | | 200 | 7883 | HTML |

图 12：Burpsuite history 仅显示范围内的项目

通过切换到 Target 选项卡并选择 Scope 子标签页来验证我们的范围已正确设置。

# OFFENSIVE SECURITY（攻击性安全）

Advanced Web Attacks and Exploitation

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_23_0.png)

Burp Intruder Repeater Window Help

Target Proxy Scanner Intruder Repeater Sequencer Decoder Comparer Extender

Site map Scope

Target Scope

定义当前工作的范围目标。此配置影响站点工具包含或排除 URL 路径的行为。

使用高级范围控制

Add Enabled Prefix

Edit http://atmail

Remove

Paste URL

Load ...

图 13：BurpSuite 范围列表

# 高级 Web 攻击与利用

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_25_0.png)

```
Request / HTTP/1.1
Host: example.com
Accept: *
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:52.0) Gecko/20100101 Firefox/52.0
Accept-Language: en-US,en;q=0.5
Upgrade-Insecure-Requests: 0
```

```
Response HTTP/1.1 200 OK
Date: Mon, 01 Oct 2018 21:59:44 GMT
Server: Apache/2.4.2 (Ubuntu)
Content-Type: text/html; charset=UTF-8
Set-Cookie: sessionid=65c4a7b8; path=/
Cache-Control: no-store, no-cache, must-revalidate, post-check, pre-check=0
```

Content-Length: 7450

```
<!DOCTYPE html PUBLIC "//W3C//HTML 4.01//EN"
 "http://www.w3.org/TR/html41/strict.dtd">
<html lang="en">
<meta http-equiv="Content-Type" content="UTF-8">
<title>Amail 6.6 Page Login</title>
<link rel="stylesheet" href="css/original.css" type="text/css">
<link rel="stylesheet" href="css/lang-en.lang-3.6.9224.css" type="text/css">
<<body>
<p>Page is in translations</p>
<form action="login/index" method="POST">
<input type="text" name="username" />
<input type="password" name="password" />
<input type="submit" value="Login" />
</form>
</body>
</html>
```

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_25_1.png)

7859 bytes | 87 millis

现在我们有了一个基响应，我们将对原始请求进行更改。具体来说，我们将 `Accept-Language` 请求头从 "en-US,q=0.5" 改为 "de"。换句话说，我们将尝试查看当我们指示 Amail 使用德语时，它是如何响应的。

```
Request / HTTP/1.1
Host: example.com
Accept: *
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:52.0) Gecko/20100101 Firefox/52.0
Accept-Language: de
```

```
Response HTTP/1.1 200 OK
Date: Mon, 01 Oct 2018 21:59:44 GMT
Server: Apache/2.4.2 (Ubuntu)
Content-Type: text/html; charset=UTF-8
Set-Cookie: sessionid=65c4a7b8; path=/
Cache-Control: no-store, no-cache, must-revalidate, post-check, pre-check=0
```

Content-Length: 7418

```
<!DOCTYPE html PUBLIC "//W3C//HTML 4.01//EN"
 "http://www.w3.org/TR/html41/strict.dtd">
<html lang="en">
<meta http-equiv="Content-Type" content="UTF-8">
<title>Amail 6.6 Page Login</title>
<link rel="stylesheet" href="css/original.css" type="text/css">
<link rel="stylesheet" href="css/lang-en.lang-3.6.9224.css" type="text/css">
<body><body>
<p>Page is in translations</p>
<form action="login/index" method="POST">
<input type="text" name="username" />
<input type="password" name="password" />
<input type="submit" value="Login" />
</form>
</body>
</html>
```

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_25_2.png)

7827 bytes | 91 millis

在第 16 页，我们已经可以看到响应头大小和内容长度的差异。为了更好地比较响应，我们可以使用 `Compare`（比较）功能。可以通过点击响应并选择 `Select to Compare`（选择比较）来激活此功能。

21

高级 Web 攻击与利用

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_26_0.png)

在切换到 `Comparator`（比较器）标签之前，我们将返回原始请求并重复相同的比较步骤，以看到我们有可以比较的不同响应（图 18, 19）。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_26_1.png)

图 18：Burp Repeater 重复请求和响应

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_26_2.png)

图 19：Burp Repeater 发送第二个响应

当我们切换到 `Comparator` 标签时，我们将看到 Burp 在各自的窗口中自动高亮了不同的响应。此时，我们有比较响应的单词或字节差异的选项。我们将选择 `Words`（图 20），因为在此实例中我们处理的是二进制响应。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_27_0.png)

图 20：BurpSuite Comparator 标签

比较结果显示在专用窗口中（图 21），Burp 允许我们使用颜色编码轻松识别 `Modified`、`Deleted` 和 `Added` 的差异。在本例中，我们处理的是修改差异，如图 21 所示。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_27_1.png)

图 21：BurpSuite Comparator 标签 - Words。这是一个非常简单的例子，它展示了在测试 Web 应用时，Repeater 和 Comparator 是非常有用的工具。

## 1.4 BurpDecoder

在检查现代 Web 应用时，我们经常遇到 HTTP 请求和响应中的编码数据。坦率地说，Burp 有一个在工作流中非常易用的通用解码工具。例如，我们切换到浏览器并对 atmail/php 执行 HTTP 请求。如果我们切换回 Burp 解码响应，就可以找到它。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_28_0.png)

| Host | Method | URL | Params | Status | Extension | Title |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| --- | --- | --- | --- | --- | --- | --- |
| 34 | atmail | `/` | | 404 | text | html (Not Found) |
| 34 | atmail | `/favicon.ico` | | 404 | image | ico (Not Found) |
| 34 | atmail | `/index.php` | | 200 | text | html |
| 14 | atmail | `/main.js` | | 200 | text | js |
| 13 | atmail | `/check.js` | | 200 | script | js |
| 13 | atmail | `/onerror.js` | | 200 | script | js |
| 9 | atmail | `/style.js` | | 200 | script | js |
| 8 | atmail | `/query?id=query-1.2-custom...` | | 200 | script | js |
| 4 | atmail | `/query?id=query-1.2-min.js` | | 200 | script | js |

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_28_1.png)

```javascript
function decode(string, quote_style) {
    if (quote_style === "") {
        var temp_str = "", entity = "";
    } else if (quote_style === "html") {
        var table = document.createElement('table');
        table.innerHTML = string;
        entity = table.firstChild;
    }
    temp_str = decodeURIComponent(string);
    return temp_str.replace(
```

查看图 22 中的 return 语句，我们看到某些字符经过了 URL 编码，因此更难解释。让我们突出该语句，右键点击并选择 `Send to Decoder`（发送到解码）。

# 高级 Web 攻击与利用

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_29_0.png)

拦截历史 Websockets 选项

过滤器：隐藏范围外项目：图像和通用二进制内容

| # | Host | Method | URL | Params | Status | Length | Extension | Title |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 33 | http://url | GET | `/favicon.ico` | | 404 | html | Not Found |
| 34 | http://url | GET | `/favicon.ico` | | 408 | html | Not Found |
| 13 | http://url | GET | `/images/favicon.co` | | 6529 | text | |
| 14 | http://url | GET | `/rememberme.js` | | 1415 | text | |
| 12 | http://url | GET | `/script.js` | | 4451 | script | |
