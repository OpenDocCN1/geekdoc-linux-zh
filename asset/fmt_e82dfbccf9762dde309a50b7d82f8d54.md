
| No response from modem | The modem is not turned on. The modem is a Windows-only model. Attempting to use the wrong device file. Linux serial device driver is not loaded; use `cat /proc/interrupts` and check for a serial device interrupt. Bad modem cable, or cable plugged into wrong port. |
| Can dial, but get gibberish from ISP | This is normal when dialing an ISP that expects to make a PPP connection. |

## PPP Authentication

当你拨号 ISP 建立 PPP 连接时，ISP 希望知道你的身份以用于安全和记账目的。你（或你的拨号脚本）向 ISP 确认身份的过程称为身份验证，目前使用有几种不同的身份验证方法：

- **Manual login—**如果你拨号 ISP 并收到要求输入用户名和密码的提示，很可能你的 ISP 支持手动登录程序。这并不意味着手动登录是你的*唯一*选项。按今天的标准，手动登录明显过时了，很少有 ISP 要求手动登录。如果你的 ISP 需要，你可以创建登录脚本在适当时间提供适当信息，但鉴于需要此程序的系统很少，本书不介绍创建此类脚本。

- PAP—PAP 是目前使用最广泛的身份验证方法之一。在最近版本的 Linux 上，它要求你创建一个包含用户名和 ISP 密码的特殊文件。然后 PPP 拨号实用程序读取此文件并在被要求时发送适当的密码。

- CHAP—CHAP 在实践中与 PAP 非常相似，尽管其内部细节有所不同。与 PAP 一样，你创建一个包含用户名和密码的特殊文件，PPP 拨号器在 ISP 询问来电者是谁时使用该文件。

对于 PAP 和 CHAP，密码文件分别是 `/etc/ppp/pap-secrets` 和 `/etc/ppp/chap-secrets`。Red Hat Linux 在 `ppp` 包中包含这些文件的示例，如果你的系统上尚未安装，你应该安装它。Red Hat 示例 secrets 文件非常简略——它们不包含任何条目，只有注释。为了提供最佳安全性，这些文件的权限应设置为 `-rw-------`（八进制表示法为 `600`），意味着只有所有者（root）可以读取或写入该文件。每个文件都可以为不同的 ISP 或用户包含单独的身份验证，每行一个身份验证。两文件中每行的信息相同：

```
client  server  secret  IP address
```

每个字段的含义是：

- client—你在 ISP 系统上的用户名。

- server—你 ISP 服务器的名称。如果你不知道服务器的名称，就像你对大多数 ISP 来说可能不知道一样，你可以在此处使用星号（`*`）。

- secret—你的密码，该密码以明文形式存储在此文件中，这就是为什么该文件不应被 root 以外的任何人读取很重要。

- IP address—远程系统将分配给你的 IP 地址。在大多数情况下，你事先不知道这会是什么，因此你应将此字段留空。

#### Tip

> 如果你不知道你的 ISP 使用 PAP 还是 CHAP，你可以创建一个文件——比如 `pap-secrets`——并为另一个文件创建指向你创建的文件的链接。你的系统随后将对 PAP 和 CHAP 使用相同的 secrets 文件。

作为示例，这里是一个可供单个客户端上的三个人使用的 `pap-secrets`/`chap-secrets` 文件，用于连接到三个不同的 PPP 账户，这些账户可能在同一 ISP 或不同 ISP 上：

```
elmo  sesame  elmopw  192.168.1.101
bert  *       bertpw
ernie *       erniepw
```

在此配置中，`elmo` 的账户是最受限制的，因为它只允许登录到服务器机器 `sesame`，并且只接受 IP 地址 `192.168.1.101`。`bert` 和 `ernie` 账户都更灵活；它们会接受任何远程服务器和任何 IP 地址。

很可能你只需要一个单行的 `pap-secrets`/`chap-secrets` 文件，不包括注释（以井号 `[#]` 开头的行）。当系统建立了 PPP 链路后，任何用户都可以使用它。因此如果 Bert 连接到他的 ISP，Elmo 和 Ernie 就可以使用该链路。如果这些账户在不同的 ISP 上，当机器连接到一个外来 ISP 时，这些用户在访问某些 ISP 服务（如电子邮件或 Usenet 新闻）时可能会遇到困难。这是因为许多 ISP 会检查此类服务的传入请求的来源，如果请求来自另一个 ISP，则会拒绝此类请求。Web 浏览、Telnet、FTP 下载以及类似功能对所有用户都正常工作。

