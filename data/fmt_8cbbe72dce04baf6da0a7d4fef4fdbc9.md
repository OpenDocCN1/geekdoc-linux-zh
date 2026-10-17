
| 输入，显示为字符 | C | a | t |

|---|---|---|---|

| 输入，十进制等价 | 67 | 97 | 116 |

| 输入，转换为二进制 | 01000011 | 01100001 | 01110100 |

| 分成 6 位块 | 010000 | 110110 | 000101 | 110100 |

| 转换为十进制 | 16 | 54 | 5 | 52 |

| 来自表格的 base64 输出 | Q | 2 | F | 0 |

这是另一个例子，长度不是三个字符的倍数，因此末尾需要进行填充：

输入： **Cats**

输出： **Q2F0cw==**

前四个输出字符的生成方式与上述完全相同，因为前三个输入字符是相同的。输出的其余部分生成如下：

| 输入，显示为字符 | s | | |

|---|---|---|---|

| 输入，十进制等价 | 115 | | |

| 输入，转换为二进制 | 01110011 | | |

| 用 0 位填充至 6 位块的倍数 | 01110011 | 0000 | | |

| 分成 6 位块 | 011100 | 10000 | | |

| 转换为十进制值 | 28 | 48 | *填充* | *填充* |

| 来自表格的 base64 输出 | c | w | = | = |

Base64 输出比原始数据大约 33%，这是当你使用完整的 8 位字符来表示输入的 6 位时预期的结果。

### 备注和延伸阅读

- RFC-1113 **1989年8月** *互联网电子邮件隐私增强*。这是 RFC 中关于 Base-64 编码的第一次描述，尽管它没有被这样称呼；它被称为“可打印编码”。

Base64 本身描述在：

- RFC-1521 **1993年9月** *MIME (多用途互联网邮件扩展) 第一部分*

- RFC-2045 **1996年11月**, *互联网消息主体*

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

在图 A15.1 中，我们使用 `telnet` 连接到服务器 Bob 上的 IMAP 知名端口。与 POP 和 SMTP 示例一样，为了清晰起见，我们将服务器的响应进行了缩进，并截断了一些行以节省空间。

与 POP 和 SMTP 的一个区别是，当您输入 IMAP 命令时，必须为其添加一个 *标签*（tag）前缀——用作标签的文本字符串。（您可以使用任意字符串，只要每个字符串在此会话中是唯一的即可。）当 IMAP 服务器对命令做出响应时，它会使用该命令的标签作为输出的前缀，以表明输出所关联的内容。这是必要的，因为 IMAP 客户端/服务器的交互是异步的，即对命令的响应不一定按照输入命令的顺序输出，并且您可以在早期命令完成之前输入另一个命令。之所以这样做是因为某些 IMAP 命令（例如大型搜索）可能需要很长时间，服务器可能不会立即响应，但*会*允许您输入进一步的命令。输出多行的命令在所有输出行上（最后一行除外）都显示星号（“*”）作为标签，最后一行则像往常一样显示输入标签，如果命令成功则接着显示 `OK`，如果失败则显示 `BAD`。

以下是图 A15.1 中会话的逐行解释：

- a1 **以用户 bex15 登录并提供密码。**（a1 是我们决定使用的第一个唯一标签。）服务器回复说登录成功，并使用我们输入的相同标签作为响应的前缀 – a1

- a2 **`SELECT`** 指定我们要使用的邮箱，在此情况下为 `/htiw/imap/mbox`。服务器回复该邮箱包含三条消息，并给出了其他详细信息

- a3 **`SEARCH`** 在此邮箱中搜索 `SUBJECT` 头包含单词“elephants”且 `FROM` 头包含“snit”的消息。我们可以通过附加条件来指定更多标准，例如 `SUBJECT` “elephants” `TO` “fred@aw.com” `NOT FROM` “bex8@uit.co.uk” 服务器回复匹配消息的编号 – 在本例中为编号 2 和 3

- a4 **`FETCH`** 消息 2 和 3，并列出我们指定的头部

- a5 **告诉我消息 1 的 MIME 结构。**（我们编辑了输出以更清晰地显示结构。通常人类不会看到此输出，因此其视觉格式并不重要。）

  - 此消息是一个 `multipart/mixed`，包含一个文本附件和一个 GIF 文件附件
