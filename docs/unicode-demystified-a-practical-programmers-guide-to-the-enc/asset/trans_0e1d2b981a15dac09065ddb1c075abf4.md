

![](img/aa8214d49e1cf50152c432845129fb3b_138_0.png)

# 图 3-17 Pine 主菜单

活动屏幕（主菜单）以及关于程序的某些额外信息。屏幕底部的两行列出了为主菜单定义的所有命令，包括通用的 pine 命令。在这两行中，每条命令都由一个高亮显示的单个字符表示，显示在命令名称的左侧。

你可以通过两种方式执行 pine 命令。你可以按下与要执行的命令左侧字符对应的按键。对于出现在屏幕中间的通用命令，你可以使用 ARROW 键（或 N 表示下一个，P 表示上一个）将光标移动到你想要的命令上，然后按 RETURN（回车键）执行该命令。

由于主菜单有许多命令无法适应屏幕底部的显示区域，因此 O（其他）命令提供了一种查看额外条目的方法。输入 O 可以查看另一个两行显示。这两个两行显示包含了主菜单激活的完整命令集；O 命令还会带你回到原始的两行显示。

主菜单的基本格式贯穿整个 pine 屏幕：顶部有一行状态行，屏幕底部有两个行显示。如有必要，可以使用 O 命令查看额外的命令，并在路径上的关键点提供帮助文本。在大多数屏幕中，M 命令将你带回主菜单，Q 则关闭（退出）pine。

要了解更多关于 pine 的信息，可以通过输入问号（？）来显示主菜单的帮助屏幕。帮助屏幕显示关于 pine 的通用信息以及主菜单中可用命令的描述。正如所有

# 第 3 章

# GNU/Linux 工具介绍

pine 屏幕一样，帮助屏幕底部的两行显示会告诉你哪些命令是激活的。

从主菜单查看帮助文本的另一种方法是高亮显示通用 pine 命令 Help，使用 N 和 P 或方向键，然后按 RETURN。使用 RETURN 选择高亮（Select-highlighted）项是大多数 pine 屏幕中都可用的快捷方式；随着你变得熟练使用 pine，你会发现它非常有用。

当开始运行 pine 时，通用 pine 命令 Folder List 被高亮。输入命令 N 或按下 DOWN ARROW 键会高亮下一个通用 pine 命令，输入 P 或按下 UP ARROW 键会高亮上一个。

要返回 shell 提示符，输入 Q。系统会询问你是否确认退出 pine，此时输入 Y 将导致 pine 退出并返回到 shell。

# 发送邮件

要学习 pine，可以给自己发封邮件。请使用以下示例作为指南，将 alex 替换为你的登录名。

为了发送给给自己，Alex 输入 pine 调出主菜单。然后他选择通用 pine 命令 Compose Message（撰写消息）并按 RETURN（他也可以输入 C）进入消息编写器。当前屏幕的行 Compose Message 显示在图 3-18 的顶部。以 To: 提示符开头的行被高亮。邮件头部由 To: 提示符和接下来的三行组成。

![](img/aa8214d49e1cf50152c432845129fb3b_139_0.png)

图 3-18 pine Compose Message 屏幕

屏幕底部的显示显示所有命令都需要使用 CONTROL 键；例如，Get Help 命令是 CONTROL-G。使用 CONTROL 键执行命令是为了将命令与你填充表头字段和邮件正文时输入的文本区分开来。pine 中还有其他几个地方命令是控制字符，例如在编辑地址录时（参见主帮助屏幕）。

Alex 正在给自己发送邮件，他在 To: 提示符后输入了自己的登录名，然后按了 RETURN：

To: alex

Alex 一一按下 RETURN，pine 就会将他的登录名替换为全名和电子邮件地址，并包裹在角括号内：

To: Alex Watson <alex@example>

Alex 的电子邮件地址允许他人向他发送邮件。Alex 可以通过用户的登录名向系统上的任何用户发送邮件，但发送到其他系统上的用户需要更复杂的地址。如果在 To: 提示符高亮时按 CONTROL-G，pine 会为你提供地址方面的帮助。

