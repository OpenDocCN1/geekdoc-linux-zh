
+OK Supported authentication mechanisms:

LOGIN

AUTH LOGIN

+VXN1ciCBYW11AA==

xxxxxxxxxx

```
# POP3 协议

第6 章

153

```
19 + UGFzc3dvcmQA

20 xxxxxxxx

21 -ERR Bad authentication

22 USER matthew

23 +OK User name accepted, password apple

24 PASS apple

25 +OK Mailbox open, 0 messages

26 QUIT

27 +OK Sayonara

28 Connection closed by foreign host

29 [matthew@shadrach matt]$

```

第 11 行显示客户端尝试与 POP3 服务器协商某些标准的 IMAP 身份验证技术，所有这些都失败了。第 12 行显示客户端发送了一个不带参数的 `AUTH` 命令。服务器在第 14 行和 15 行列出它支持的身份验证方法。第 16 行显示客户端尝试使用服务器支持的 `LOGIN` 方法。第 17 行显示服务器对 `AUTH` 命令的加密响应。不幸的是，客户端无法使用 `LOGIN` 身份验证方法登录，不得不在第 22 行到 25 行使用 `USER/PASS` 组合。

## POP3 客户端命令

当 POP3 客户端成功登录服务器后，它会进入事务模式。它必须发出命令来控制消息从服务器到客户端的传输。每个命令都会向服务器请求一个特定的 POP3 动作。

### STAT

`STAT` 命令没有参数。它用于从 POP3 服务器获取“投递列表”（drop listing）。投递列表是一行格式化的文本，用于指示邮箱箱的当前状态。该行的格式如下：

```
+OK nn mm
```

`STAT` 响应的格式允许邮件客户端解析响应以获取信息。`nn` 值代表用户邮箱箱中的消息总数。被标记为删除的消息不计入此值，但已读的消息会计入在内。`mm` 值代表由该计数所代表的消息的总字节数。`STAT` 命令通常用于邮件客户端快速检查邮箱箱的状态。通过登录并发出 `STAT` 命令，邮件程序可以将消息计数数字与上一次检查邮件时获得的值进行比较。如果数字不同，邮件程序就可以继续获取消息。这种方法的唯一问题是，客户端并不知道之前下载了多少条未删除的消息。

### LIST

`LIST` 命令用于获取邮箱箱的扫描列表。扫描列表是邮箱箱内容的简要摘要，包括消息编号及其以字节为的大小。不带参数发出的 `LIST` 命令将显示邮箱箱中所有消息的扫描列表。通过将消息编号作为参数，`LIST` 命令将显示该特定消息的扫描列表。列表 6.6 显示了一个示例 `LIST` 命令会话。

#### 列表 6.6 LIST 命令示例

```
1 [alex@shadrach alex]$ telnet localhost 110
2 Trying 27.0.0.1...
3 Connected to localhost.
4 Escape character is '^'.
5 +OK POP3 v6.50 server ready
6 USER alex
7 +OK User name accepted, password
8 PASS tarzan
9 +OK Mailbox open, 2 messages
10 LIST
11 +OK Mailbox scan listing follows
12 1 355
13 2 465
14 -
15 LIST 1
16 +OK 1 355
17 LIST 2
18 +OK 2 465
19 LIST 3
20 -ERR No such message
21 QUIT
22 +OK Sayonara
23 Connection closed by foreign host.
24 [alex@shadrach alex]$
```

第 10 行显示客户端向服务器发送了不带参数的 `LIST` 命令。服务器在第 12 行到 14 行响应，在第 11 行给出确认，然后在第 12 行和 13 行给出消息扫描列表。在某些 POP3 服务器实现中，确认响应将包含 `STAT` 输出以总结消息，但客户端软件不能依赖这一点（如此列表所示）。
第 15 行和 17 行显示客户端针对单个消息发出 `LIST` 命令，服务器的响应显示在第 16 行和 18 行。第 19 行显示客户端对不存在的消息编号发出 `LIST` 命令。服务器在第 20 行返回否定响应。

### RETR

`RETR` 命令用于从邮箱箱中检索单个消息的文本。此命令使用的参数是前述 `LIST` 命令返回的消息编号。如果消息编号有效，服务器将返回一个确认行以及消息的完整文本，随后跟一个终止字符（单独占一行的句号）。发送给客户端的消息应该是服务器邮箱箱中包含的完整 RFC 822 格式消息，并由主机软件（通常是 SMTP）返回。POP3 服务器不会以任何方式对消息进行格式化或处理。POP3 服务器的任务是将消息完整传输给客户端。列表 6.7 显示了一个示例 `RETR` 会话。

#### 列表 6.7 RETR 命令示例

```
[rich@shadrachich]$ telnet localhost 110
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^'.
+OK POP3 localhost v6.50 server ready
USER rich
+OK User name accepted, password please
PASS guitar
+OK Mailbox open, 2 messages
LIST
+OK Mailbox scan listing follows
355
2 465
RETR 1
+OK 1 355 octets
Return-Path: <rich@shadrachich>
Date: Thu, 2 Sep 1999 10:15:25-0500
From: rich@shadrachich
Subject: Message 1
Status: 0
This is 
```

## 邮件服务简介

### DELE

`DELE` 命令标记消息待删除。在会话终止之前，不会实际删除消息。此命令使用的参数是要删除的消息的编号。如果消息编号有效，服务器将返回确认。随后该消息被标记为删除，且不会包含在后续的 `LIST` 响应中。

### NOOP

`NOOP` 命令正如其名——什么都不做。接收到 `NOOP` 后服务器将返回确认响应。此命令可用于确定 POP3 服务器的连接性。它可能仅在登录服务器建立会话后发出。

### RSET

`RSET` 命令将在客户端与服务器身份验证后将会话重置为开始状态（客户端无需重新登录）。重要的

了解 `RSET` 命令的关键在于，它将导致服务器取消任何已标记为删除的消息。取消标记的消息将带有其原始消息编号返回到扫描列表中。

### QUIT

`QUIT` 命令用于终止 POP3 会话。当服务器接收到 `QUIT` 命令时，它实际上会删除用户邮箱中任何已标记为删除的消息，并终止 TCP 会话。如果 POP3 会话应该终止，客户端使用 `QUIT` 命令，此时任何标记为删除的消息都将恢复而不会被删除。

### TOP

`TOP` 命令是一个可选的 POP3 命令，服务器可能会选择实现。`TOP` 命令是客户端获取邮箱中可用消息的简要摘要的方便方法。它将返回消息的 RFC 822 头部字段，以及消息正文中指定行数的的内容。`TOP` 命令有两个参数，且都是必须的。`TOP` 命令的格式为：

```
TOP n n
```

其中 m 是来自 `LIST` 扫描的邮件编号，n 是表示将显示的消息正文行数的整数。邮件客户端经常使用此命令来获取消息的主题（Subject）头部字段，以便在消息列表中显示，而无需下载消息的全文。列表 6.9 显示了 `TOP` 命令使用的示例。

#### 列表 6.9 TOP 命令示例

```
1 [rich@shadrach]$ telnet localhost 110.
2 Trying 127.0.0.1...
3 Connected to localhost.
4 Escape character is '^'.
5 +OK POP3 localhost v7.59 server ready
6 USER name
7 +OK User name accepted, password please
8 PASS guitar
9 +OK Mailbox open, 5 messages
10 LIST
11 +OK Mailbox scan listing follows
12 1 387
13 2 396
14 3 374
15 4 375
16 5 383
17 
```
