
```
| 1: | <dtml-var standard_html_header>
| 2: | <image Files/>
| 3: | <dtml-call expr="REQUEST.set('expand_all',1)">
| 4: | <dtml-tree name="Folder1" branches="objectValues">
| 5: | <dtml-if expr="meta_type == 'Image">
| 6: | <IMG SRC="dtml-var name="icon">
| 7: | <a href="dtml-var name="tree-item-url"><dtml-var name="id"></a>
| 8: | <dtml-else>
| 9: | <IMG SRC="dtml-var name="tree-var id">
| 10: | </dtml-if>
| 11: | </dtml-tree>
| 12: | <dtml-var standard_html_footer>
```

在第 3 行，通过调用 `REQUEST.set` 将 `expand_all` 变量设置为 true，以指示树标签默认将其所有分支展开到叶子节点。打开树标签（第 4 行）并指定 `Folder1` 为树递归查找的文件夹。`dtml-tree` 的 `branches` 属性被设置为 `objectValues`（一个返回文件夹中所有对象的方法），而不是默认的 `methodValues`（该方法仅返回文件夹对象）。

在树的主体内部，我们使用 `dtml-if`（第 5 行）来检查当前对象是否为图像，该语句通过测试其 `meta_type` 值（All Zone 对象的属性）来判断。如果该对象是图像，我们显示其图标，并使用树标签提供的变量 `tree-item-url` 构建指向它的链接（第 6 行和第 7 行）；否则，仅插入图标和对象 ID（第 9 行）。随后关闭树标签的主体（第 11 行）。图 4-10 显示了文档的渲染输出。

![](img/43a28cce5475b2f487bf455365567fb6_109_0.png)

图 4-10：`Folder1` 的完整树结构视图

## 4.3.12 sendmail 标签

`sendmail` 标签使用标准邮件传输协议 `SMTP` 发送电子邮件。`sendmail` 标签的一个特点是不进行文本替换，这意味着发送电子邮件时不会将文本渲染到你的文档中。由于邮件文本不会出现在查看包含 `sendmail` 标签页面的用户面前，因此应该在页面的其他地方包含一条确认邮件已发送的消息。

`sendmail` 标签需要四个参数：一个 SMTP 主机地址或 Zope `mailhost` 地址；收件人地址；发件人地址以及主题。

最后三项既可以作为标签内部的属性指定（按照惯例），也可以以头行格式放置。一个头行由头字段后跟冒号、一个空格，然后相关数据组成。`sendmail` 标签的头字段应包含以下字段：

- To: [收件人地址]
- From: [接下来是发件人地址。此信息是可选的，但不能省略头字段]
- Subject: [邮件主题。此信息是可选的，但不能省略头字段]

消息文本紧随这些参数之后。主题行和消息文本之间必须至少有一个空行。

一旦调用 `sendmail` 标签，电子邮件就会发送。因此，最好将发送邮件消息的代码编写在一个单独的对象中，该对象仅为此目的而被调用。

### 4.3.12 "SampleMail" 示例

例如，根据下面的代码所示，Smith 女士将收到这封邮件（尽管使用邮件程序发送这封一次性邮件显然更有意义）。如果你通过许多 DTML 标签增强 `sendmail` 标签以实现动态布局，你可以使用 `sendmail` 标签从网站发送带有变量内容的邮件。

```
<sendmail smtphost="mail.mycompany.com">
To: smith@company.com
From: Michael Haze <Michael@wproductions.cde>
Subject: Your order
Dear Ms. Smith,
我很遗憾地通知您，您最近订的货物将延迟最多两天。
我们对您带来的任何不便表示歉意，并感谢您的耐心。
Best regards,
Michael Haze
</sendmail>
```

接下来的示例说明了两种 DTML 方法。DTML 方法 `form_dtml`（列表 4-1）生成一个表单，其中只需要输入地址、主题和实际消息。然后数据将传递给 DTML 方法 `sendmail`（列表 4-2），该方法包含用于发送指定消息的 `sendmail` 标签（`sendmail` 标签属性列表请参见表 4-15）。

#### 列表 4-1：form_dtml

```
<dtml-var standard_html_header>
<h2>Message</h2>
<form action="sendmail">
Sender: <input type="text" name="name"><br>
Recipient: <input type="text" name="address"><br>
Subject: <input type="text" name="subject"><br>
<textarea name="message" rows="10" cols="50"></textarea>
<input type="submit" value="Send Message">
</form>
<dtml-var standard_html_footer>
```

#### 列表 4-2：sendmail

```
<dtml-var standard_html_header>
<sendmail smtphost="mail.mycompany.com">
To: <dtml-var name="address">
From: <dtml-var name="name">
Subject: <dtml-var name="subject">
<dtml-var name="message">
</sendmail>
<dtml-var standard_html_footer>
```

使用 `sendmail` 标签发送的文件必须以文件对象的形式存在 Zope 服务器上；你不能直接从文件系统发送文件。要将文件从文件系统发送到系统设置，请先创建一个新的 Zope 文件对象并插入所需的文件。你可以在管理界面中看到你的文件对象，如图 4-12 所示。

| 编辑 | 查看 | 属性 | 安全 | 撤销 | 所有权 |

|---|---|---|---|---|---|

| 文件位于 /Book/wordfile | | | | | 帮助 |

| 你可以使用下面的表单更新此文件的数据。点击浏览按钮从本地计算机选择数据文件，并点击上传以更新文件内容。 | | | | | |

| 标题 | | | | | | |

| 内容类型 | application/msword | | | | | |

| 前提条件 | | | | | | |

| 最后修改时间 | 2001-05-28 02:53 | | | | | |

| 文件大小 | 35, 328 bytes | | | | | |

| 文件数据 | 保存更改 浏览... | | | | | |

图 4-12：文件对象的属性，包含要发送的文件

你可以使用此屏幕来确定相应的边界中正确设置了哪个 MIME 内容类型。接收者何时可以点击收到的文件并在关联程序中打开它——这取决于接收者用于查看邮件的邮件程序。

如果你使用 `name` 属性作为已标识文件类型的文件名，则不需要设置 `type` 属性。例如，`.doc` 文件扩展名表示文件是使用 Microsoft Word 创建的。如果 `name` 属性不包含扩展名，邮件客户端将无法找到应用程序。在这种情况下，必须设置 `type` 属性，否则文件将被视为“未指定类型”且不会与相应的应用程序关联。

在接下来的示例中，我们有两个文件：第一个在 Microsoft Word 中创建，其全名位于 `name` 属性中（因此不需要 `type` 属性）。第二个是图像文件，没有指定文件扩展名，并且必须设置内容类型。

```
<html-boundary name="Working with Zope Versions" disposition="attachment"
<html-var wordfile"
encode="base64">
<html-boundary type="image/bmp" name="spacecraft" disposition="attachment"
encode="7bit">
<html-var e_h.bmp>
```

</html-mime>

<html-sendmail>
