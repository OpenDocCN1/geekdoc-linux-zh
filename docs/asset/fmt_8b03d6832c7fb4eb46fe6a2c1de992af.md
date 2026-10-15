
# 第 25 章 使用 SLIP 和 PPP

### 表 25.1 dip 常用参数

| 参数 | 描述 |
| :--- | :--- |
| `-a` | 提示用户名。 |
| `-t` | 以命令模式运行 `dip`。 |
| `-v` | 与 `-t` 使用显示当前错误级别。 |
| `-i` | 告诉 `dip` 以输入模式运行。 |
| `-m` | 强制 `dip` 使用指定的 MTU 值。 |
| `scriptfile` | 要运行的 `dip` 脚本。 |

### 表 25.2 dip 可用命令

| 命令 | 描述 |
| :--- | :--- |
| `chatkey keyword [code]` | 将关键字和错误代码添加到 `dial` 命令返回的错误集中。`chatkey` 命令可以检测调制解调器返回 `BUSY`、`VOICE` 或其他消息。 |
| `config [arguments]` | 允许你直接操作 `dip` 提供的接口。此命令通常被禁用，因为存在严重的安全风险。必须轻微修改源代码 `file.c` 来启用此命令。 |
| `databits bits` | 设置每个字节中可用数据的位数。这适应了 6 位和 7 位拨号连接。 |
| `default` | 导致 `dip` 在内核路由表中设置指向远程主机的默认路由。 |
| `dial num` | 设置指定的号码。 |
| `echo on\|off` | 开启或关闭。开启 `echo` 后 `dip` 会显示它发送和接收的内容。 |
| `flush` | 丢弃任何尚未读取的调制解调器响应。 |
| `get $var` | 将变量 `$var` 设置为常量或远程常量、提示用户输入值、或从串行行获取下一个单词并赋值给 `$var`。 |
| `goto label` | 跳转到 `dip` 脚本中的指定标签。 |
| `help` | 在命令模式下显示可用命令列表。 |
| `if $var op number` | 在 `goto label` 脚本中执行条件分支。`$var` 必须是 `$err1`、`$locip` 或 `$retip` 之一。数字必须是整数，可用的运算符具有传统的 C 语言含义：`==`, `!=`, `<`, `>`, `<=`, 和 `>=`。 |

### 表 25.2 续

| 命令 | 说明 |
| --- | --- |
| `init initstring` | 将通过重置命令发送到调制解调器的初始化字符串设为 `initstring`。 |
| `mode SLIP\|CSLIP` | 设置连接的协议模式并让 `dip` 进入守护进程模式。此命令通常会让 `dip` 进入守护进程模式，而不会将控制权返回给脚本或 `<DIP>` 命令行。 |
| `modem HAYES` | 设置调制解调器类型。仅支持 `HAYES` 调制解调器类型。（`HAYES` 必须大写）。 |
| `netmask mask` | 将 `dip` 安装的路由的子网掩码设置为 `mask`。 |
| `parity E\|O\|N` | 设置串口的校验位：偶数、奇数或无。 |
| `password` | 提示用户输入密码并以安全的方式获取。此命令在输入密码时不会回显密码。 |
| `print` | 在启动 `dip` 的控制台上回显文本。文本中的变量将被替换为其值。 |
| `port dev` | 设置 `dip` 使用的设备。 |
| `quit` | 退出 `dip` 程序。 |
| `reset` | 向串口发送初始化字符串。 |
| `send text` | 将指定的文本发送到串口。可以正确处理传统的 C 语言风格反斜线序列。 |
| `sleep num` | 延迟处理指定的秒数。 |
| `speed num` | 设置串口波率。 |
| `stopbits bits` | 设置串口使用的停止位数量。 |
| `timeout num` | 将默认超时时间设置为整数值 `num`。单位为秒。 |
| `term` | 让 `dip` 进入终端仿真模式。这允许你直接与串口链路进行交互。按下 `<Ctrl->>` 可返回 `DIP` 提示符。 |
| `wait word num` | 让 `dip` 等待串口上出现指定的单词，超时时间为 `num` 秒。 |

## 使用 dip 自动化 SLIP 操作

`dip` 还提供了许多供你使用的变量。其中一些变量（如本地和远程 IP 地址）可以由你设置；另一些是只读的，用于诊断和信息目的。每个变量都以美元符号开头，并且必须以小写输入。表 25.3 列出了这些变量及其用途。

