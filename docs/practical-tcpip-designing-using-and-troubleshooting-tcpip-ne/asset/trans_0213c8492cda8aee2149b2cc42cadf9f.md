
## 附录 14 嵌套的 MIME 附件

这基于 RFC-2045 中的一个示例。如果将图 A14.1 的内容作为消息发送，在 Outlook Express 中将其显示为图 A14.2 所示。图 A14.3 展示了分隔符如何将消息结构化为多个嵌套的附件。

### 图 A14.1
包含嵌套 MIME 附件的消息内容

```
MIME-Version: 1.0
From: fred@example.com
To: jim@example.com
Date: Sat, 23 Mar 2002 12:15:17 +0000 (GMT)
Subject: A multipart example
Content-Type: multipart/mixed; boundary=unique-boundary-1

This is the preamble area of a multipart message.
Mail readers that understand multipart format
should ignore this preamble.

If you are reading this text, you might want to
consider changing to a mail reader that understands
how to properly display multipart messages.

--unique-boundary-1
This is the first attachment.
(Note that the blank between the boundary and the start of the text in
this part means no header fields were given and this is text in the
US-ASCII character set.)

--unique-boundary-1
Content-type: text/plain; charset=US-ASCII

This could have been part of the previous part, but illustrates
explicit versus implicit content-type specification for body parts.

--unique-boundary-1
Content-Type: multipart/parallel; boundary=another-separator

--another-separator
Content-Type: audio/basic
Content-Transfer-Encoding: base64

 [audio data goes here]
--another-separator
Content-Type: message/rfc822

From: jane@example.com
To: mary@example.com
Subject: hi!
Date: Fri, 22 Mar 2002 12:34:56 +0000 (GMT)
Content-Type: Text/plain; charset=ISO-8859-1
Content-Transfer-Encoding: Quoted-printable

Hello Mary
--another-separator
Content-Type: image/jpeg
Content-Transfer-Encoding: base64

 [image data goes here ...]
--another-separator--

--unique-boundary-1
Content-type: text/enriched

This is <bold><italic>enriched</italic></bold>
<smaller>as defined in RFC 1896</smaller>
Isn't it
<bigger><bigger>cool?</bigger></bigger>
--unique-boundary-1--
```

![](img/a2132b646d336d5f9a21102d6320e537_824_0.png)

图 A14.2 在 Outlook Express 中查看图 A14.1 的消息

![](img/a2132b646d336d5f9a21102d6320e537_824_1.png)

图 A14.3 分隔符如何组织消息内的附件

## 附录 15 IMAP 会话示例

在图 A15.1 中，我们使用 **telnet** 连接到服务器 Bob 上的 IMAP 知名端口。与 POP 和 SMTP 示例一样，为了清晰起见，我们将服务器的响应进行了缩进，并截断了一些行以节省空间。

与 POP 和 SMTP 的一个区别是，当您输入 IMAP 命令时，必须为其添加一个 *标签*（tag）前缀——用作标签的文本字符串。（您可以使用任意字符串，只要每个字符串在此会话中是唯一的即可。）当 IMAP 服务器对命令做出响应时，它会使用该命令的标签作为输出的前缀，以表明输出所关联的内容。这是必要的，因为 IMAP 客户端/服务器的交互是异步的，即对命令的响应不一定按照输入命令的顺序输出，并且您可以在早期命令完成之前输入另一个命令。之所以这样做是因为某些 IMAP 命令（例如大型搜索）可能需要很长时间，服务器可能不会立即响应，但*会*允许您输入进一步的命令。输出多行的命令在所有输出行上（最后一行除外）都显示星号（“*”）作为标签，最后一行则像往常一样显示输入标签，如果命令成功则接着显示 **OK**，如果失败则显示 **BAD**。

以下是图 A15.1 中会话的逐行解释：

- a1 **以用户 bex15 登录并提供密码。**（a1 是我们决定使用的第一个唯一标签。）服务器回复说登录成功，并使用我们输入的相同标签作为响应的前缀 – a1
- a2 **SELECT** 指定我们要使用的邮箱，在此情况下为 */htiw/imap/mbox*。服务器回复该邮箱包含三条消息，并给出了其他详细信息
- a3 **SEARCH** 在此邮箱中搜索 **SUBJECT** 头包含单词“elephants”且 **FROM** 头包含“snit”的消息。我们可以通过附加条件来指定更多标准，例如 **SUBJECT** “elephants” TO “fred@aw.com” NOT FROM “bex8@uit.co.uk” 服务器回复匹配消息的编号 – 在本例中为编号 2 和 3
- a4 **FETCH** 消息 2 和 3，并列出我们指定的头部
- a5 **告诉我消息 1 的 MIME 结构。**（我们编辑了输出以更清晰地显示结构。通常人类不会看到此输出，因此其视觉格式并不重要。）
  - 此消息是一个 **multipart/mixed**，包含一个文本附件和一个 GIF 文件附件
- a6 **仅检索消息 1 的第一个（纯文本）附件。** 该附件内容为“This message has one line of text and a small GIF image attached.”
- a7 **退出登录。**

