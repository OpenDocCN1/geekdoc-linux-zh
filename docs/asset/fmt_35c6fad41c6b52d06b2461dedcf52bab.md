
除了 `POP` 之外最重要的替代方案是 `IMAP`。该缩写代表互联网消息访问协议。与 `POP` 的本质区别是消息保留在互联网提供商的服务器上。因此，`IMAP` 并不是为离线操作设计的。然而，该协议对于从不同位置/计算机/操作系统访问邮件的人来说具有优势，因为所有消息都是集中式管理的（而不会出现在各种计算机、分区等地方）。在书中，不再进一步考虑 `IMAP`。

![](img/b30873dd3d753687a59253fb9ad26a0b_371_0.png)

## 基础

### 发送消息

最后，关于你发送的消息的几句话。它们发送后的位置也取决于配置。在独立系统中，消息通常存储在名为 `outbox` 的文件夹中，直到它们被转发到互联网提供商。随后，它们会进入 `sent-mail`（或类似）文件夹，以便你始终知道发送了什么。

当邮件程序作为客户端工作时，情况会有所不同。在这种情况下，程序在写入 `sendmail` 后立即转发消息。例如，由于（目前）没有互联网连接，它会被临时存储在目录 `/var/spool/queue`。在此目录下，每条消息都以一个加密密码名称存储在单独的文件。通常，你不应修改该目录中的任何内容——`sendmail` 本身会处理存储在这里的文件。可以使用 `mailq` 显示队列邮件列表。

### 术语，工作技术

为了更好地理解下一节中邮件程序的描述，以下段落解释了一些术语和工作技术，这些内容在所有邮件程序中都是相似的。如果你已经有一些邮件经验，可以跳过本节。

### 邮件头

- `From: address` 发送者的电子邮箱地址
- `To: address` 收件人的电子邮箱地址
- `Subject: contents` 内容简要描述（一行）
- `Reply-To: address` 不要回复给 `From`；而是回复到此地址
- `Cc: address` 消息的副本会发送到 `Cc` 地址
- `Bcc: address` 与 `Cc` 相同，但不同之处在于，主收件人不会被通知消息也发送给了另一个人（密抄）

### 文件夹

如果你收到多封邮件消息，消息的组织非常重要。大多数邮件程序都允许你创建文件夹。你可以根据主题、日期或任何你认为有用的标准来组织消息。你可以将消息从一个文件夹移动到另一个文件夹，或者在不再需要时将其删除。某些邮件程序还允许你在特定文件夹内搜索消息。在管理大量邮件时，这是一个非常实用的功能。

### 签名 (Signature)

在互联网社区中，在电子邮件和新闻文章末尾附几行文本是一种礼貌行为，这些文本除了公司名称、地址等数据外，还可能包含个人陈述（如“我喜欢 Linux”）。为了避免你重复输入这些文本，大多数电子邮件程序会自动在消息末尾插入 `~/.signature` 文件的内容。

### 二进制文件 (Binary files)

电子邮件通常只包含 `ASCII` 文本，这对任何电子邮件程序都不会产生问题。此外，所有现代电子邮件程序都支持邮件标准 `MIME`。该缩写代表多用途互联网邮件扩展（Multipurpose Internet Mail Extensions）。`MIME` 可用于方便传输二进制文件。在某些电子邮件程序中，当收件人的程序支持 `MIME` 时，你可以直接查看图像和 `HTML` 文件。

当编码后的文件直接作为文本显示时，就会出现问题。这看起来类似于下面的列表：

```
---137161636-894403337-790290599:#100
Content-Type: TEXT/PLAIN; CHARSET=US-ASCII; NAME="picture.ps"
Content-Transfer-Encoding: BASE64
Content-ID: .3.89.9501170859.B100hofer.muenchen
Content-Description: Image
I0Z2JRYAyJLENCgWIDENCgNCAWIDLEgTGECAwMDAg4cMDAMCAIdDAMDAIDEAyLIAyAYQgMTY41DE20CA20ASNASCA2MDAQgMgMQDoxIdQgMCAXOx
MCAwUljAwMDAwIDMgTTAID3MSNCAMjkq2psa2psamramxbgtGqGtq
---137161636-894403337-790290599:#100--
[EO3B]
```

