

## TAC 用户 ID
telnet 支持 TAC 用户 ID（也称为 TAC 访问控制系统，或 TACACS 用户 ID）选项。在主机服务器上启用该选项后，用户无需进行第二次登录序列即可通过 telnet 连接到该主机。TAC 用户 ID 选项使用与 rologin 相同的安全机制，用于授权远程主机和用户的访问。系统管理员必须在被指定为参与主机的系统上启用（telnetd）选项。系统管理员还必须为每个 TAC 用户 ID 用户在允许使用该功能的所有系统上分配完全相同的 UID。（参见 telnetd(1M) 和《系统管理任务手册》，PN 3355-00051。）

## 选项
以下 telnet 选项可用：

- `-8` 在本地 tty 上启用 cs8（8 位传输）。
- `-ec` 将 telnet 命令模式转义字符设置为 `^c`，而不是其默认值 `^`。
- `-l` 如果在客户端启用了 TAC 用户 ID 选项，则禁用该选项，以便提示用户输入登录用户名和密码。省略 -l 选项将执行默认设置。

## 命令

以下命令可在命令模式下使用。您只需输入每个命令的足够部分以唯一标识它即可（对于 mode、set、toggle 和 display 命令的参数也是如此）。

- `open host [port]` 在指定端口处打开与命名主机的连接。如果未指定端口，telnet 将尝试在标准 TELNET 端口联系 TELNET 服务器。主机名可以是 gethostbyname() 所理解（参见 gethostent(3N)）的官方名称或别名，也可以是 hosts(4) 中描述的以点分表示法指定的互联网地址。如果未给出主机名，telnet 将提示输入一个。
- `close` 关闭一个 TELNET 会话。如果该会话是从命令模式启动的，telnet 将返回到命令模式；否则 telnet 将退出。
- `quit` 关闭任何打开的 TELNET 会话并退出 telnet。文件结束（在命令模式下）也将关闭会话并退出。
- `z` 挂起 telnet。如果 telnet 是从支持作业控制的外壳程序（如 csh(1) 或 ksh(1)）运行的，z 命令将挂起 TELNET 会话并让用户返回到调用 telnet 的外壳程序。然后可以使用 fg 命令恢复该作业（参见 csh(1) 或 ksh(1)）。
- `mode mode` 将 telnet 的用户输入模式更改为 mode，该模式可以是 character（“逐字符”模式）或 line（“逐行”模式）。远程主机将被请求进入所请求模式的权限。如果远程主机能够进入该模式，则进入所请求的模式。在 character 模式下，telnet 在键入每个字符时将其发送到远程主机。在 line 模式下，telnet 将用户输入收集为行，并在用户键入回车符、换行符或 EOF（通常是 `^D`；参见 stty(1)）时向远程主机传输每一行。请注意，设置 line 模式还会设置本地回显。期望逐字符解释用户输入的应用程序（如 more、csh、ksh 和 vi）在 line 模式下无法正常工作。
- `status` 显示 telnet 的当前状态。telnet 报告当前转义字符。如果 telnet 已连接，它报告其连接的主机和当前模式。如果 telnet 未连接到远程主机，它报告 No connection。一旦 telnet 已连接，它报告本地流量控制开关值。
- `display [argument ...]` 显示所有或部分 set 和 toggle 值（参见下文）。
- `? [command]` 获取帮助。如果没有参数，telnet 打印帮助摘要。如果指定了命令，telnet 仅打印关于该命令的帮助信息。帮助信息仅限于对该命令的一行描述。
- `! [shell_command]` 外壳程序逃逸。检查 SHELL 环境变量以确定执行命令所使用的 shell 名称。如果未指定 shell_command，将启动一个 shell 并将其连接到用户的终端。如果 SHELL 未定义，则使用 /usr/bin/sh。

### send 参数
向远程主机发送一个或多个特殊字符序列。每个参数可以具有以下任何值（每个 send 命令可以指定多个参数）：

