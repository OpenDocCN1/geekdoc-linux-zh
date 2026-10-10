
## ASCII、HTML、HTTP、GIF、JPEG、MPEG 和 MIME

似乎每一次技术进步都会引发新一轮缩语的涌现。以下是一些与互联网和万维网相关的重要缩语精选：

- **ASCII**（美国标准信息交换码）。计算机使用数字——具体来说是二进制数——来表示所有数据。一种标准的数值表示文本的方案是*美国标准信息交换码*（*American Standard Code for Information Interchange*），更通俗地称为 ASCII（发音为“ask-key”）。该代码将大写字母、小写字母、数字和常用标点符号表示为 7 位二进制数。尽管大多数用户实际上看不到 ASCII 表示，但你可能会听到有人谈论“ASCII 文件”。这只是指仅包含文本的文件——例如没有图形、视频或音频。
- **HTML**（超文本标记语言）。许多万维网文档都基于*超文本标记语言*（*Hypertext Markup Language*，HTML）。HTML 文档包含有关网页如何由 Web 浏览器解释和显示的指令。已经开发了各种版本的 HTML，包括 SHTML，即*安全超文本标记语言*（*Secure Hypertext Markup Language*），旨在为 Web 上的金融交易提供安全性。
- **HTTP**（超文本传输协议）。为了相互通信，Web 客户端和服务器遵循一组称为*超文本传输协议*（*Hypertext Transport Protocol*，HTTP）的规则。你自己不需要了解 HTTP 的任何细节——你的浏览器会处理这些细节——但你在通过 Web 请求文档时经常会使用这个缩语。
- **GIF**（图形交换格式）。图形——包括绘图、图表和照片——的存储和传输方式与文本不同。*图形交换格式*（*Graphic Interchange Format*，或称 GIF，发音为“jif”）由 CompuServe 在 20 世纪 80 年代开发，用于通过网络高效传输图像。GIF 采用文件压缩技术来最小化图形文件的大小。（不幸的是，GIF 压缩算法限制了图像中可使用的颜色数量。）GIF 文件通常通过*后缀*.gif* 来识别。
- **JPEG**。虽然 GIF 是 Web 上最广泛使用的图形格式，但它并非唯一。一个行业组织*联合图像专家组*（*Joint Photographic Experts Group*，JPEG）定义了一种针对彩色照片压缩优化的替代文件格式。JPEG 文件名通常带有*后缀*.jpeg* 或*.jpg*。
- **MPEG**。这种由*运动图像专家组*（*Motion Picture Experts Group*）定义的 MPEG 文件格式常用于传输压缩的视频和音频数据。MPEG 文件通过*后缀*.mpeg* 来识别。
- **MIME**。最初，UNIX 邮件程序仅限于文本（ASCII）消息。一些较新的邮件程序还可以处理 MIME（*多用途互联网邮件扩展*，*Multi-Purpose Internet Mail Extensions*），这是一种在电子邮件中包括多媒体对象的标准。

缩语 http 是“Hypertext Transport Protocol”（超文本传输协议）的简写，表明该信息页面包含超文本。以 ftp: 开头的 URL 指的是可以通过 ftp 访问的文档。同样，前缀 gopher: 表示可以通过 gopher 访问的文档。大多数 Web 浏览器都可以处理 http、ftp 和 gopher 文档。

双斜杠（//）位于网站（或主机计算机）的域名之前，在本例中该域名为 1cweb.loc.gov。

单个斜杠（/）标志着包含该文档的文件绝对路径名的开始。在本例中，路径名是 /homepage/1chp.html。这个路径名的解释与你之前看到的 UNIX 路径名完全相同。

## 13.11 练习

1. 请确保你能定义以下术语：
   - 网络
   - WAN（广域网）
   - 互连网
   - TCP/IP
   - 域
   - URL（统一资源定位符）
   - GIF（图形交换格式）
   - LAN（局域网）
   - 网关
   - Internet（互联网）
   - SLIP（串行线路互联网协议）
   - 电子邮件
   - ASCII（美国标准信息交换码）
   - JPEG
   - CAN（控制器局域网）
   - 骨干网
   - 数据包
   - PPP（点对点协议）
   - 浏览器
   - HTML（超文本标记语言）
   - MPEG
   - MAN（城域网）
   - 拓扑
   - 协议
   - IP 地址
   - 超文本
   - HTTP（超文本传输协议）
   - MIME

