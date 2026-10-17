
<!-- 此处注释 -->

代码中的注释通常供应用程序作者使用；拥有这些信息的攻击者可以洞察代码。ASP 或其他动态内容机制（PHP、SSI 等）中的注释对最终用户是不可直接可见的，但标准 HTML 中的注释是可见的（见图 11.1）。即使是简单的作者姓名或发布日期，也为后的用户名/密码猜测攻击提供了可能。

“清理”代码是有效的，可以确保最终用户不会获得过多的信息。查看应用程序源代码不仅可以让你寻找揭示性的注释，还能让你快速查看内部情况，以便更好地了解正在发生什么。这种方法论在章节中得到扩展。

# 破解自定义 Web 应用 • 第 11 章

## 图 11.1 HTML 中的注释

![](img/729efc56f204a2ebffb8295c3a2dfdfb_599_0.png)

## 定位可能的可交互区域

Web 应用攻击的基础主要在于更改或操纵客户端与应用程序之间的交互。因此，该方法的下一个逻辑步骤是寻找那些可能交互的区域。一个典型的例子是定位 Web 页面中的表单。表单可能是向 Web 应用传递参数的最的方法。

表单在 Web 页面很容易发现，并被 `<FORM>` 标签包裹。让我们来看下面的表单并识别关键元素：

```
 <FORM METHOD="POST" ACTION="http://www.sensepost.com/special_ops/login.asp">

<!-- body of the form --

<INPUT TYPE="TEXT" NAME="USERNAME" SIZE="20">

<INPUT TYPE="PASSWORD" NAME="PASSWORD" SIZE="20">

<INPUT TYPE="SUBMIT" VALUE="LOGIN" NAME="LOGIN">

<!-- body of the form ends --

</FORM>
```

第一行可以被视为表单的定义。它可以分解如下：
`METHOD="POST"`

`METHOD` 可以是 `GET` 或 `POST`。主要的区别在于表单数据传递给 CGI 程序的方式。如果使用 `GET` 方法，表单数据将简单地附加到从服务器请求的 URL 末尾。服务器端的 CGI 通过查询环境变量 `QUERY_STRING` 来访问发送的数据。如果我们的示例表单使用 HTTP `GET` 向服务器传递详细信息，那么以下将是提交操作的准确表示：

```
GET /special_ops/login.asp?USERNAME=Haroon&PASSWORD=secret&SUBMIT=

HTTP/1.0
```

