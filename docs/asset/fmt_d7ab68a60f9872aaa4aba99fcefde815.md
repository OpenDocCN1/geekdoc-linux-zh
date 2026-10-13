
### 新的 Mail 处理工具：`nmh`

Mail Handler 客户端（通常称为 `nmh`）在管理邮件方面与大多数其他邮件客户端不同。`nmh` 由一组你在 shell 中执行的命令组成，就像你执行任何 Unix 命令一样。它没有像 Mail 那种特殊的邮件 shell。一个 `nmh` 命令发送消息，另一个命令显示你的入站消息，还有一个命令保存消息。`nmh` 命令及其选项列于表 17-4 所示。一组环境变量为你执行的 `nmh` 命令提供了上下文环境，例如跟踪当前消息或邮件文件夹。

### 表 17-4：`nmh` 命令

| 命令 | 描述 |
|---|---|
| `inc` | 将收到的邮件存放在你的收件箱中并显示消息头信息 |
| `show num` | 显示当前消息或指定的消息 |
| `prev` | 显示上一条消息 |
| `next` | 显示下一条消息 |
| `scan` | 重新显示消息头信息 |
| `Mhl` | 显示消息的格式化列表 |
| `folders` | 列出所有邮件文件夹 |
| `forw` | 转发消息 |
| `repl` | 回复消息 |
| `send` | 重新发送消息或将文件作为消息发送 |
| `pick` | 按指定标准选择消息并为其分配序列 |
| `folder` | 切换到另一个邮箱箱文件（文件夹） |

注意：与其使用命令界面操作，不如使用 `xmh` 或 `exmh`，它们提供了一个用于访问 `nmh` 消息的 X Windows 界面。

要使用 `nmh` 发送消息，你首先需要使用 `comp` 命令撰写消息，然后使用 `send` 命令发送消息。要编写消息，在命令行上单独输入 `word` 命令并按回车。此时，你将进入 `nmh` 默认编辑器（通常是 Vi）的输入模式。屏幕顶部会提示输入地址、抄送（cc）和主题。在虚线下方，你输入你的消息。你可以使用方向键在不同位置之间移动。一旦你输入了消息内容，像往常一样保存并退出编辑器。在 `What now?` 提示处，你可以发送消息、编辑它、将其保存到文件，或在不发送消息的情况下退出。`send` 命令发送消息。在 `What now?` 提示处按回车键会显示你可以输入的命令列表。在下一个示例中，用户为地址为 robert 的另一个用户撰写了消息。

```
$ comp

To: robert

cc:

Subject: Birthday

-----------------

Your present is in the mail

really.

What now? send

$ 
```

要用 `nmh` 读取邮件，你首先需要使用 `inc` 命令将新收到的邮件存入指定的 `nmh` 邮箱箱文件。`inc` 命令会显示你收件箱中每条邮件消息的头信息列表。一个 `nmh` 头信息包含 06/07 Christopher Peter trip<<Are you ready for the trip? chris >>
2 06/07 Aleina Petersen party<<its on for tomorrow night. Aleina >>
3 06/07 Dylan Petersen newsletter<<Did you write your article yet? Dyla >>

```
$ inc

1+ 06/07 Christopher Peter trip<<Are you ready for the trip? chris >>

2 06/07 Aleina Petersen party<<its on for tomorrow night. Aleina >>

3 06/07 Dylan Petersen newsletter<<Did you write your article yet? Dyla >>
```

如果你想重新绘制头信息，需要使用另一个名为 `scan` 的 `nmh` 命令。

```
$ scan

1+ 06/07 Christopher Peter trip<<Are you ready for the trip? chris >>

2 06/07 Aleina Petersen party<<its on for Aleina >>

3 06/07 Dylan Petersen newsletter<<Did you Dylan >>
```

你使用 `show`、`next` 和 `prev` 命令来显示消息。`show` 命令显示当前消息，`next` 命令显示当前消息之后的消息，而 `prev` 命令显示当前消息之前的消息。初始状态，当前消息是新收到的消息中的第一条。如果你想显示特定的消息，可以使用带有消息编号的 `show` 命令。`show 2` 显示消息 2。你也可以通过列出消息编号来引用多条消息。`show 1` 显示消息 1 和 3。你还可以通过指定第一个数字和最后一个数字（用连号隔开）来指定消息范围。`show 1-3` 显示消息 1、2 和 3。

