
如果“历史”插件项左侧没有显示标记，请勾选该复选框并点击确定以启用插件。（注：原文此处后续部分存在大量重复文本，翻译已根据要求去重处理）

# 桌面用户的 Ubuntu 和 Kubuntu

使用斜杠（`/`）字符前缀来与服务器本身交互。以下是常用的 IRC 命令：

- `/chat nickname`：请求与指定昵称的用户进行直接的、对用户的会话聊天。
- `/help`：总结可用的 IRC 服务器命令。你可以在 `/help` 命令后加上另一个命令的名称（不带 `/`）来获取有关该命令的特定信息。
- `/join #channel`：允许你连接到特定频道。如果指定的频道不存在，它通常会创建该频道并让你成为操作者，但某些 IRC 服务器会将频道创建限制为特定用户，以减少噪音（并防止由于输入错误自动创建频道）。
- `/leave`：离开指定的频道。
- `/list`：显示可用频道列表。
- `/quit`：断开与 IRC 的连接，并显示告别（`quit`）。
- `/who #channel`：列出当前连接到特定频道的用户。

虽然最初的客户端适用于 Windows 和类 Unix 系统，但在 IRC 出生后不久，其他操作系统也出现了 IRC 客户端。Mac OS、Mac OSX 和 Microsoft Windows 提供了丰富的 IRC 客户端选择。`mIRC` (www.mirc.com/) 可能是最流行的 IRC 客户端，还有许多其他选择。Windows 版 Miranda 客户端也支持 IRC，Tilera (www.tileratudios.com) 也是如此。Macintosh 用户通常使用 IRC II (miranda.com)，它在 Macintosh 系统上已经存在很久；Adium X (www.adium.com)，它同时提供 IM 和 IRC 访问；以及 Colloquy (http://colloquy.info)，它在 OS X 桌面和 iPhone 上都令人印象深刻。

接下来的部分讨论如何使用 Pidgin 和 Kopete 消息客户端连接到 IRC——它们被称为多协议客户端并非没有理由。第三部分提供了获取更多 IRC 信息的提示。

## 在 Pidgin 中使用 IRC

正如“在 Ubuntu 上使用 Pidgin 进行即时消息”中所讨论的，IRC 是 Pidgin 内置的消息协议之一。大多数 IRC 服务器都是开放的，你可以创建一个 IRC 账户并连接到 IRC 服务器而无需重新注册，但你必须创建一个 Pidgin 账户来实现此操作。你可以像创建其他账户一样创建 Pidgin IRC 账户，选择账户管理（Accounts manage）选项并选择 IRC 协议，如图 13 所示。

你的名称就是你的昵称，你可以随心所欲地命名，但在你连接的 IRC 服务器上必须是唯一的。默认情况下，Pidgin IRC 账户会将你连接到 IRC 服务器 `irc.ubuntu.com`（Freeode IRC 网络的一部分），但如果你出于某些原因连接到另一个 IRC 服务器，可以更改服务器名称。

一旦你有了 Pidgin IRC 账户，你将看到标准的伙伴列表（Buddy List）对话框。

图 13-3 显示了连接到 `irc.ubuntu.com` 服务器后看到的窗口。

### 发送和接收即时消息

#### 图 13-32

在 Pidgin 中创建 IRC 账户

![](img/e3248f698da647444405a34229bd9df5_562_0.png)

#### 图 13-33

到 IRC 服务器的初始连接

![](img/e3248f698da647444405a34229bd9df5_562_1.png)

连接到 IRC 服务器后，你可能可以使用 `/list` 命令查看可用频道，或者使用 `/join` 命令加入特定频道。加入频道会打开一个用于在该频道通信的新标签页，并在后台打开 ChanServ（频道服务器）标签页，该标签页显示已向管理 ChanServ 服务注册的频道的注册、管理和通用信息消息。图 13-34 显示了在 Pidgin 聊天窗口底部文本窗口输入 `/join #ubuntu` 后连接到 `#ubuntu` 频道的界面。

# 桌面用户的 Ubuntu 和 Kubuntu

#### 图 13–34

加入 `#ubuntu`

![](img/e3248f698da647444405a34229bd9df5_563_0.png)

此时，你可以在 `pidgin` 屏幕底部的文本窗口中输入 IRC 命令，或者直接输入文本发送到频道。当你提问、回答或简单地切换通信流时，可以使用 `/leave` 命令离开频道，或使用 `/quit` 关闭你与 IRC 服务器的连接。

> 如果你觉得 IRC 有趣、有用，或者两者兼有，也许你可能想研究其他的 Linux 客户端。虽然 Pidgin 对于我的需求足够了，但 Xchat 程序是一个存在已久的 UNIX/Linux IRC 客户端，非常受欢迎，并且可以方便地同时连接到多个频道和服务器。Xchat 使用 GTK，如果你愿意安装其 GTK 依赖项，它非常适合基于 GNOME 的桌面或 Kubuntu 系统。Xchat 默认不安装，但在 Ubuntu 仓库可用。Xchat 的最新版本位于 `xchat-nome` 软件包中，你必须使用 Synaptic（或 Kubuntu 系统上的 apt-install）、`apt` 或 `opt-` 来安装它。

## 在 Kopete 中使用 IRC

正如“在 Kubuntu 上使用 Kopete 进行即时消息”章节中所讨论的，IRC 是 Kopete 内置的消息协议之一。大多数 IRC 服务器都是开放的，你可以创建一个 IRC 账户并连接到 IRC 服务器而无需重新注册，但你必须创建一个 Pidgin 账户来实现此操作。你可以像创建其他账户一样创建 Kopete IRC 账户，选择账户管理（Accounts manage）选项并选择 IRC 协议，如图 13 所示。

你的名称就是你的昵称，你可以随心所欲地命名，但在你连接的 IRC 服务器上必须是唯一的。默认情况下，Pidgin IRC 账户会将你连接到 IRC 服务器 `irc.ubuntu.com`（Freeode IRC 网络的一部分），但如果你出于某些原因连接到另一个 IRC 服务器，可以更改服务器名称。

一旦你有了 Pidgin IRC 账户，你将看到标准的伙伴列表（Buddy List）对话框。

图 13-3 显示了连接到 `irc.ubuntu.com` 服务器后看到的窗口。

### 发送和接收即时消息

#### 图 13-32

在 Pidgin 中创建 IRC 账户

![](img/e3248f698da647444405a34229bd9df5_562_0.png)

#### 图 13-33

到 IRC 服务器的初始连接

![](img/e3248f698da647444405a34229bd9df5_562_1.png)

连接到 IRC 服务器后，你可能可以使用 `/list` 命令查看可用频道，或者使用 `/join` 命令加入特定频道。加入频道会打开一个用于在该频道通信的新标签页，并在后台打开 ChanServ（频道服务器）标签页，该标签页显示已向管理 ChanServ 服务注册的频道的注册、管理和通用信息消息。图 13-34 显示了在 Pidgin 聊天窗口底部文本窗口输入 `/join #ubuntu` 后连接到 `#ubuntu` 频道的界面。

# 桌面用户的 Ubuntu 和 Kubuntu

#### 图 13–34

加入 `#ubuntu`

![](img/e3248f698da647444405a34229bd9df5_563_0.png)

此时，你可以在 `pidgin` 屏幕底部的文本窗口中输入 IRC 命令，或者直接输入文本发送到频道。当你提问、回答或简单地切换通信流时，可以使用 `/leave` 命令离开频道，或使用 `/quit` 关闭你与 IRC 服务器的连接。

> 如果你觉得 IRC 有趣、有用，或者两者兼有，也许你可能想研究其他的 Linux 客户端。虽然 Pidgin 对于我的需求足够了，但 Xchat 程序是一个存在已久的 UNIX/Linux IRC 客户端，非常受欢迎，并且可以方便地同时连接到多个频道和服务器。Xchat 使用 GTK，如果你愿意安装其 GTK 依赖项，它非常适合基于 GNOME 的桌面或 Kubuntu 系统。Xchat 默认不安装，但在 Ubuntu 仓库可用。Xchat 的最新版本位于 `xchat-nome` 软件包中，你必须使用 Synaptic（或 Kubuntu 系统上的 apt-install）、`apt` 或 `opt-` 来安装。（注：由于原文中存在大量重复段落，此处已根据“不要重复输出原文”的原则进行精简翻译，保留核心内容）

## 发送和接收即时消息

## 获取更多 IRC 信息