![](img/729efc56f204a2ebffb8295c3a2dfdfb_599_1.png)
Accept: image/gif, text/html, /*
Accept-Language: en-us
User-Agent: Mozilla/4.0 (compatible; MSIE 5.0; Windows NT 5.0; .NET CLR 1.0.3705)
Host: www.sensepost.com

`GET` 方法通常是不受欢迎的，因为表单可能会被截断（URL 的允许长度有限制），并且因为它呈现了如此明显的篡改能力。

```
POST /special_ops/login.asp HTTP/1.0

Accept: image/gif, text/html, /*

Accept-Language: en-us

Content-Type: application/x-www-form-urlencoded

User-Agent: Mozilla/4.0 (compatible; MSIE 5.01; Windows NT 5.0; .NET CLR 1.0.3705)

Host: www.sensepost.com

Content-Length: 31

USERNAME=Haroon&PASSWORD=secret
```

在上面的表单中，我们使用了三种类型的输入：`TEXT`、`PASSWORD` 和 `SUBMIT` 类型。其他类型的输入可以是 `CHECKBOX`、`RADIO`、`TEXTAREA`、`OPTION` 和 `HIDDEN`。

攻击者寻找的交互性包含在表单中，但使用 `GET` 请求可以嵌套在 Web 页面上正常的、可点击的链接中，例如看起来无害的 `Next` 链接。它可能如下：

```
<A href="http://www.sensepost.com/special_ops/login.asp?USERNAME=Haroon&PASSWORD=secret">Next</A>
```

寻找可交互区域强化了该方法的上一步骤：查看源码以揭示信息。下一步涉及精确确定应用程序设计中的缺陷。

## 确定攻击向量

为了确定攻击者如何利用该应用程序，你首先需要对应用程序本身有全面的理解。你需要完全理解应用程序的功能、它被设计用来做什么的，并结合

![](img/729efc56f204a2ebffb8295c3a2dfdfb_600_0.png)

这些信息，思考攻击者可能做什么。通过理解应用程序的原始意图，你就可以识别其设计中的潜在缺陷。

这些缺陷大部分属于以下类型之一：

- 目录遍历
- 命令执行
- 跨站脚本攻击
- 参数传递
- 数据库查询

信息收集经常被忽视，但它可以是一个强大的起点。通过返回此类详尽的错误信息（针对一个简单的文件未找到错误），Web 应用向潜在攻击者泄露了大量信息。例如，路径 `/psis/imgview/inc/` 可能永远不会被发现。只需浏览到此目录就揭示了另一个漏洞：该目录在没有默认文档的情况下是可以索引的，这再次为潜在攻击者提供了比需要得多的信息。

此案例可以进一步推进：下载并浏览之前未见的源代码，以寻找可能存在漏洞的脚本。

Web 服务器的文档根。这确保了即使 Web 服务器允许列出目录，也会返回一个空白页面。

# 图 11.5 暴露的可索引目录

![](img/729efc56f204a2ebffb8295c3a2dfdfb_604_0.png)

## 目录遍历

目录遍历简单是指在目录之间导航。为了说明，我们在典型的 Windows 2000 机器上使用了 MS-DOS 提示符。
你应该看到以下内容：

Microsoft Windows 2000 [Version 5.00.2195]
(C) Copyright 1985-2000 Microsoft Corp.

```
C:\>
```

我的个人文档位于我的主目录下，该目录距离根目录隔了几层，即 `C:\SensePost\users\haroon`：

```
C:\
```

```
Temp

Windows

SensePost

Finances

Stuff

Office

Users
```

Haroon
Jaco
Chris
Charll
Blah
Blah2
Common Files
Program Files

如果我在我的主目录下执行 `dir` 命令，我将看到其中的所有文件。在处理目录时，点 (`.)` 和双点 (`..`) 分别表示当前目录和父目录。因此，命令 `dir .` 将有效地列出当前目录，而 `dir ..` 将列出父目录的内容。这可以进一步操作。在保持在我的主目录 `C:\Sense\users\haroon` 内的情况下，我可以通过执行 `dir ..\.\` 命令来列出根目录 `c:` 的内容。简而言之，这被称为遍历。

某些应用程序根据请求参数向用户提供图像或其他内容。当用户可以在请求的资源前加上点 (`.`)、双点 (`..`) 和斜杠 (`/`) 时，这些应用程序就会受到遍历攻击。例如，一个流行的 Web 数学程序根据用户输入的数据创建图像，然后使用随机名称将这些图像保存到托管服务器上的某个目录中。然后，通过指向新生成的 URL 在用户的浏览器中提供这些图像：

```
http://www.sensepost.com/WebApplication/SENSEAPP?SENSEStoreID=SP888808189_2408042780&StoreType=image/gif
```

这个问题在于 CGI 应用程序 `SENSEAPP` 未能过滤恶意的用户输入，并提供文档树内的任何文档。进入的用户可以进一步调整上述 URL，使其指向：

```
http://www.sensepost.com/WebApplication/SENSEAPP?SENSEStoreID=../../../../../../etc/passwd&StoreType=image/gif
```

在那里，他们只需通过遍历目录树，就可以请求目录层次结构中更高处的文件。在这种情况下，只需查看返回页面的源代码即可获得目标 Web 服务器梦寐的 `passwd` 文件。始终确保用户输入已过滤掉可能具有敌性的字符！

![](img/729efc56f204a2ebffb8295c3a2dfdfb_605_0.png)

## 命令执行
