
## Armitage

如果你不喜欢直接执行命令，可以使用 Armitage，它是 Metasploit 的图形界面（GUI）版本。Armitage 设计为一种允许在使用 Metasploit 的同时进行攻击管理的工具。它的设计也是为了让后渗透（post-exploitation）变得简单一些。使用 Armitage 时，你会发现客户端攻击变得容易了一些但你也可以使用社交工程工具（Social Engineering toolkit），它比 Armitage 更好。

Armitage 预装在 BackTrack 5 或更高版本中。对于旧版本，你需要在 shell 中执行命令 `apt-get install Armitage` 来安装该工具。要启动它，在 shell 中使用命令 `Armitage`，工具就会启动。只需点击 `connect` 按钮，工具就会开始。我们已经介绍了 Armitage 大大部分扫描操作。

关于 Armitage 有很多细节需要学习。你可以在 Metasploit 控制台中执行的每一个命令在 Armitage 中都可以使用。你可以在此处了解更多关于该工具的信息：

`http://www.fastandeasyhacking.com/manual`

## 第8章

## 攻击客户端的技巧

在第七章中，我们查看了攻击服务器的不同技术。然而，服务器每天都在变得越来越强大。在客户端隐藏在 NAT、路由器或防火墙之后且无法直接访问的情况下，你将需要依赖客户端攻击。俗说，“人非圣圣”——意味着你的受害者会犯错，从而让你获得访问其系统的权限。

为了让客户端攻击生效，你需要收集受害者的个人信息，包括他们的喜好、厌恶、朋友、工作地、宠物名称以及任何可能帮助你发起攻击的个人细节。社交媒体是寻找所有这些细节的绝佳场所。

### 客户端攻击攻击场景

你可以使用许多方法来攻击受害者。

### 带有恶意附件的邮件

在这里，你以 PDF、mp3 或 exe 的形式将恶意文件发送给受害者。如果受害者打开、下载并执行这些文件，你将获得一个 `meterpreter` 会话（session），这将让你获得访问受害者系统的权限。

### 邮件中的恶意链接

在这种方法中，你向受害者发送一个链接，希望他们会点击该链接。链接可以将受害者重定向到虚假的登录页面或带有恶意代码的服务器。当你托管 Web 服务器时，代码将在受害者的浏览器上执行，这将为你提供一个 `meterpreter` 会话，通过你可以控制受害者的系统。

### 劫持更新

在这种情况下，你需要确保受害者在每次更新软件时都会下载恶意代码。我们将在下面详细介绍这一点。

### 物理安装在受害者机器上的恶意软件

如果你对目标机器有物理访问权限，可以在机器上插入 U 盘。这个 U 盘可能包含恶意文件或可执行代码。当你插入 U 盘时，该代码或文件会立即执行，并在目标机器上打开一个 `meterpreter`。

要执行上述四种攻击，你可以使用社交工程工具（SET）。

### 带有恶意附件的邮件攻击

在这里，你需要创建一个自定义的可执行文件或 PDF 来攻击受害者。创建一个自定义的可执行文件并没有挑战性——最让大多数道德黑客面临挑战的，如何说服目标执行 `.exe` 文件。你可以创建自己的可执行文件，但可能会被受害者的防病毒软件检测，或者你可以从 `hack-forums.net` 等论坛购买加密器（crypter）并创建一个不可检测的可执行文件。如果你选择自己创建，你需要让它绕过受害者使用的防病毒软件。

### 使用 SET 创建后门

当你需要在利用 Metasploit 功能的同时执行客户端攻击时，SET 非常有用。要使用 set 创建后门，请按照以下步骤操作：

在 BackTrack 上打开 `/pentest/exploits/set` 目录并执行以下命令：

```
cd /pentest/exploits/set
./set
```

社交工程工具是 TrustedSec 的产品。

访问：`https://www.trustedsec.com`

- 从菜单中选择：
  1) 社交工程攻击 (Social-Engineering Attacks)
  2) 快速渗透测试 (Fast-Track Penetration Testing)
  3) 第三方模块 (Third Party Modules)
  4) 更新 Metasploit Framework (Update the Metasploit Framework)
  5) 更新社交工程工具 (Update the Social-Engineer Toolkit)
  6) SET 配置 (SET configuration)
  7) 帮助、感谢和关于 (Help, Credits, and About)
  99) 退出社交工程工具 (Exit the Social-Engineer Toolkit)

按 `1` 选择第一个选项，然后你需要选择第四个选项 `创建负载和监听器（Create a payload and a listener）`。在使用之前确保你已更新 SET。

工具会要求你输入反向 IP，你需要输入它。在互联网上进行攻击时需要在路由器上进行端口转发。

选择一个符合你要求的适当负载。你可以选择看到的第一个选项 `Windows Shell Reverse_TCP` 来使其简单。然后你将被要求选择编码，你可以选择 `shikata_ga`。虽然 SET 推荐使用 `backdoored`，但你需要对其进行多次编码以绕过防病毒软件。

下一步是你选择所需的端口，你可以选择任何你喜欢的端口。此过程需要时间，Metasploit 将启动。你将看到如下：在根目录 `/pentest/exploits/set` 下有一个名为 `msf` 的文件。之后，将创建并存储 `.exe` 文件到 `/pentest/exploits/set`。

### 使用 PDF 进行黑客

如果你通过 Wordpad 等文本编辑器打开 PDF 文件，你会发现它有四个部分：头部（header）、正文（body）、交叉引用表（cross-reference table）和尾部（trailer）。头部显示 PDF 版本，正文携带所有对象，交叉引用表指定对象的位置，尾部（始终从 `%EOF` 开始）是读取开始的地方。

### PDF 启动动作

PDF 启动动作是 PDF 的重要功能。通过此功能，你可以启动其他程序。在 Adobe Reader 更新停止启动恶意代码之前，黑客会随 PDF 传播恶意软件和机器人网络。受害者会收到像下面这样的邮件：

| 发件人：Royal Mail |
| 日期：2010年4月15日 星期四下午1:32 |
| 收件人： |
| 主题：重要：Royal Mail 递送 #109217 |
| 附件：Royal_Mail_Delivery_Invoice_109217.pdf (111 KB) |

我们在递送时错过了您。请查看发票并就任何问题与我们联系。我们将在下一个工作日再次递送。Royal Mail。

下载 PDF 后，尝试打开它会弹出一个对话框，点击 `打开`，Ze 就会安装。你可以创建一个带有启动动作的 PDF 来攻击你的受害者。要这样做，你需要一个空的 PDF 文件或内容极少的文件。你还需要 Adobe reader 9.3.2 版本，可以从 `oldapps.com` 下载。用 Wordpad 或记事本打开你的 PDF 文件。在你的编辑器中，文件如下所示：`img/d52d8402f5bef7b14bcbab9bcc53820f_277_0.png`

滚动到名称对象部分，如下所示：

```
5 0 obj
<</Length 500
stream
BT/Y 10 Tf 350 750 Td 20 20 L 1 Tr (blank.pdf) Tj ET
BT/Y 15 Tf 233 690 Td 0 Tr 0.0 0.58823294117647 0.0 rg (This is a PDF!) Tj ET
endstream
```

将部分 `<<length 500` 替换为：

```
/Type/Action
/S/Launch
/Win <<
/F (calc.exe)
)
```

```
108 0 obj
<<
/Type /Action
/S /Launch
/win
/F (calc.exe)
>>
endobj
```
