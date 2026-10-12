

当你安装 `ipop3d` 时，`/etc/cram-md5.pwd` 数据库并未被创建。你需要使用你喜欢的编辑器创建该文件并添加一些条目，类似于

```
# CRAM-M5 authentication database
# Entries are in form <user><tab><password>
# Lines starting with "#" are comments

fredubble
wilma flintstone
barney barret
betty wired
```

显然，在任何文件中存储明文密码都是不好的做法——这是 `ipop3d` 软件的一个缺点。希望将来能在 APOP 数据库中加入加密功能。但在当前，你必须继续确保该文件具有正确的权限。此外，不建议用户使用与登录服务器相同的密码（即指定在 `/etc/passwd` 中的密码）来访问 APOP 电子邮件。

# IMAP

正如本章开头所述，POP 是让非 UNIX 操作系统用户读取基于 UNIX 的电子邮件的一个良好起点。但随着时间推移和分布式计算的真正兴起，其缺点变得显而易见。POP 服务器不会保留消息的已读或未读状态。消息会被下载到用户的 PC 并从服务器上删除，因此当用户更换 PC 时，他不得不在两台不同的机器之间迁移其邮箱。在这个远程通信日益普及的时代，人们发现，如果有许多消息需要下载，通过调制解调器从家访问电子邮件可能非常缓慢，而且他们无法从家中访问在工作 PC 上创建的电子邮件文件夹。

IMAP 协议现在允许人们将所有文件夹存储*在线*。这使得你能够在旅行、在家或工作时通过笔记本电脑访问电子邮件，而无需在本地和服务器之间来回传输消息。其工作原理是传输你正在阅读的文件夹的所有消息头。然后，使用你的 IMAP 客户端软件，你可以选择一条消息，它会显示在你的屏幕上。当然，主要优势在于消息保留在服务器上，因此你可以在任何地方访问它们。

与 POP3 协议类似，IMAP（通常也称为 IMAP4）也是一项 RFC 标准，因此它是一个透明协议，可以添加到任何消息系统中。IMAP 实现不仅适用于 UNIX 系统，还适用于 Microsoft Exchange、Novell Groupwise 以及无数其他系统。

## 配置 IMAP 服务器

在你的 Red Hat Linux 系统上配置 IMAP 服务器相对简单。你需要确保 imapid RPM 已安装：

```
[root@gonzo /] # rpm -q imap
imap-4.7c2-3
```

如果你得到类似的输出，说明你可以继续操作。否则，你需要安装 imap，它位于你的 Red Hat Linux CD-ROM 中。

你还需要检查 `/etc/xinetd.d/imap` 文件中的 imapd 是否未被禁用。它应包含以下内容：

```
service imap
{
	disable			= no
	socket_type		= stream
	wait			= no
	user			= root
	server		= /usr/sbin/imapd
	log_on_success	+= DURATION USERID
	log_on_failure	+= USERID
}
```

如果你需要更改它，则让 xinetd 重新加载其配置文件，你可以这样操作：

```
[root@gonzo /] # /etc/init.d/xinetd reload
```

此时，imapd 正在运行，你应该能够连接到它。这类似于你在上一节中测试与 POP 服务器连接的方式。

输入以下内容：

```
telnet imapsrver imap
```

imapsrver 是运行 imapd 程序的计算机名称。你应该会得到类似的响应：

+   - OK imapsrver IMap4rev1 v11.241 server ready

这意味着 IMAP 服务器已响应并等待指令（通常由客户端邮件阅读器完成）。如果你想测试认证服务，可以尝试以你自己登录，看看服务是否识别你的当前邮箱。例如，要以 sshah 身份登录，密码为 mars1031，输入

```
A001 user sshah mars1031
A001 OK LOGIN completed
```

你现在已登录到 IMAP 服务器。既然你只是在进行测试，现在可以通过输入以下内容注销：

```
A002 logout
* BYE imapserver IMAP4rev1 server terminating connection
```

你的 IMAP 服务器现已设置好，可以使用了！

## 邮件获取

