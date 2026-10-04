
# 大部分内容为 Linux 命令 `chat` 构建一组参数，用于与另一个系统进行对话

首先，这是该脚本：

```sh
#!/bin/sh
#
TELEPHONE=phoneNumber # 连接用的电话号码
LOGIN=login # 用于 ISP 的登录标识符
PASSWORD=password # 在 ISP 上登录账户的密码

DIALSCRIPT=/tmp/dialscript.$$

trap rm -f $[DIALSCRIPT] exit INT HUP QUIT
umask 066
cat <<EOF $DIALSCRIPT
TIMEOUT 3
ABORT="\nBUSY\r"
ABORT="\nNO CARRIER\r"
ABORT="\nNO ANSWER\r"
'' '\nAT\r"
OK ATD$TELEPHONE
TIMEOUT 0
login:\r\d\d\r'
login: $LOGIN
password: $PASSWORD
EOF
/usr/sbin/chat -v f $[DIALSCRIPT]
```

我们现在逐行讨论这些代码。

- `TELEPHONE=phoneNumber` – 设置要拨打的电话号码。phonumber 是你 ISP 调制解调器的号码。

- `LOGIN=login` – 设置用于登录你 ISP 系统的标识符。login 是你的 ISP 分配给你的登录标识符。使用 CHAP 或 PAP 协议时不需要此设置，所以如果你已经确认可以使用其中一种协议进行身份验证，请不要设置它。

- `PASSWORD=password` – 设置登录你 ISP 系统的密码。password 是你的 ISP 分配给你的密码。使用 CHAP 或 PAP 协议时不需要此设置，所以如果你已经确认可以使用其中一种协议进行身份验证，请不要设置它。

## 第二部分：安装网络

- `DIALSCRIPT=/tmp/dialscript.$$` 此脚本写入拨号脚本，即 `chat` 执行以拨打你的调制解调器并登录到 ISP 机器的脚本。我们生成一个拨号脚本而不是将选项作为命令行参数传递，出于安全考虑：如果我们将这些参数作为命令行参数传递给 `chat`，那么这些参数（包括你的登录标识符和密码）对任何可以使用 `ps` 命令的用户可见。shell 会将后缀 `$$` 替换为执行该脚本的 Linux 内核进程进程号。例如，如果 Linux 内核以进程 757 执行此脚本，则拨号脚本将写入文件 `/tmp/dialscript.757`。

- `trap -f $[DIALSCRIPT] exit INT HUP QUIT` - 在这里，我们使用 `trap` 命令来捕获 INT（中断）、HUP（挂断）和 QUIT（退出）信号。如果执行此脚本的进程接收到这三个信号中的任何一个（表示进程正在终止），就会调用两个命令：rm（删除拨号脚本文件）以及 exit（退出脚本）。这确保了在脚本结束或中止时，包含登录和密码信息的拨号脚本会被删除。

- `umask 066` - 该命令为由此脚本创建的任何文件设置默认权限。在这种情况下，权限 066 移除了文件所有者的读、写、执行权限。这是一项安全措施，有助于确保此脚本编写的拨号脚本只有有理由的用户才能读取。

- `cat <<EOF $DIALSCRIPT>` - 此命令向环境变量 `DIALSCRIPT` 定义的文件写入脚本中的后续所有行，直到包含 `EOF` 标记的行。EOF 是 shell 术语中所谓的“在此文档”（here document）的示例。`chat` 命令将按照脚本在此处出现的顺序执行这些行。

- `TIMEOUT 3` - 此指令告诉 `chat`，如果你的调制解调器在三秒内无法拨号并连接 ISP 的调制解调器，则退出。这防止了在调制解调器不可（例如有人拔掉了插头）时 `chat` 挂起。如果你的调制解调器与 ISP 调制解调器连接需要超过三秒，你可能希望延长几秒钟——例如，ISP 的调制解调器接听之前电话必须响几次，或者调制解调器在连接时必须经过漫长的协商序列（调制解调器首次连接时听到的哨声和尖叫声）。

- `ABORT "\nBUSY\r"` - 此指令及后续两个指令指示返回无法连接 ISP 机器的调制解调器。转义序列 `\r` 表示回车符；转义序列 `\n` 表示换行符。大多数现代调制解调器在 ISP 调制解调器的电话线繁忙时返回 BUSY。

