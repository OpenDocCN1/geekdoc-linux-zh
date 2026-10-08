

# 破解 Web 应用 (Hacking Exposed Web Applications)

暴露（可能还有几个网站想要称霸世界）。客户端技术依赖于将“状态信息”发送给客户端，并信任客户端原封不动地返回这些信息。简而言之，客户端是不可信的。每当信息离开服务器时，例如 cookie 值，客户端都可以修改 cookie 以包含任意信息。如果你遇到一个执行状态管理的 Web 服务器，那么几乎可以确定状态信息正在被传递给客户端。它也极可能是不安全的。

由于客户端技术被频繁使用，它们必须具有某些优势。客户端技术的主要优势是，它们特别在具有 Web 农场（Web farm）的负载均衡架构中运行得非常良好。传入的请求可以分发到最空闲的服务器上，而无需担心服务器应该如何响应。服务器会检查状态信息，在数据库中查找，检查购物车，并返回适当的数据。另一方面，负载均衡器正变得越来越智能，可以处理涉及多个服务器的单个会话（session）。现在，让我们来看一些存储状态信息的载体。

## 隐藏字段 (Hidden Fields)

隐藏表单很容易识别，因此我们从这一类开始。隐藏字段并不意味着安全性低，但它可能是一个指标。让我们看看从应用程序登录页面创建的 FORM 是什么样的：

```html
<FORM name=login_form https://login.victim.com/config/login4r0naidr6d3 method=post>
<INPUT name=Tries type=hidden><INPUT value=us name=I8N type=hidden>
<INPUT name=Bypass type=hidden><INPUT value=64mbvjoubdp06 name=hidden type=hidden><INPUT value=pVj3sXMRJKD8lggZTYDLWNY_name=Challenge type=hidden>
User Name:<INPUT name=Login>
Password:<INPUT type=password maxLength=32 value="" name=Passwd>
```

当用户提交用户名和密码时，她实际上向服务器提交了七项信息，尽管在 Web 页面上只有两项是可见的。表 7-2 总结了这些值。

从这里看出，似乎有两个隐藏字段正在跟踪状态信息，“Tries”和“U”。目前还不清楚是否存在漏洞。请记住，我们需要先识别出所有的状态机制。

> 当我们继续研究会话管理技术时，我们一定会触及 Web 安全的其他方面。会话管理对于应用程序处理身份验证和授权的方式关关。此外，从客户端收集的数据始终受到输入验证和攻击的影响。安全性测试确实需要应用程序的全局视角。

## 第 7 章：攻击会话状态管理

| Value | 描述 |
| --- | --- |
| Tries | 可能代表用户从现在起尝试登录账户的次数，因为我们还没有提交密码。如果我们想发起暴力破解攻击，我们会尝试将此数字保持为零。如果此值超过某个阈值，服务器可能会锁定账户。潜在漏洞：应用程序强制锁定账户以保护自己免受暴力破解；然而；锁定变量携带在客户端侧，可以被轻易地修改。 |
| I8N | 该字段的值被设置为 "us"。由于它似乎在处理网站的语言，更改此值可能对会话不会产生任何安全影响。潜在漏洞：该字段仍可能受到输入验证攻击。请参阅第 8 章以获取更多信息。 |
| Bypass | 这是一个听起来很兴奋的字段名。bypass（绕过）需要特定的字符串吗？或者它可以是一个布尔值，允许用户在不需要密码的情况下登录？潜在漏洞：作为授权攻击的绕过登录页面（第 6 章）。 |
| U | 未知字段。这可能包含会话标识符或应用程序信息。至少，它值得调查。请查看本章后半部分的“SessionID 分析”部分以获取如何检查未知值的想法。潜在漏洞：可能包含已编码（易于破解）或加密（难以破解）的敏感信息。 |
| Challenge | 此字符串可能是挑战-响应身份验证机制的一部分。 |
| Login | 用户的登录名。 |
| Passwd | 用户的密码。 |

表 7-2. 隐藏字段示例值

## URL

再次看一眼上一节中的 FORM 示例。在 FORM 的 action 元素中还有另一个隐藏的“字段”：

```html
<FORM name=login_form action=https://login.victim.com/config/login?4fr0naidr6d3 method=post>
```

会话变量并不非要在 SET 中才能让顺序跟踪它们。服务器可以设置针对特定用户自定义的参数或重定向。其他示例可能如下所示：

```
/redirect.html/103-673347-6580661/
/ViewBase#sidrS5J5iOEEACi6r0E2ksQJnUEiakKFH/
/index.php?session_id=E3DF0FC4C-E5F7-4844-8DD9-4808906D85
```

在后一种情况下，“sid”名称提供了会话 ID。在 URL 中携带会话 ID 并不安全，但有许多点需要注意。

- *HTTPS*：如果会话 ID 可以从另一台计算机解码，恶意用户可以清除明文 HTTP 连接以伪造其他用户。
- *书签*：用户可能会对包含会话 ID 的 URL 建立书签。
- *内容*：这适用于任何会话 ID。请参阅本章的“内容”。如果内容可以被解码，则会话 ID 是安全的。

## HTTP 头部 (HTTP Headers) 和 Cookie

Cookie 值可能是最常用的方法。临时性（非持久性）Cookie 用于跟踪状态。浏览器在关闭时会删除它们。持久性 Cookie 存储在用户的计算机上。这是一个示例：

```
Set-Cookie: NAME=VALUE; expires=Sat,01-Jan-2023 GMT; path=/; domain=DOMAIN_NAME
```

这意味着 Cookie 是通过 HTTP 发送。“记住我”的网站使用持久性 Cookie。这是一个示例：

```
Set-Cookie: autolog=bWlrZteXMzYIdA3D%3D%3D; expires=Sat,01-Jan-2023 GMT;
```

## 过期时间 (Expire Times)

当你从使用持久性 Cookie 的应用程序注销时，通常的行为是将 Cookie 值设置为过去的某个过期时间。这会删除 cookie。应用程序可能还会使用过期时间强制用户每 20 分钟重新验证身份。该 Cookie 从用户首次身份验证起有效 20 分钟。当 Cookie 过期后，浏览器会删除它。应用程序消失并请求新的凭据。这似乎是一种有效的会话超时方法，但前提是必须正确执行。如果应用程序设置了一个 20 分钟过期的“密码”：

```
Set-Cookie: HasPwd=451jh28f;expires=Tue,17-Apr-2002 12:00 GMT; path=/; domain=victim.com
```

然后扩展过期时间并查看服务器是否尊重该 Cookie：

```
Set-Cookie: HasPwd=451jh28f;expires=Tue,17-Apr-2003 12:00 GMT; path=/; domain=victim.com
```

通过这种方法你可以判断是否存在对会话时间的服务器控制。如果这个有效的 20 分钟加一年的 Cookie 持续了一小时，那么你就知道 20 分钟的窗口是任意的——服务器正在执行 60 分钟的硬超时。

## HTTP Referer

我们见过网站使用 HTTP Referer（是的，就是这样拼写的）头部来处理会话和身份验证。这与在 URL 中传递状态类似，但必须使用像 Achilles这样的这样的来捕获。

## 服务端技术 (SERVER-SIDE TECHNIQUES)

服务器端会话跟踪技术往往比将信息传输给客户端的技术更强大。当然，没有任何服务器端技术会保留客户端的所有状态信息。毕竟，必须识别用户。服务器端技术的区别在于，个人资料、权限和购物车信息等状态信息都存储在服务器上。客户端只传递单个会话 ID 作为标识。