你可以使用头部的下一行即 Cc: 行向其他用户发送消息副本。作为响应，你可以输入接收消息副本的用户名称。用逗号分隔列表中的名称，并按 RETURN 或 DOWN ARROW 键结束列表。因为 Alex 只想给自己发邮件，所以他按 RETURN 高亮头部的下一行。

第三行显示了 Attachmnt:（附件）提示符。作为响应，你可以提供想要附加到邮件消息中的文件或多个文件（文本或二进制文件）。Alex 按 RETURN 跳过了这一行。

头部的最后一行包含 Subject: 提示符。Alex 输入邮件消息的主题并按 RETURN：

Subject: Test Message

在输入主题后，Alex 输入了一段短消息，每行都以 RETURN 结尾：

This is a test message that I am sending myself.
Iam using Pine to write it and will use Pine to read it.

当他写完消息后，Alex 按 CONTROL-X 发送它。对于许多 pine 命令，Alex 都会被提示确认他的意图。输入 y 表示是（或直接按 RETURN——yes 已经被高亮），pine 就会发送他的消息。Alex 可能会留在那里，由于许多 pine 命令，Alex 会被提示确认他的意图。在主菜单中，他可能会为了删除 pine。

# 第 3 章 GNU/Linux 工具介绍

![](img/aa8214d49e1cf50152c432845129fb3b_141_0.png)

图 3-19 pine Index 屏幕

由于为了删除，Alex 退出 pine。要回到 shell 提示符，输入 Q。系统会询问你是否确认退出 pine，此时输入 Y 将导致 pine 退出并返回到 shell。

# 发送邮件

要学习 pine，可以给自己发封邮件。请使用以下示例作为指南，将 alex 替换为你的登录名。

为了发送给自己，Alex 输入 pine 调出主菜单。然后他选择通用 pine 命令 Compose Message（撰写消息）并按 RETURN（他也可以输入 C）进入消息编写器。当前屏幕的行 Compose Message 显示在图 3-18 的顶部。以 To: 提示符开头的行被高亮。邮件头部由 To: 提示符和接下来的三行组成。

![](img/aa8214d49e1cf50152c432845129fb3b_142_0.png)

图 3-20 Alex 给自己的消息

# 接收接收邮件

屏幕底部的显示显示所有命令都需要使用 CONTROL 键；例如，Get Help 命令是 CONTROL-G。使用 CONTROL 键执行命令是为了将命令与你填充表头字段和邮件正文时输入的文本区分开来。pine 中还有其他几个地方命令是控制字符，例如在编辑地址录时（参见主帮助屏幕）。

Alex 正在给自己发送邮件，他在 To: 提示符后输入了自己的登录名，然后按了 RETURN：

To: alex

Alex 一一按下 RETURN，pine 就会将他的登录名替换为全名和电子邮件地址，并包裹在角括号内：

To: Alex Watson <alex@example>

Alex 的电子邮件地址允许他人向他发送邮件。Alex 可以通过用户的登录名向系统上的任何用户发送邮件，但发送到其他系统上的用户需要更复杂的地址。如果在 To: 提示符高亮时按 CONTROL-G，pine 会为你提供地址方面的帮助。

你可以使用头部的下一行即 Cc: 行向其他用户发送消息副本。作为响应，你可以输入接收消息副本的用户名称。用逗号分隔列表中的名称，并按 RETURN 或 DOWN ARROW 键结束列表。因为 Alex 只想给自己发邮件，所以他按 RETURN 高亮头部的下一行。

第三行显示了 Attachmnt:（附件）提示符。作为响应，你可以提供想要附加到邮件消息中的文件或多个文件（文本或二进制文件）。Alex 按 RETURN 跳过了这一行。

头部的最后一行包含 Subject: 提示符。Alex 输入邮件消息的主题并按 RETURN：

Subject: Test Message

在输入主题后，Alex 输入了一段短消息，每行都以 RETURN 结尾：

This is a test message that I am sending myself.
Iam using Pine to write it and will use Pine to read it.

当他写完消息后，Alex 按 CONTROL-X 发送它。对于许多 pine 命令，Alex 都会被提示确认他的意图。输入 y 表示是（或直接按 RETURN——yes 已经被高亮），pine 就会发送他的消息。Alex 可能会留在那里，由于许多 pine 命令，Alex 会被提示确认他的意图。在主菜单中，他可能会为了删除 pine。