## 创建 PPP 脚本

Red Hat Linux 6.0 包含一些基本的 PPP 支持文件，包括 `pppd`，即用于启动 PPP 会话以及在你希望计算机作为拨入式 PPP 服务器时监听会话的 PPP 守护进程。然而，如果你想实际使用这些功能，你必须以某种方式将它们连接起来。一种方法是编写一个简短的脚本来完成工作。事实上，你需要三个脚本：两个用于启动 PPP 会话，一个用于终止它。因为如果你想配置拨号按需设置，如本章后面“设置拨号按需以实现自动连接”一节所述，你将使用脚本，所以我在此介绍更基础的脚本。你可能更喜欢使用更偏向 GUI 的方法，并且有几种 GUI PPP 拨号器可用，因此我在本章后面“使用 GUI PPP 拨号器”一节中介绍了使用方法。

#### NOTE

> 你可能需要为你的系统修改这些脚本。至少，你需要在 `ppp-on` 脚本中插入你自己的用户名和 ISP 电话号码。你可能还需要根据你的硬件或软件需求，或 ISP 的需求来更改其他脚本。关于调试 PPP 连接的一些信息，出现在本章后面“PPP 问题解决”一节中。

## 创建 ppp-on 脚本

首先，这里有一个基本的 `ppp-on` 脚本。你可以输入它，保存在 `/usr/local/bin` 或其他方便的位置，并赋予执行权限。随书光盘上也有此文件的版本，位于 `sams-extras/ppp` 目录中。言归正传，以下是该脚本：

## 创建 ppp-on-dialer 脚本

正如你创建了 `ppp-on` 脚本一样，你必须创建 `ppp-on-dialer` 脚本。它要么必须放在 `/etc/ppp` 目录中，要么你必须修改 `ppp-on` 脚本中对该脚本的引用。以下是 `ppp-on-dialer` 的示例（同样，你可以在随书光盘上找到此文件）：

```
#!/bin/sh
#
# This is part 2 of the ppp-on script. It will perform the
# connection protocol for the desired connection.
#
exec /usr/sbin/chat -v
TIMEOUT 3
ABORT '\nBUSY\r'
ABORT '\nNO ANSWER\r'
ABORT '\nRINGING\r\n\r\nRINGING\r'
'' 'AT'
'OK' 'ATZ'
TIMEOUT 40
'OK' ATDT$TELEPHONE
'CONNECT'
```

该脚本只是运行 `/usr/sbin/chat`，它是一个实用程序，用于根据某些字符串向串口传输数据。除了 `TIMEOUT` 和 `ABORT` 等关键字外，左列包含 expect 字符串，即程序期望从调制解调器看到的内容，右列包含 send 字符串，即程序作为响应发送的内容。这里需要对具体细节做一些说明：

- 大多数行末的反斜杠 (`\`) 字符是行 continuation 字符；许多 Linux 程序，包括 shell，都将其识别为将一行扩展到下一物理行的信号。它们在这里使用是因为 `chat` 希望其输入在一行上，但多行格式对人类来说更容易理解。

- 作为对 `OK` 的响应，`chat` 将发送 `ATZ`。这是调制解调器初始化代码，在此情况下将调制解调器重置为默认值。你可以将此字符串更改为你喜欢的任何其他内容——例如，降低调制解调器的音量或更改其拨号速度。请参阅调制解调器的文档了解详细信息，或从另一个程序复制你喜欢的初始化字符串。不过，不同的调制解调器使用不同的命令代码，因此不要从使用与你的调制解调器型号不同的调制解调器的系统复制字符串。

- `TIMEOUT` 值 `40` 对于大多数情况应该足够，但如果你的 ISP 接听电话需要很长时间，你可能需要增加 `TIMEOUT` 值。

## 配置 DNS

在你运行 `ppp-on` 脚本来启动 PPP 链接之前，还有一个细节需要处理：DNS。与第 7 章所述的以太网网络一样，你必须配置系统以了解你的 ISP 的 DNS 服务器。你可以通过编辑文件 `/etc/resolv.conf` 来实现。以下是该文件的一个示例：
