

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
METHOD="POST"

METHOD 可以是 GET 或 POST。主要的区别在于表单数据传递给 CGI 程序的方式。如果使用 GET 方法，表单数据将简单地附加到从服务器请求的 URL 末尾。服务器端的 CGI 通过查询环境变量 `QUERY_STRING` 来访问发送的数据。如果我们的示例表单使用 HTTP GET 向服务器传递详细信息，那么以下将是提交操作的准确表示：

```
GET /special_ops/login.asp?USERNAME=Haroon&PASSWORD=secret&SUBMIT=
HTTP/1.0
```

![](img/729efc56f204a2ebffb8295c3a2dfdfb_599_1.png)

Accept: image/gif, text/html, /*
Accept-Language: en-us
User-Agent: Mozilla/4.0 (compatible; MSIE 5.0; Windows NT 5.0; .NET CLR 1.0.3705)
Host: www.sensepost.com

GET 方法通常是不受欢迎的，因为表单可能会被截断（URL 的允许长度有限制），并且因为它呈现了如此明显的篡改能力。

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

在上面的表单中，我们使用了三种类型的输入：TEXT、PASSWORD 和 SUBMIT 类型。其他类型的输入可以是 CHECKBOX、RADIO、TEXTAREA、OPTION 和 HIDDEN。

攻击者寻找的交互性包含在表单中，但使用 GET 请求可以嵌套在 Web 页面上正常的、可点击的链接中，例如看起来无害的 Next 链接。它可能如下：

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

