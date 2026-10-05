

## Content-Type 头部

Content-Type 头部标识消息所携带的数据类型。该标头的通用格式为：

标头的 `type` 字段定义了数据类型，`subtype` 字段定义了特定的数据类型。例如 `application/msword`，它将消息定义为 Microsoft Word 的应用程序数据。可选的 `attribute=value` 对用于某些数据类型，以提供关于消息中承载数据的附加信息。例如 `text/plain; charset=us-ascii`，它表示消息是使用美国 ASCII 字符组成的纯文本。RFC 2046（“多用途互联网邮件扩展 (MIME) 第二部分：媒体类型”）定义了若干媒体类型：

- text 基础数据类型。与 text 类型相匹配的子类型示例包括 `plain`、`enriched` 和 `html`。
- image。图像数据的常见子类型有 `jpeg`、`gif` 和 `tiff`。
- audio 数据。RFC 2616 中描述的子类型是 `basic`，它是脉冲编码调制 (PCM) 数据的名称。
- video 动态图形图像。video 的子类型示例有 `mpeg` 和 `quicktime`。
- application 二进制数据或必须由特定程序处理的数据。子类型包括 `octet-stream`（八位二进制数据）和 `msword`（需由特定文字处理器处理的数据）。
- multipart 由多个独立部分组成的消息，每个部分都可以包含自己的类型的数据。RFC 为此定义了四种子类型：
    - mixed，其中每个部分都是完全独立的。
    - alternative，其中每个部分以不同格式包含相同的数据。
    - parallel，其中每个部分应该同时查看。
    - digest，其中消息的每个部分都是一个封装的消息。
- message 这是一个封装的邮件消息，反反可以是任何有效的消息类型。

除了这七种数据类型外，RFC 2046 还提到了几个子类型。但这仅仅是冰山一角。实际上有成百种数据子类型。供应商根据 RFC 2048（“多用途互联网邮件 (MIME) 第四部分：注册程序”）中的指令注册其数据的子类型。已注册的大量数据子类型表明想要通过电子邮件传输的应用程序数量巨大。要查看注册数据类型的最新列表，请从 ftp.isi.edu 的 `in-notes/iana/assignments` 目录下载 `file-types` 文件。

由于 MIME 为邮件消息增加了结构，头部不再局限于消息的开头。Content-Type 头部可以在消息中出现多次。列表 1.4 显示了来自 Caldera Linux 系统的邮件，它使用 MIME 在消息内部封装了消息。

## 列表 1.4 带有 MIME 部的消息

```
Received: from localhost (localhost)
by ani.foobirds.org (8.9/8.9.3) with internal id IAB1301;
Sat, 29 Jul 2000 08:13:52 -0400
Date: Sat, 29 Jul 2000 08:13:52 -0400
From: Mail Delivery' <MAILER-DAEMON@ani.foobirds.org>
Message-ID: <e00007291213.IAB1301@ani.foobirds.org>
To: craig@ani.foobirds.org
MIME-Version: 1.0
Content-Type: multipart/report; report-type=delivery-status;
binary="IAB1301.96478232/ani.foobirds.org"
Subject: Returned user unknown
Auto-Submitted: auto-generated (failure)
Status:

This is a MIME-encapsulated message

--IAB1301.96478232/ani.foobirds.org

The original message was received at Sat, 29 Jul 2000 08:13:12 -0400
from@localhost

----- The following addresses had permanent errors -----
frank@wren

----- Transcript of session -----
.... while talking to wren.foobirds.org:
>>> RCPT To:<frank@wren.foobirds.org>
<<< 550 <frank@wren.foobirds.org>... Relaying denied
550 frank@wren... User unknown

--IAB01301.96487232/ani.foobirds.org
Content-Type: message/delivery-status

Reporting-MTA: dns; ani.foobirds.org
Arrival-Date: Sat, 29 Jul 2000 08:13:12 -0400

Final-Recipient: RFC2222; frank@wren.foobirds.org
Action: failed
Status: 5.1.1
Remote-MTA: DNS; SMTP: 550 <frank@wren.foobirds.org>... Relaying denied
Last-Attempt-Date: Sat, 29 Jul 2000 08:13:52 -0400

--IAB01301.96487232/ani.foobirds.org
Content-Type: message/rfc822

Return-Path: <root@localhost>
Received: from localhost (localhost)
by ani.foobirds.org (8.9/8.9.3) with internal id IAB1301;
Sat, 29 Jul 2000 08:13:52 -0400
Date: Sat, 29 Jul 2000 08:13:52 -0400
From: Mail Delivery' <MAILER-DAEMON@ani.foobirds.org>
Message-ID: <e00007291213.IAB1301@ani.foobirds.org>
To: craig@ani.foobirds.org
MIME-Version: 1.0
Content-Type: multipart/report; report-type=delivery-status;
binary="IAB1301.96478232/ani.foobirds.org"
Subject: Returned user unknown
Auto-Submitted: auto-generated (failure)
Status:

This is a MIME-encapsulated message

--IAB1301.96478232/ani.foobirds.org

The original message was received at Sat, 29 Jul 2000 08:13:12 -0400
from@localhost

----- The following addresses had permanent errors -----
frank@wren

----- Transcript of session -----
.... while talking to wren.foobirds.org:
>>> RCPT To:<frank@wren.foobirds.org>
<<< 550 <frank@wren.foobirds.org>... Relaying denied
550 frank@wren... User unknown

--IAB01301.96487232/ani.foobirds.org
Content-Type: message/delivery-status

Reporting-MTA: dns; ani.foobirds.org
Arrival-Date: Sat, 29 Jul 2000 08:13:12 -0400

Final-Recipient: RFC2222; frank@wren.foobirds.org
Action: failed
Status: 5.1.1
Remote-MTA: DNS; SMTP: 550 <frank@wren.foobirds.org>... Relaying denied
Last-Attempt-Date: Sat, 29 Jul 2000 08:13:52 -0400

--IAB01301.96487232/ani.foobirds.org
Content-Type: message/rfc822