- `ABORT "\nNO CARRIER\r"` - 大多数现代调制解调器在与 ISP 调制解调器连接但未接收载波信号时返回此字符串。这会发生在，例如，你不小心拨通了语音电话并有人接听了。

- `ABORT "\nNO ANSWER\r"` - 大多数现代调制解调器在无人接听时返回此字符串——即电话响了预设次数（通常为十次）未被接听。

- `OK ATD$TELEPHONE` - 此行继续与调制解调器对话。在对话的一部分，调制解调器发送字符串 OK（作为对上一行发送的 AT 指令的响应）。作为响应，脚本发送字符串 ATDT（调制解调器的标准指令“注意，拨号音”），随后是根据变量 `PHONE` 设置的电话号码。当执行此指令时，你的调制解调器将拨打 ISP 的调制解调器并建立连接。

- `TIMEOUT 30` - 此时，`chat` 已经拨通 ISP 的调制解调器并建立了连接（如果你无法连接，要么会超时，要么你的调制解调器会返回其中一个 ABORT 字符串）。此时，我们将超时时间从 3 改为 30。这为脚本留了时间与调制解调器执行对话并登录。注意，如果你可以使用 CHAP 或 PAP，则不需要脚本的剩余部分。

- `\r\d\d\r` - 此行继续对话，但此时对话的对象是 ISP 机器而不是你的调制解调器。在这里，ISP 显示以字符串 OK 结尾的文本（横幅）。作为对 ISP 的响应，脚本发送三个回车符（由 `\r` 序列表示），间隔两个延迟（由 `\d` 表示）。实际上，脚本点击三次回车键以获取 ISP 的横幅并进入登录提示。请注意，此指令取决于特定的 ISP 机器：你的 ISP 可能不使用横幅，或者使用一个结尾不是 OK 的横幅。这部分对话你需要根据 ISP 如何配置系统自行填写。脚本的这部分需要你进行一些尝试。在本章的后部分，我们将遍历 `chat` 返回的消息，以便你完全遵循 ISP 发送的精确提示。

- `login:$LOGIN` - 此行继续与 ISP 系统对话。脚本等待以字符串 `login:` 结尾的提示。字符串 `login:-` 有特殊含义：

  - 在预设时间内等待以 `login:` 结尾的字符串。
  - 如果字符串没有到达，`chat` 将发送中断信号（稍微扰动 ISP 系统），然后再次等待以 `login:` 结尾的字符串。
  - 如果字符串随后在预设时间内仍未出现，`chat` 退出。
  - 然而，如果 `chat` 确实收到了以 `login:` 结尾的字符串，作为响应，它将发送变量 `LOGIN` 定义的字符串（我们在脚本早期定义的）。

  这部分对话取决于 ISP 选择发送什么样的登录提示。例如，如果它的登录提示以冒号 `:` 结尾，那么这部分对话将失败。你必须检查 ISP 如何配置其登录程序，以确保这部分对话完全无误。（正如你所看到的，当我们说编写拨号脚本是一项令人痛苦的任务时，并不是在开玩笑！）

# 第3 章：为你的 Linux 系统添加网络软件

- `password:$PASSWORD` – 这结束了我们与 ISP 系统的对话。脚本会等待一个以冒号结尾的字符串：这可能表示 `Password:` 或 `password:`。响应此提示，对话将发送由环境变量 `PASSWORD` 定义的字符串，这是我们在该脚本稍早些时候设置的。再次强调，你必须确保提示词的字母完全匹配。然而，一旦正确完成了这一步，你就完成了——你已经与 ISP 的机器建立了连接。

- `EOF` – 此行标记了之前脚本之前定义的文档的结束——因此，这些行被回显到 DIALCRIPT 文件中。

- `/usr/sbin/chat v $DIALCRIPT` – 现在我们已经构建了拨号脚本，现在执行此命令。该命令将执行相应的指令。

- 参数 `-f $DIALCRIPT` 告诉 `chat` 从环境变量 `DIALCRIPT` 指定的文件获取其聊天脚本，而不是从命令行参数。

