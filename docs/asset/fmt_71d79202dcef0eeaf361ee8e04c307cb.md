
`dip` 手册页中包含一个示例 `dip` 聊天脚本，请显示并阅读手册页内容，然后保存该文件（通过重定向或复制手册页源文件）并编辑脚本。以下是一个示例聊天脚本，必要时您可以手动输入，当然要确保填入您自己的数据：

```bash
# SLIP 连接脚本
# 获取目标主机的 IP 地址。

main:
# 设置所需的串行端口和速度。
port /dev/cua0
speed 38400
# 重置调制解调器和终端线路。
reset
# 准备拨号。
send ATZ1\r
wait OK 4
if $errlvl != 0 goto error
dial 666-0999		## 更改为您的服务器号码！
if $errlvl != 0 goto error
wait CONNECT 60
if $errlvl != 0 goto error
# 已连接。登录到系统。
login:
sleep 3
send \r\n\r\n
wait merlin> 20	## 更改为您的服务器提示符
if $errlvl != 0 goto error
send login\n
wait name: 10	## 等待用户名：提示
if $errlvl != 0 goto error
send login_name\n		## 更改为您自己的用户名
wait ord: 10		## 等待密码提示
if $errlvl != 0 goto error
send my_password\n		## 更改为您自己的密码！
wait merlin> 10
if $errlvl != 0 goto error
send slip\n		## 更改以适配您的服务器
wait SLIP 30		### 等待 SLIP 提示
if $errlvl != 0 goto error
get $local remote 10	## 假设服务器在您输入 slip 后立即发送您的 IP..
if $errlvl != 0 goto error	## 地址。
get $remote merlin	## 从 /etc/hosts 获取 slip 服务器地址
done:
print CONNECTED to $remote with address $rmtip we are $local
default
mode SLIP
goto exit
error:
print SLIP to $host failed.
exit:
# 结束 dip 脚本
```

目前有多种不同变体的聊天脚本可供选择，包括大多数 CD-ROM 发行版中附带的一些脚本。如果您可以访问互联网，可以在某些 FTP 站点或 Linux 新闻组上找到它们。

## 设置 PPP

`PPP` 是比 `SLIP` 更强大的协议，对于大多数用途来说更受青睐。`PPP` 功能分为两部分；一部分用于高级数据链路控制（`HLDC`）协议，有助于定义两台机器之间发送 `PPP` 数据报的规则；另一部分用于名为 `pppd` 的 `PPP` 守护进程，它在 `HLDC` 系统建立通信参数后处理该协议。

与 `SLIP` 一样，`PPP` 在两台机器之间建立调制解调器链路，然后将线路控制权移交给 `PPP`。在建立 `PPP` 链路之前，必须建立回环驱动程序。即使使用 `/etc/hosts` 文件或简单的仅缓存 `DNS` 名称服务器，你也应该拥有一个正在运行的名称解析系统。（请参阅本章后面“使用 `DNS` 进行 `SLIP` 和 `PPP`”一节。）

## 设置 PPP 账户

如果你允许人们通过 `PPP` 拨入你的系统，出于安全原因，最好使用一个名为 `PPP` 的特殊用户账户来运行 `PPP`。如果你只是向外拨号，则无需这样做，你可以轻松地从任何用户账户使用 `PPP`；但为了更安全的操作，考虑仅为 `PPP` 创建一个新用户，特别是在允许拨入时。首先，你需要向系统添加一个新用户。你可以使用操作系统通常使用的任何脚本（如 `newuser`、`adduser`，或直接编辑 `/etc/passwd` 文件）。

一个 `PPP` 账户（`UID` 设置为 `201`，`GID` 设置为 `51`）的 `/etc/passwd` 条目示例如下：

```bash
ppp:*:201:51:PPP account:/tmp:/etc/ppp/pppscript
```

在这种情况下，账户没有设置密码（因此没有人可以登录到该账户），并且由于没有创建文件，所以使用 `/tmp` 作为主目录。启动程序设置为 `/etc/ppp/pppscript`，这是您创建的一个包含配置信息的文件。（你可以使用任何文件名代替 `pppscript`。）

`pppscript` 文件的示例如下：

```bash
#!/bin/sh
msg n
stty -echo
exec pppd -detach silent modem crtscts
```

