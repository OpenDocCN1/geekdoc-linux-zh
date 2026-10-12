
`Weekday` 是星期，`DD` 是日期，`Mon` 是月份的前三个字母，`YY` 是年份（例如 02），`HH` 是小时，`MM` 是分钟，`SS` 是秒。始终使用 GMT 时区。示例日期

```
Monday, 20-Sep-10 12:00:00 GMT
```

代表 GMT 时间 2010 年 9 月 20 日。虽然 Cookie 以两位格式存储年份，但它们并不存在 2000 年问题（Y2K）。浏览器接受 2010 年这个年份。如果 Cookie 在 21 世纪中期仍然存在，那个时代的浏览器将需要更新以支持该世纪后半部分的日期。指定长期用户偏好的 Cookie 应该指定几年的过期日期，以确保在未来需要时可以使用 Cookie。指定短期状态信息的 Cookie 应在几天后过期，届时过期的（旧的）Cookie 将被自动删除。

# path=PATH 字段

该字段为与 Cookie 关联的 URL 指定一个更通用的路径。例如，假设一个 CGI 程序的 URL 是 `path=PATH`。`path` 字段指定 Cookie 应用的路径。

# domain=DOMAIN_NAME 字段

当 Cookie 存储在本地时，`domain` 字段指定 Cookie 应该应用的更多域名。例如，假设一个 CGI 程序的 URL 具有 `domain=DOMAIN_NAME`。`domain` 字段将 Cookie 与所有主机关联，而不仅仅是一个主机。

# secure 字段

如果指定了 `secure`，Cookie 将通过安全通信通道（HTTPS）发送。

![](img/6e99147f217994f89499215b2cff677f_211_0.png)

> 注意
>
> 你可以在 http://www.netscape.org/edoc/cookie/ 找到 Netscape 关于 Cookie 的原始文档。

# 使用 Cookie 为 Cookie

开发提供了强大的功能，但在 CGI 程序中使用它们可能会有些混乱。你必须设计程序通过响应头部发送 Cookie，并通过请求头部接收 Cookie。虽然这实现起来并不困难，但意味着更多的处理是在服务器上而不是浏览器进行的。相反，JavaScript 可以通过在浏览器本地读取和设置 Cookie 来充分利用 Cookie，消除了由 CGI 程序处理 Cookie 的需求。JavaScript 脚本可以转发 CGI 程序执行所需的任何信息。通过使用 JavaScript 维护 Cookie 并尽可能在浏览器上执行操作，可以简化并在某些情况下消除 CGI 程序。

你使用 `document.cookie` 属性设置与文档关联的 Cookie。设置 Cookie 时必须提供与 CGI 程序相同的 Cookie 字段。例如，考虑以下语句：

```
email="jamie@jaworski.com"
expirationDate="Thursday, 01-Dec-11 12:00:00 GMT"
document.cookie="email="+email+";expires="+expirationDate
```

这些语句将当前文档的 `cookie` 属性设置为字符串 `"email=jamie@jaworski.com; expires=Thursday, 01-Dec-11 12:00:00 GMT"`。注意，需要 `expires` 字段防止 Cookie 在当前浏览器会话后过期。设置 cookie 属性时还可以使用 `domain`、`path` 和 `secure` 字段。

当使用以下语句检索 Cookie 值时，`cookieString` 被赋值为 `"email=jamie@jaworski.com"`：

`cookieString=document.cookie`

如果当前文档设置了多个 Cookie，`cookieString` 将包含一组由分号分隔的名称=值值对。例如，考虑以下语句：

```
email="jamie@jaworski.com"
firstName="Jamie"
lastName="Jaworski"
expirationDate="Thursday, 01-Dec-11 12:00:00 GMT"
document.cookie="email="+email+";expires="+expirationDate"
document.cookie="firstName="+firstName+";expires="+expirationDate"
document.cookie="lastName="+lastName+";expires="+expirationDate"
```

# 第六章 186

`cookieString` 的值包含了 `email`、`firstName` 和 `lastName` cookie 的 `name=value` 键值对。此值值为 "email=jamie@jaworski.com; firstName=Jamie; lastName=Jaworski"。

为了直感受如何通过 JavaScript 访问 cookie，请运行列表 6.6 中的 `cooktest.htm` 文件。它会显示图 6.6 所示的表单。该表单允许你输入 cookie 文本并通过点击 Set Cookie 按钮来设置 cookie。新的新值将显示在网页顶部。

### 列表 6.6：Cookie 测试程序 (cooktest.htm)

```html
<HTML>
<HEAD>
<TITLE>Cookie Test</TITLE><!--
<SCRIPT LANGUAGE="JavaScript">
function updateCookie() {
document.cookie=document.form1.cookie.value
location.reload(true)
}
--></SCRIPT>
</HEAD>
<BODY>
<SCRIPT LANGUAGE="JavaScript">
document.write("Your current cookie value is: ' + document.cookie+"")
</SCRIPT>
<FORM ACTION="" NAME="form1">
<P>Enter new cookie: <INPUT TYPE="TEXT" SIZE="60" NAME="cookie"/></P>
<INPUT TYPE="BUTTON" NAME="setCookie" VALUE="Set Cookie" onclick="updateCookie()">
</FORM>
</BODY>
</HTML>
```

要查看脚本如何工作，请输入图 6.7 所示的 cookie 并点击 Set Cookie 按钮。新的 cookie 将显示出来，如图 6.8 所示。通过实验此程序：输入具有不同或无过期日期的 cookie，关闭浏览器并重启，以查看哪些 cookie 在浏览器会话之间持久存在。

### 使用隐藏字段和 Cookie

![](img/6e99147f217994f89499215b2cff677f_214_0.png)

**图 6.6：** Cookie 测试程序的启动界面告诉用户当前的 cookie 值，并提示他们输入新的 cookie。（列表 6.6）

![](img/6e99147f217994f89499215b2cff677f_214_1.png)

**图 6.7：** 如何输入 cookie 文本的示例。（列表 6.6）

![](img/6e99147f217994f89499215b2cff677f_215_0.png)

图 6.8：当页面重新加载时，将显示新的 cookie。（列表 6.6）

Cookie 测试程序非常简单。这证明了 JavaScript 支持 cookie 的强大和灵活。该程序由两个脚本组成：一个在文档头部（head），一个在文档正文（body）。正文中的脚本显示文档可用的当前 cookie 值。头部的脚本通过设置用户输入值的 cookie 来处理与 Next Cookie 按钮关联的 onClick 事件。然后它会重新加载当前的 cookie 测试 .htm 文档，以便显示更新后的 cookie 值。请注意，cookie 测试程序在本地运行，不需要 CGI 程序。对于不需要从用户收集信息的 Web 应用程序，在许多情况下，JavaScript 和 cookie 的结合可以消除开发 CGI 程序的需求。

作为另一个结合 JavaScript 和 cookie 构建完全在浏览器上运行的 Web 的示例，让我们开发一个测试用户对历史事实理解程度的 JavaScript 应用程序。用浏览器打开 `quiz.htm`；它会显示图 6.9 所示的网页。点击对应正确答案的单选按钮，然后点击 Continue 按钮。网页将重新显示，并带有新问题和更新的分数。如果你选择了错误答案，会收到警告消息通知，并重新显示问题。当你成功回答测验中的所有问题时，将看到图 6.10 所示的网页向你祝贺。

![](img/6e99147f217994f89499215b2cff677f_216_0.png)