```
alice# telnet bob imap
Trying 192.0.2.63.
Connected to localhost.
Escape character is '^]'.
* OK localhost IMAP4rev1 v1.264 server ready
a1 login bex15 xcc
a1 OK LOGIN completed
a2 SELECT /htiw/imap/mbx
* 3 EXISTS
* 0 RECENT
* OK [UIDVALIDITY 995036481] UID validity status
* OK [UNINDEX 4] Predicted next UID
* FLAGS (\Answered \Flagged \Deleted \Draft \Seen)
* OK [PERMANENTFLAGS (\* \Answered \Flagged \Deleted \Draft \Seen)] Permana
a2 OK [READ-WRITE] SELECT completed
a3 SEARCH SUBJECT "elephants" FROM "snit"
* SEARCH 2 3
a3 OK SEARCH completed
a4 FETCH 2,3 (BODY[HEADER.FIELDS (DATE FROM TO SUBJECT)])
* 2 FETCH (BODY[HEADER.FIELDS ("DATE" "FROM" "TO" "SUBJECT")] {142}
From: "Trudo von Snit" trudo@example.com
Date: Fri, 13 Jul 2001 15:51:46 +0100
To: bex15@uit.co.uk
Subject: Mice are desktop elephants

* 3 FETCH (BODY[HEADER.FIELDS ("DATE" "FROM" "TO" "SUBJECT")] {167}
From: "Trudo von Snit" trudo@example.com
Date: Fri, 13 Jul 2001 15:52:31 +0100
To: bex15@uit.co.uk
Subject: Assembly programmers hunt elephants on their knees

a4 OK FETCH completed
a5 FETCH 1 (BODYSTRUCTURE)
* 1 FETCH

       (BODYSTRUCTURE
       (
              ("TEXT" "PLAIN" ("CHARSET" "us-ascii") NIL NIL "7BIT" 67 1 NIL
              ("IMAGE" "GIF" ("NAME" "dir.gif") NIL NIL "BASE64" 188 NIL NIL
              "MIXED" ("BOUNDARY" "PART-BOUNDARY= 21010713154504.2MS863.dennis"))
       ))

a5 OK FETCH completed
a6 FETCH 1 (BODY[1])
* 1 FETCH (BODY[1] {67}
This message has one line of text and a small GIF image attached.

a6 OK FETCH completed
a7 LOGOUT
* BYE bob.uit.co.uk IMAP4rev1 server terminating connection
a7 OK LOGOUT completed
Connection closed by foreign host.
alice#
```

**图 A15.1** 使用 telnet 作为客户端的 IMAP 会话示例

## 附录 16 安装 ethereal；ethereal 字段名称

**ethereal** 网站，提供下载和文档，地址为：

- [http://www.ethereal.com](http://www.ethereal.com) *Ethereal – 嗅探维持互联网连接的胶水*

有一份有用的用户手册可供获取：

- [http://www.ethereal.com/docs/user-guide/](http://www.ethereal.com/docs/user-guide/) *Ethereal 用户指南*

### 在 Linux 上安装 ethereal

如今，与大多数软件工具一样，安装时您有两种选择：要么下载源代码，构建它并从中安装，要么下载并安装已为您的 Linux 版本预构建的二进制包。对于 **ethereal**，我们一直选择二进制包路径，因为它非常快速且简单。另一方面，如果您想要最新版本，通常必须从源代码构建；幸运的是，这通常非常简单。**ethereal** 网站提供了适用于六种不同 Linux 版本的二进制包，您可以在常用的特定 Linux 发行版网站上找到特定版本的包。

有关在 Linux 上构建和安装的详细信息，请参阅《Ethereal 用户指南》第 2 章：

- [http://www.ethereal.com/docs/user-guide/](http://www.ethereal.com/docs/user-guide/) > 2. 构建和安装 Ethereal

### 在 Windows 上安装 ethereal

在 Windows 上从源代码构建 **ethereal** 的文档并不完善，因此最好从二进制包安装，可从以下地址下载：

- [http://www.ethereal.com/distribution/win32/](http://www.ethereal.com/distribution/win32/) *Win32 二进制发行版*

正如上述网页指出的那样，您还需要 **Winpcap** 数据包捕获库，可从生产 **WIndump**（**tcpdump** 的 Windows 版本）的同一群人处获取：

- [http://winpcap.polito.it/](http://winpcap.polito.it/) *WinPCAP：Windows 的免费数据包捕获架构*

除了下载和文档外，该网站还有一个有用的常见问题解答（FAQ）：

- [http://winpcap.polito.it/misc/faq.htm](http://winpcap.polito.it/misc/faq.htm)

### ethereal 的字段名称和显示过滤器

如模块 13.4 所述，**ethereal** 在显示过滤器中使用自己特有的语法和字段名称，它们与捕获过滤器不同。通常，显示过滤器表达式由字段、逻辑（比较）运算符和值组成。字段由协议名称指定，通常还包括该协议内某个字段的名称。一个典型的例子是：

```
tcp.dstport ne 6000
```

表 A16.1 和 A16.2 展示了我们最常使用的协议和字段名称。