- `escape` 发送当前的 telnet 转义字符（初始为 `^]`）。
- `synch` 发送 TELNET SYNCH 序列。此序列导致远程系统丢弃所有之前键入（但尚未读取）的输入。此序列作为 TCP 紧急数据发送（在某些系统上可能不起作用——如果不起作用，终端上可能会回显小写字母 `r`）。
- `brk` 发送 TELNET BRK（中断）序列，这对远程系统可能具有意义。
- `ip` 发送 TELNET IP（中断进程）序列，这应导致远程系统中止当前正在运行的进程。
- `ao` 发送 TELNET AO（中止输出）序列，这应导致远程系统将远程系统的所有输出冲洗到用户的终端。
- `ayt` 发送 TELNET AYT（你在吗）序列，远程系统可能选择响应也可能不响应。
- `ec` 发送 TELNET EC（擦除字符）序列，这应导致远程系统擦除最后一个输入的字符。
- `el` 发送 TELNET EL（擦除行）序列，这应导致远程系统擦除当前正在输入的行。
- `ga` 发送 TELNET GA（继续）序列，这可能对远程系统没有意义。
- `nop` 发送 TELNET NOP（无操作）序列。
- `?` 打印 send 命令的帮助信息。

### set variable_name value
将若干 telnet 变量中的任何一个设置为特定值。特殊值 off 关闭与变量相关联的功能。变量的值可以通过使用 display 命令来显示。可以指定以下 variable_name：

- `echo` 这是该值（初始为 ^E），在逐行模式下，在显示输入的字符的本地回显（用于正常处理）和抑制输入字符的回显（例如用于输入密码）之间切换。
- `escape` 这是 telnet 转义字符（初始为 ^\），当连接到远程系统时，它会导致进入 telnet 命令模式。
- `interrupt` 如果 telnet 处于 localchars 模式（参见下文 toggle localchars）并且键入了中断字符，则向远程主机发送 TELNET IP 序列（参见上文 send ip）。中断字符的初始值取自终端的 intr 字符。
- `quit` 如果 telnet 处于 localchars 模式（参见下文 toggle localchars）并且键入了退出字符，则向远程主机发送 TELNET BRK 序列（参见上文 send brk）。退出字符的初始值取自终端的 quit 字符。
- `flushoutput` 如果 telnet 处于 localchars 模式（参见下文 toggle localchars）并且键入了 flushoutput 字符，则向远程主机发送 TELNET AO 序列（参见上文 send ao）。flush 字符的初始值为 ^O。
- `erase` 如果 telnet 处于 localchars 模式（参见下文 toggle localchars），并且 telnet 以逐字符模式运行，则当键入此字符时，向远程系统发送 TELNET EC 序列（参见上文 send ec）。erase 字符的初始值取自终端的 erase 字符。
- `kill` 如果 telnet 处于 localchars 模式（参见下文 toggle localchars），并且 telnet 以逐字符模式运行，则当键入此字符时，向远程系统发送 TELNET EL 序列（参见上文 send el）。kill 字符的初始值取自终端的 kill 字符。
- `eof` 如果 telnet 以逐行模式运行，在行的第一个字符位置输入此字符会导致向远程系统发送该字符。eof 字符的初始值取自终端的 eof 字符。

### toggle arguments ...

切换（在 TRUE 和 FALSE 之间）各种控制 telnet 如何响应事件的标志。可以指定多个参数。这些标志的状态可以通过使用 display 命令来显示。有效参数为：

- `localchars` 如果为 TRUE，则 flush、interrupt、quit、erase 和 kill 字符（参见上文 set）在本地被识别，并转换为适当的 TELNET 控制序列（分别为 ao、ip、brk、ec 和 el；参见上文 send）。此 toggle 的初始值在逐行模式下为 TRUE，在逐字符模式下为 FALSE。
- `autoflush` 如果 autoflush 和 localchars 均为 TRUE，每当识别出 ao、intr 或 quit 字符（并转换为 TELNET 序列 - 有关详细信息请参见上文 set）时，telnet 将拒绝在用户的终端上显示任何数据，直到远程系统确认（通过 TELNET Timing Mark 选项）已处理这些 TELNET 序列。此 toggle 的初始值为 TRUE。
- `autosynch` 如果 autosynch 和 localchars 均为 TRUE，当键入 intr 或 quit 字符（有关 intr 和 quit 字符的描述请参见上文 set）时，发送的结果 TELNET 序列后面跟随 TELNET SYNCH 序列。此过程应导致远程系统开始丢弃所有之前键入的输入，直到两个 TELNET 序列都被读取并执行。此 toggle 的初始值为 FALSE。
- `binary` 在输入和输出上启用或禁用 TELNET BINARY 选项。此选项应该