```
$ show

$ next
```

要打印消息，你首先用 `show` 输出它，并将其输出通过传输到打印机。你以同样的方式将消息保存到文本文件中。你先用 `show` 输出消息，然后将输出重定向到文件。

```
$ show | lpr

$ show > myfile
```

使用 `repl` 命令回复当前消息。你需要知道消息编号或消息主题才能进行回复。使用 `rmm` 删除当前消息。要删除特定消息，你使用编号配合 `rmm`。你可以使用 `folder` 命令创建自己的邮箱箱。邮箱箱通常被称为文件夹。要创建一个新文件夹，输入 `folder` 命令后跟名称。

```
$ repl

$ rmm

$ folder +mailbox
```

### 接收到的邮件的通知

当邮件消息被接收时，它们会自动存放在邮箱箱中，但你不会收到自动通知。要检查是否有任何等待的消息，你可以使用 `mail monitor` 获取消息，或者使用 `mail monitor` 告知你是否有邮件。Gnome 也有可用的邮件监控程序（mail monitors）。在 KDE 桌面内部，你可以从两个组件中选择：Mail Check 和 Mail Notify。Mail Check 组件将显示一个小信封和收到的消息数量。两者在左侧显示 Mail Check，右侧显示 Mail Notify。其他组件如 Sonicmail 会通知你任何 POP3 邮件警报。Biff 执行与 Korn 类似的邮件监控。Maillet 将监控邮箱箱，并为每个邮箱箱分配优先级。

KDE 桌面有一个名为 Korn 的邮件监控工具，其工作方式相同。当没有邮件时，Korn 显示一个空的收件箱，当邮件到达时，显示一个带有信件的托盘。如果邮件仍在邮箱箱中，则会显示信件。你可以按照需要设置这些图标。你还可以指定使用的邮件客户端以及检查新邮件的间隔。如果你有多个账户，为每个账户设置一个配置。每个账户会显示不同的图标，告诉你邮件何时到达。

如果你正在使用窗口管理器（如 fwm 或 Enlightenment），可以使用 `xbill` 工具执行相同的功能。`xbill` 在你的桌面上显示一个带有标记的邮箱箱图标。当邮件到达时，该标记会升起。如果你喜欢，`xbill` 还可以发出响声。对于命令行界面，你可以使用 biff 工具。Biff 在消息接收时会通知你。这在你期待某条消息并想及时知道时非常有用。Biff 在消息接收时会自动显示头信息和标题行。要关闭它，在命令行输入 `bf n`。要查看它是否开启，输入 `bf o`。

你可以通过 `msg n` 命令临时阻止通知，防止在屏幕上显示任何消息。`msg n` 仅停止新消息，它也会停止通知。稍后，你可以通过 `msg y` 解除阻止。

### 访问远程服务器上的邮件

大多数邮件客户端都配备了访问远程服务器邮件账户的功能。对于大多数邮件客户端，你可以指定一个自己的邮箱箱。例如，你可以安排将不同账户的邮件直接进入你 Linux 系统的收件箱。来自 ISP 邮件服务器的邮件将出现在你的本地收件箱中。这种功能对于使用 Elm 或 Base 等不支持访问 ISP 邮件服务器的邮件客户端的用户非常有用。你可以使用 Fetchmail 实现这种功能。Fetchmail 检查远程邮件服务器并将其下载到你的本地收件箱（如果它显示为新收到的邮件）。

要使用 Fetchmail，你必须知道远程服务器的 Internet 地址和邮件协议。大多数远程邮件服务器使用 POP3 协议，但其他可能使用 IMAP、ETRM 或 POP2 协议。在命令行中输入 fetchmail，并带有邮件服务器地址和任何所需的选项。邮件协议通过 `-p` 选项指定，邮件服务器类型通常为 POP3。如果你的电子邮件用户名与你的 Linux 登录名不同，请使用 `-u` 选项和电子邮件名称。一旦执行 fetchmail 命令，系统会提示你输入密码。POP3 邮件服务器的 fetchmail 命令语法如下：

```
fetchmail -p POP3 -u username mail-server
```