第一行强制脚本在 Bourne（或 bash）shell 中执行，无论您当前运行的是哪种 shell（详见第 14 章“Shell 编程”）。第二行关闭了所有尝试写入 `PPP` 账户 `tty` 的行为。第三行的 `stty` 命令是必要的，用于阻止远程发送的所有内容再次被回显到屏幕上。最后，最后一行的 `exec` 命令运行 `pppd` 守护进程（它处理所有 `PPP` 流量）。您稍后将在本节中了解 `pppd` 守护进程及其选项。

## 使用 chat 向外拨号

`PPP` 要求在接管并处理通信之前，必须先与远程机器建立调制解调器连接。目前有几种实用程序可以执行此操作，但最常用的是 `chat`。`chat` 程序很受欢迎，因为它使用类似于 `UUCP` 的脚本风格。

要使用 `chat`，请组装一个与 `UUCP` `/etc/Systems` 文件条目几乎相同的命令行。例如，要使用 Hayes 兼容调制解调器（使用 `AT` 命令集）呼叫号码 `555-1234` 的远程机器，请使用以下命令。它格式化为 `UUCP` 风格的 chat 脚本：

```bash
chat "" ATZ OK ATDT5551234 CONNECT "" login: ppp word: secret1
```

所有条目都采用 `UUCP` 的发送-期望格式，发送的内容位于从指定远程接收到的内容之后。chat 脚本始终以期望字符串开始，该字符串必须设置为空，因为如果没有信号发给调制解调器，它不会响应。在空字符串之后，首先发送 `ATZ`（重置）命令并等待来自调制解调器的 `OK`，然后发送拨号命令。收到来自调制解调器的 `CONNECT` 消息后，将执行远程机器的登录脚本，过程如下：首先发送一个空白字符，然后出现 `login:`（登录）提示符，接着发送登录名 `ppp`，等待 `word:`（密码）提示符，最后发送密码（当然要替换为您的登录名和密码）。登录完成后，`chat` 终止但保持线路开启。

如果连接的另一端在调制解调器应答时没有立即以登录脚本响应，您可能需要强制通过线路发送 `BREAK` 命令以唤醒远程端。这通过以下命令完成：

```bash
chat -v "" ATZ OK ATDT5551234 CONNECT "" ogin:-BREAK-ogin: ppp word: secret1
```

这种类型的 chat 条目存在安全问题，因为任何执行 `ps -ef` 命令的用户都能看到整条命令行（包括其中的密码）。如果您是系统中唯一的用户，这不是问题，但为了避免麻烦，您可以将命令中的脚本部分嵌入到文件中，并将该文件读取到 `chat` 中。这会导致脚本不出现在 `ps` 输出中。要调用文件供 `chat` 使用，请使用 `-f` 选项：

```bash
chat -f chat_file
```

`chat_file` 将包含以下行：

```
"" ATZ OK ATDT5551234 CONNECT "" login: ppp word: secret1
```

聊天脚本可以帮助你检测常见的错误状况，例如线路忙或连接未建立。你的调制解调器发送的消息（标准 Hayes 命令集分别使用 `BUSY` 和 `NO CARRIER` 消息）通过 `ABORT` 选项嵌入聊天脚本中，这允许你在这些错误状况之一发生时优雅地退出聊天脚本。为了处理这些中止条件，在正常的聊天脚本之前嵌入聊天关键字 `ABORT` 以及应触发的中止消息。例如，若要修改上述聊天脚本以在调制解调器返回 `BUSY` 或 `NO CARRIER` 消息时中止，脚本如下所示：

```
ABORT BUSY ABORT 'NO CARRIER' "" ATZ OK ATDT5551234 CONNECT "" login: ppp word: secret1
```

我们需要两个 `ABORT` 命令，因为每个命令只接受一个参数。聊天脚本的其余部分保持不变。注意 `NO CARRIER` 消息周围的引号，否则中间的空格会使脚本感到困惑。

## 运行 pppd

如果你已经建立了一个 `PPP` 连接，并且你的机器使用 `PPP` 账户登录到远程机器，你可以启动 `pppd` 守护进程来控制 `PPP` 会话。如果由于你的机器使用设备 `/dev/cua1`（`Linux` 中用于带调制解调器控制的第一串行端口）进行 `38400` 波特率的 `PPP` 连接，请使用以下命令启动 `pppd` 守护进程：

```
pppd /dev/cua1 38400 crtscts defaultroute
```