- 选项 `-v` 告诉 `chat` 记录登录过程的每一步。日志消息由守护进程 `syslog` 捕获，并默认写入 `/usr/adm/messages`——尽管这可能与你的 Linux 版本有所不同（我们将在本章稍后详细讨论 `syslog`）。正如我们在章后部分描述的，当你调试聊天脚本时，这个功能价值价值。

就是这些——我们完成了。当此脚本执行时，它会构建 `DIALCRIPT`，然后调用 `chat` 执行该脚本。脚本执行时，`chat` 使用拨号脚本连接到你的调制调器，拨打你的 ISP 电脑，执行登录程序，删除存放聊天脚本的文件并退出。一旦此命令将你的系统登录到 ISP 机器，它就会退出并将控制权交还给 `pppd`（记住，此脚本是作为 `pppd` 命令行的参数被调用的）。`pppd` 与 ISP 的 PPP 服务器进行协商，建立 PPP 链路。只有这样，你才能启动系统与 Internet 交换数据报。

## 调试脚本

现在见真章的时刻到了：让我们试一下。要做到这一点，使用 `su` 切换到超级用户 `root`，然后输入命令：

```bash
ppp on
```

过了一会儿，此脚本将调用守护进程 `/usr/sbin/pppd`，构建一个聊天脚本，调用命令 `chat` 执行该脚本。你应该能听到或看到调制调器拨号，然后进行协商并与 ISP 机器建立连接。

正如我们之前提到的，命令 `chat` 的选项 `-v` 告诉它记录所有的活动。系统守护进程 `syslogd` 捕获这些消息并默认将它们存储在文件 `/usr/adm/messages` 中，尽管你的系统可能配置为使用另一个文件。下面的摘录显示了使用上述示例脚本成功建立 PPP 连接时生成的日志消息。我们会在必要的地方进行注释。

第一条日志消息显示调用了 `chat` 命令并设置了默认超时时间：

```
Dec 28 09:42:57 systemchat chat[5384]: timeout set to 10 seconds
```

接下来的三条日志消息显示 `chat` 在我们的对话中执行指令：

```
ABORT '\nBUSY\r'
ABORT '\nNO CARRIER\r'
ABORT '\nNO ANSWER\r'
```

接下来的日志消息显示 `chat` 在我们的对话中执行指令 `'\nAT\r`：

```
Dec 28 09:42:57 systemchat[5384]: send (^JAT^M^M)
Dec 28 09:42:57 systemchat[5384]: expect (OK)
Dec 28 09:42:57 systemchat[5384]: "M"
Dec 28 09:42:57 systemchat[5384]: OK-got it
Dec 28 09:42:57 systemchat[5384]: send (ATDT5554321-M)
```

接下来的日志消息显示 `chat` 在我们的对话中执行 `OK ADDT$PHONE`：

也就是说，在我们发送调制调器指令后，脚本期望从调制调器听到 `OK`。该字符串已接收（如消息 `got it` 所示），响应此提示，脚本发送了拨打 ISP 电话号码的指令。（在这里我们将 ISP 的电话号码设置为 "5554321"）。

接条日志消息显示 `chat` 在我们的对话中执行 `TIMEOUT 30`：

```
Dec 28 09:42:58 systemchat[5384]: timeout set to 30 seconds
```

现在情况变得有点复杂了。在此时，脚本已经拨打了 ISP 的调制调器并与其建立了连接。剩余的对话不是与你的调制调器通信，而是与 ISP 的机器通信。接下来的日志消息显示 `chat` 在我们的对话中执行指令 `'ion.\\r\d\d\r`——也就是说，对话等待 ISP 机器发送一个以 `ion,` 结尾的字符串，并相应发送一系列回车符，以跳过 ISP 在登录提示符之前显示的任何杂乱信息：

```
Dec 28 09:42:58 system chat[5384]: expect (ion).
Dec 28 09:42:58 system chat[5384]: *M
Dec 28 09:43:16 system chat[5384]: *M
Dec 28 09:43:16 system chat[5384]: CONNECT
SI120U/ARO/V34/LAPM/V42B5*M
Dec 28 09:43:17 system chat[5384]: *M
Dec 28 09:43:17 system chat[5384]: Welcome to Internet Provider
Dec 28 09:43:17 system chat[5384]: Chicago, Illinois*M
Dec 28 09:43:17 system chat[5384]: *M
Dec 28 09:43:17 system chat[5384]: enter 'guest' at login and password prompts*M
Dec 28 09:43:17 system chat[5384]: for more information.-got it
Dec 28 09:43:17 system chat[5384]: send (*M^d*M^d*M)
```