### uuencode 和 uudecode

`uuencode` 和 `uudecode` 命令是 `MIME` 标准建立之前的遗留。它们用于将二进制文件转换为 `ASCII` 格式，或从 `ASCII` 文件重建二进制文件。通过这种方式，可以使用石器时代的电子邮件程序发送二进制文件。在极少数你收到或发送邮件的情况下，以下是这两个命令的语法：

```
user$ uuencode file name > uufile
user$ uudecode uufile
```

`uuencode` 编码文件并将结果存储在 `uufile` 中。`name` 指定要存储在编码文件中的文件名。通常指定相同的文件名；`uudecode` 可以在不需要额外信息的情况下恢复文件名。

## Netscape Messenger

`Netscape` 的 `Netscape` 组件允许你读写电子邮件和新闻。从 `Netscape` 主窗口开始，你可以通过 `COMMUNICATOR MESSENGER` 或 `MAIL|` 启动 `Messenger`。

在使用 `Messenger` 之前，你需要在 `EDIT|PREFERENCES|MAIL|IDENTITY` 对话框表格中输入你的全名和电子邮件地址。某些进一步规格是可选的，例如签名的文件名或回复地址。（只有当你不希望缺件人向你的发送者地址以外的地址发送回复时，才需要此项。）

![](img/b30873dd3d753687a59253fb9ad26a0b_375_0.png)

### 使用 Netscape 阅读邮件

#### 作为独立系统的配置

如果你想在没有 `sendmail` 或 `fetchmail3` 等额外程序的情况下使用邮件功能，在 `MAIL SERVERS` 对话框上需要以下设置：

`INCOMING MAIL SERVERS`：在这里你指定你的互联网提供商 `POP` 服务器的互联网地址（示例用户页 305 使用 `pop.provider.de`）。作为 `USER`，你必须指定 `POP` 账户的登录名。这可能与你的电子邮件地址相同（即为 `hofer`）。当你第一次建立连接时，系统会提示输入密码。如果你希望 `Netscape` 立即记住此密码，必须激活相应的选项。（加密密码存储在 `~/.netscape/preferences.js` 中。）

`CHECK FOR MAIL EVERY ... MINUTES` 选项应该禁用——它在离线操作下没有意义。最后，你可以指定你的邮件是否保留在你的互联网提供商的服务器上。此设置对于初次非常有用（否则，邮件可能会在配置混乱中丢失），但绝对需要禁用它，否则来自提供商的邮件列表将不断增长直到填满所有可用存储空间。

在 `OUTGOING MAIL SERVER` 下，你输入用于发送所有邮件的提供商服务器名称（示例用户 `hofer` 使用 `mail.provider.de`）。

如果你不指定不同的目录，所有邮件文件夹（包括收件箱）通常存储在 `~/nsmail/` 目录下。

![](img/b30873dd3d753687a59253fb9ad26a0b_376_0.png)

图 10.2 作为独立系统的配置。

#### 作为 sendmail/fetchmail 客户端配置

如果 `Netscape` 仅用于读取本地邮件（`sendmail` 和 `fetchmail`）并处理消息转发（见第 359 页），某些配置细节看起来略有不同：

作为 `INCOMING MAIL SERVER`，你现在使用随 `Netscape` 提供的 `movemail` 程序。使用 `USER`，你需要指定邮件存储在 `/var/spool/mail` 下的名称（通常规则上是你的本地登录名）。你应该激活 `CHECK FOR EVERY MINUTE` 选项——每分钟检查一次本地文件的内容并不费精力。

在读取邮件消息时，`Netscape` 在 `/var/spool/mail` 中创建一个锁文件。然而，只有当程序被允许在该目录下写入数据时才有效。因此，可能需要扩展 `/var/spool/mail` 的权限：

```
root chmod +w /var/spool/mail
```

这种方法的缺点是，任何用户现在都可以任意存储文件。唯一的替代方案是使用具有 `SETUID` 权限的外部邮件程序从该目录读取消息。