### 表 25.3 dip 提供的变量

| 变量 | 说明 |
| --- | --- |
| `$local` | 本地机器的主名。 |
| `$locip` | 分配给本地机器的 IP 地址。 |
| `$remote` | 远程机器的主名。 |
| `$rmtip` | 远程机器的 IP 地址。 |
| `$mtu` | 连接的 MTU（最大传输单元）值。 |
| `$modem` | `dip` 使用的调制解调器类型（只读）。 |
| `$port` | `dip` 使用的串口设备名称。 |
| `$speed` | 串口设备的速率设置（只读）。 |
| `$errlvl` | 上一个执行的命令的结果码（只读）。零表示成功；任何其他值均表示错误。 |

将 `$local` 或 `$remote` 变量设置为主机名会导致 `dip` 解析该主机名的 IP 地址并将其存储在相应的 IP 地址变量中。这可以为你编写的脚本减少了一个步骤。

> 注意：你无法直接使用 `get` 命令设置只读变量。

## 配合静态 IP 地址使用 dip

为使用 SLIP 提供商的每台机器分配单独的 IP 地址是非常。当你的机器向远程主机发起 SLIP 链路时，`dip` 会用此已知地址配置 SLIP 接口。列表 25.1 是使用静态 IP 地址从 `unit1.tristar.com` 到 `unit1.tristar.com` 发起 SLIP 链路的 `dip` 脚本。

### 列表 25.1 通过 SLIP 使用静态 IP 地址的 dip 脚本

```bash
+ * 使用 unit1 连接到 unit1
+ * Connect unit1 to unit1 using unit1
+ * Connect unit1 to unit1 using unit1

+ set localIP 192.168.1.1
set remoteIP 192.168.1.2
set netmask 255.255.255.0
mode SLIP
timeout 30
port /dev/ttyS0
speed 3840
modem HAYES
reset
init "ATZ"
send "ATDT" "
noecho
password
print "Connected to /dev/ttyS0
sleep 10
wait "OK" 5
wait "AT
print "SLIP connection established"
exit
```

就是这些。设置好 SLIP 账户和 `/etc/diphosts` 文件即可完全配置您的系统以支持入站的 SLIP 链接。

## 使用 PPP

点对点协议（PPP）是另一种用于串行链路发送数据报文的协议。PPP 在 SLIP 之后开发，包含了许多 SLIP 欠缺的功能。它可以自动协商如 IP 地址、数据大小和客户端授权等选项。它还可以封装来自 IP 以外协议的数据包。

## 使用 pppd 和 chat 自动化 PPP 链接

PPP 分为两个部分：Linux 内核中的 PPP 驱动程序和用户必须运行的 `pppd` 程序。使用 PPP 最基本的方法是使用通信程序手动登录远程主机，并在远程和本地主机上手动启动 `pppd`。使用配合 `pppd` 的 `chat` 脚本会更方便，它可以处理调制调器控制、登录到远程主机并启动 `pppd`。在深入研究 `pppd` 之前，先简单查看 `chat`。

**使用 `chat` 程序**是一个用于自动化您的计算机与调制调器之间交互的程序。它主要用于在本地和远程 `pppd` 守护进程之间建立调制调器连接。`chat` 的语法为

```bash
chat [options] script
```

表 25.4 列出了 `chat` 程序的命令行选项。

### 表 25.4 chat 程序的命令行选项

| 选项 | 描述 |
| --- | --- |
| `-f filename` | 使用指定文件的 `chat` 脚本 |
| `-l lockfile` | 使用指定的锁文件创建一个 UUCP 风格的锁文件 |
| `-t num` | 使用指定的数字作为每个字符串的秒超时时间 |
| `-v` | 将发送和接收的所有内容记录到系统日志 (`syslog`) |
| `script` | 要使用的 `chat` 脚本 |

您不能同时使用 `-f` 选项或指定 `chat` 脚本——它们是互斥的。如果您在 `chat` 中使用了 `-l` 选项，请不要在 `pppd` 中使用 `lock` 选项，因为 `chat` 脚本创建的锁文件会导致 `pppd` 失败，因为它认为调制调器设备已在占用。

> **提示** 在调试脚本时，在一个虚拟控制台上运行 `tail -f /var/adm/messages`，并在运行 `chat` 时使用 `-v` 选项。这样您就可以在第一个虚拟控制台上观察 `chat` 正在进行的对话内容。

## 创建 chat 脚本