2. 你的计算机是否是局域网的一部分？如果是，有多少其他机器连接到同一个网络？它们位于哪里？

3. 你的系统是否可以访问互联网？如果可以，你的主机互联网地址是什么？它的域名是什么？

4. 你的电子邮件地址是什么？

## 14 教程：使用电子邮件

在本章中，你将看到如何使用标准的 UNIX 邮件程序 `Mail` 和 `mailx` 来发送和接收文本消息。

造成混淆的一个原因是，在某些系统上，`mail` 命令会调用 `Mail` 或 `mailx`；而在其他系统上，`mail` 命令会调用较旧的 UNIX 邮件程序。

### 14.1 发送电子邮件

如果你刚开始使用一个新的 UNIX 账户，不太可能有人已经给你发送过电子邮件。不过，你可以从给自己发送消息开始。

1. 输入 Mail 命令，后跟收件人的邮件地址。如果你使用的是 AT&T UNIX，请尝试 `mailx` 程序：

```
$ mailx address
```
在此处输入收件人的邮件地址。

如果你使用的是 BSD UNIX，请键入：
```
$ Mail address
```
在此处输入收件人的邮件地址。

计算机将提示你输入消息的主题：
```
Subject:
```

2. 指定主题。为你的消息输入简短的描述或标题：
```
Subject: Test Message #1
```

3. 输入消息正文。邮件程序的编辑功能有限：你每次只能编辑一行，并且无法返回去编辑之前的行。因此，在开始新行之前，请确保每一行都是正确的：

*别惊慌。*（*Return*）
*这只是一个测试。*（*Return*）

4. **当消息完成时，发送它。** 这是通过开始新行，然后按（*Control*-*D*）（表示“完成”）来实现的：

（*Return*）
（*Control*-*D*）

在某些系统上，计算机会询问你是否想给任何人发送副本（Cc）：

Cc: 

5. **发送副本（如果有）。** 输入应收到你消息副本的任何人的登录名。如果你不打算向任何人发送副本，只需按（*Return*）。

Cc: （*Return*）

UNIX 提示符告诉你已返回到 UNIX shell：
```
$
```

### 14.2 邮寄文件

由于邮件程序的编辑功能有限，使用 *vi* 编辑器创建一个包含你消息的文件，然后邮寄该文件通常更为方便。在本节中，你将看到如何使用电子邮件发送文件的副本。

1. **使用文本编辑器创建一个文件。**

2. **将文件重定向到电子邮件程序。** 要将文件 *poems* 发送到账户 *login*，请键入：

```
$ mailx login < poems (*Return*)
```
或者：
```
$ Mail login < poems (*Return*)
```
输入重定向箭头（*<*) 告诉邮件程序从文件 *poems* 的内容中获取输入。

> 警告 务必使用输入重定向箭头（*<*），而不是输出重定向箭头（*>*）。使用错误的箭头可能会破坏文件的内容。

### 14.3 在邮件程序中使用 vi

在发送邮件前编辑消息的一种方法是从邮件程序调用 vi 编辑器。然后你可以使用 vi 命令来编辑消息。

1. 启动邮件程序并输入收件人地址。为了练习，你可以指定自己为收件人：

```
$ mailx yourlogin (Return)
```
或者：
```
$ Mail yourlogin (Return)
```
你会被要求输入主题：

2. 指定主题。

```
Subject: Another Test Message (Return)
```

3. 输入你的消息。例如：

```
There once was a fellow named Lester,
Whose knowledge grew lesser and lesser.
It at last grew so small,
He knew nothing at all;
So they hired him as a professor.
```

4. 启动 vi 编辑器。开始新行，然后输入波浪号（~），接着输入 v（代表 vi），然后按 RETURN：

```
(Return)
~v (Return)
(Return)
```
这将调出 vi 编辑器并将你的消息放入缓冲区：

```
There once was a fellow named Lester,
Whose knowledge grew lesser and lesser.
It at last grew so small,
He knew nothing at all;
So they hired him as a professor.
~
~
~
/tmp/Re24223 6 lines, 163 characters
```

5. 使用 vi 命令编辑消息。如果你正在跟随示例操作，可以尝试将“Lester”更改为“Chester”。