在服务器上设置好 `imapd` 后，你可以使用多种方法访问你的邮件。你可以使用 Linux 控制台上的命令行程序，如 Pine，使用兼容 IMAP 的基于 Windows 或 Macintosh 的电子邮件客户端（其列表可在 `http://www.imap.org/products.html` 找到），或者使用 Netscape Communicator，它随 Red Hat Linux 发行版提供。

### 配置 Netscape 用于 POP3 或 IMAP 获取

设置 Netscape 与你的邮件服务器通信非常简单。你只需告知它你的 IMAP 或 POP 服务器名称、你的登录名，以及如果你要使用 IMAP，服务器上你的主目录中存放文件夹的子目录。

首先登录你的账户并创建一个名为 `Mail` 的目录：`[fred@gonzol]$ mkdir Mail`

你将使用此目录存储你的邮件文件夹，以便本地电子邮件客户端和远程 IMAP 客户端都能访问它们。

现在启动 Netscape。只需输入 `netscape` 即可启动。如果你收到 `not found` 错误，你需要安装 Microsoft 或 Red Hat CD-ROM。

点击 Communicator 菜单并选择 Messenger Mailbox。这将打开 Netscape 消息系统。现在点击 Edit、Preferences，然后点击屏幕左半部分的 Identity。你会看到一个如图 10.3 所示的对话框。

输入你的真实姓名。这个名称将用于你发出的电子邮件消息的 From: 头中。此外，填写你的正确电子邮件地址。这是人们将在 From: 头中看到的地址。

点击 Mail Servers，你会看到一个类似于图 10.4 的窗口。

**图 10.3**
使用 Netscape Messenger 设置你的身份

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_351_0.png)

**图 10.4**
使用 Netscape Messenger 设置你的邮件服务器详细信息

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_351_1.png)

在第一个文本框中，输入你在邮件服务器上使用的用户名。现在你需要输入你的出站（SMTP）服务器名称。删除给定的传入邮件服务器，然后点击 Add。这将弹出一个类似于图 10.5 的屏幕。输入传入服务器名称（这两个通常是相同的）。在你刚输入的信息下方，你可以选择传入邮件服务器类型。出于演示目的，选择 IMAP——但如果你不想要或不需要所有 IMAP 的便捷功能，同样可以轻松选择 POP3。使用顶部的标签页，你可以设置该协议支持的功能，例如选择将已删除的消息移动到 Messenger 回收站、如果 IMAP 服务器支持则选择 SSL 加密，或者选择为新文件夹设置离线下载。这允许你下载消息，使它们物理上驻留在本地 PC 以及服务器上，以便离线阅读。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_352_0.png)

如果你使用的是 IMAP，还有一个最终选项需要在开始使用 Messenger 阅读电子邮件之前设置。点击 Advanced Options 标签页，并在 IMAP 服务器目录中输入你在此节开始时创建的目录（Mail）。这是 Messenger 将用于你离线邮件文件夹的目录。点击 OK，再次点击 OK，然后点击 Get Msg 按钮。Messenger 会请求你的密码，然后开始下载所有你的电子邮件消息头并显示它们以便轻松浏览。然后，你可以使用工具栏正下方的下拉框轻松切换到不同的文件夹。

## fetchmail

`fetchmail` 最好通过示例来描述。假设你的邮件存储在你的 ISP 处。要通过传统方式访问你的邮件，例如使用 Netscape Messenger，你需要将其设置为 POP3 访问。这样，当你拨号接入时，它会将所有消息下载到你个人的 Linux 账户中，以便你可以随意阅读、回复和整理消息。

`fetchmail` 的模式略有不同。`fetchmail` 作为一个独立的程序执行，其唯一目的是登录你的 POP3 或 IMAP 服务器并下载所有消息，而不是使用你的邮件阅读器下载邮件。但这不仅仅是它能做的！在下载邮件时，每条消息都会传递给你的常规邮件传递代理（MDA）。如果你使用 `sendmail`、`qmail`、`smail` 或其他兼容 SMTP 的邮件服务器，所有消息都会传递到你本地 Linux 机器的 25 端口，就好像你