我们的脚本等待 Internet 服务商向我们发送一个以 `ion` 结尾的提示符。Internet 服务商会显示大量供人类阅读的信息，以 `information` 一词结尾——这就是我们编写脚本的地方。`got` 词显示预期的字符串已接收。脚本随后发送了三个回车符，其之间有微小的延迟，以跳过这一部分——就像是你亲自在与 ISP 机器交互并多次按下 Enter 键一样。

接下来的日志消息显示 `chat` 在我们的对话中执行指令 `login:-login`：

```
Dec 28 09:43:19 system chat[5384]: expect (login):
Dec 28 09:43:19 system chat[5384]: *M
Dec 28 09:43:19 system chat[5384]: *M
Dec 28 09:43:19 system chat[5384]: User Access Verification*M
Dec 28 09:43:19 system chat[5384]: *M
Dec 28 09:43:19 system chat[5384]: ISPI login-got it
```

接下来的日志消息显示 `chat` 在我们的对话中执行 `login:-login`：

```
Dec 28 09:43:19 system chat[5384]: expect (login):
Dec 28 09:43:19 system chat[5384]: *M
Dec 28 09:43:19 system chat[5384]: *M
Dec 28 09:43:19 system chat[5384]: User Access Verification*M
Dec 28 09:43:19 system chat[5384]: *M
Dec 28 09:43:19 system chat[5384]: ISPI login-got it
```

## 第 3 章：为你的 Linux 系统添加网络软件

## ppp-on

以下是一个包含认证所需选项的 ppp 示例。在此示例中，我们的 Linux 工作站 `myexample` 正在拨打名为 `myisp` 的 ISP。我们假设你已经按照我们描述的方法设置了 `chap secrets` 和 `pap secrets` 文件：

```sh
#!/bin/sh
#
MYNAME=myexample
ISPNAME=myisp
DIALER_SCRIPT=/etc/ppp/ppp-on dialer
#
exec /usr/sbin/pppd name $MYNAME remotename $ISPNAME lock modem
crtscts=
	/dev/ttyS0 38400 noip defaultroute
$DIALER_SCRIPT
```

该脚本中的前三个指令定义了三个变量：

- `MYNAME` - 该变量定义了你的站点向远程 PPP 服务器标识身份的名称。如果你不设置此标识符，pppd 默认将传递你的系统名称。

- `ISPNAME` - 该变量定义了你将拨打的远程主机名称。通常，这个远程主机是一个互联网服务提供商，因此变量名如此。

- `DIALER_SCRIPT` - 该变量定义了拨打电话并与远程调制调器建立连接的脚本名称。我们将在本章后面讨论这个脚本。

第二个命令调用了 `pppd`。如你所见，我们使用了 `pppd` 的绝对路径以避免安全漏洞。我们还在命令前加了 `exec` 命令，作为一种安全措施，它让 `pppd` 作为一个独立的进程执行，而不是作为脚本进程的子进程。

当我们调用 `pppd` 时，我们传递了以下命令行参数：

- `name $MYNAME` - 此参数设置了 pppd 标识身份的名称。它会将此名称传递给远程主机的 PPP 服务器，服务器将使用该名称来查找正确的密钥（存储在 `pap secrets` 和 `chap secrets` 文件中）并传递给 PPP 服务器。如果你不设置此参数，pppd 默认使用你的主机名称来标识其身份。

# 第二部分：安装网络

- `remotename $ISP` - 此参数设置了远程主机的名称，pppd 将使用此选项来帮助查找传递给 PPP 服务器的正确密钥。请注意，此参数是可选的。如果你将拨入远程站点的机器池（大型商业 ISP 通常如此），你可能不知道你将连接的主机标识符；在这种情况下，你不应该使用此选项；相反，你应该将 `secrets` 文件中的服务器名称设置为通配符 `*`，并仅使用本地名称（通过参数 `name` 设置）来查找密钥。

- `lock` – 当 pppd 打开调制调器的串口端口时写入一个锁文件。

- `modem` – 与串口端口使用调制调器连接交互。

- `crtscts` – 在调制调器上使用硬件流控。
