
本节提供了许多关于 `dip` 命令的辅助信息。节末尾提供了一个 `dip` 脚本，它由变量列表和命令列表。但首先，表 13.1 列出了给 `dip` 最常用的命令行参数。

| 表 13.1. 常用 dip 命令参数 |
| --- | --- |
| -a | 提示用户名和密码。 |
| -i | 作为拨号服务器运行。 |
| -k | 杀死锁定了指定设备或最近调用的 `dip` 进程。 |
| -l | 指示要杀死的线路。 |
| - mtu | 设置最大传输单元 (MTU)；默认值为 296。 |
| -p proto | 将线路协议设置为这些之一：SLIP, CSIP, SLIP6, CLSIP6, PPP 或 TERM。 |
| -t | 在（交互模式或命令模式）下运行 `dip`。 |
| -v | 设置详细模式。这将启用调试输出，包含脚本的每一行。 |

如你所见，`dip` 也可以通过 `-i` 切换作为拨号服务器使用。`dip` 命令还可以在交互模式（或命令模式）下被调用，由 `-t` 切换指定。这允许你参与拨号和登录过程，允许你记录建立现代连接所需的提示和响应。然后你可以使用结果并建立一个脚本来自动化该过程。

表 13.2 列出了 `dip` 支持的命令。只需输入命令以及任何所需的参数并按回车。这些命令可以包含在聊天脚本中，也可以在你处于命令模式时使用：

| 表 13.2. 常用 dip 命令 |
| --- | --- |
| iabel: | 定义一个标签。 |
| beep [times] | 在用户终端上蜂响 [times] 次。 |
| bootp [howany|howlong] | 使用 BOOTP 协议获取本地和远程 IP 地址。 |
| Break | 发送 BREAK 信号。 |
| chatkey keyword [code] | 允许你向 `dip` 的现代响应添加内容。 |
| config [interface|routing|preup|down|post] | 存储接口配置 [arguments...] 参数。 |
| databits 78 | 设置数据位数。 |
| Command | Description |
| `dec Variable [decrement-value${Variable}]` | 递减变量值；默认值为 1。 |
| Default | 指示 `dip` 将默认路由设置为其所连接的远程主机。 |
| `dial phoneNumber [timeout]` | 将 `init` 变量中的字符串作为调制解调器初始化字符串发送，然后拨号指定号码。默认超时时间为 60 秒。`Dip` 将解析解调器返回的任何字符串并相应地设置 `result`。代码为：0- OK, 1- CONNECT, 2- ERROR, 3- BUSY, 4- NO CARRIER, 5- NO DIALTONE。你可以用 `chatkey` 命令更改或添加这些代码。 |
| `echo off` | 启用或禁用调制器命令的显示。 |
| `exit [exit-status]` | 退出脚本，保持已建立的 [SLIP] 连接完好并运行 `dip`。 |
| `flush` | 刷新终端上的输入。 |
| `get Variable [ask|remote [timeout${Variable]]` | 获取指定变量的值。如果参数是 ask，则打印提示符并从标准输入读取值。如果参数是 remote，则从远程机器读取值。否则，参数是常量或另一个提供值的变量。 |
| `goto label` | 将 `chat` 脚本的控制权转移到指定的标签。 |
| `help` | 打印命令列表。 |
| `if expr goto label` | 测试条件。`expr` 必须具有 `Variable operator constant` 的形式，其中操作符为以下之一：`==`, `!=`, `<`, `<=` |
| `inc Variable [increment-value${Variable}]` | 增加指定变量。默认增量为 1。 |
| `init init-string` | 将初始化字符串设置为指定的字符串（默认是 AT E0 Q0 V X4）。注意初始化字符串在拨号命令发出之前发送。 |
| `node` | 设置线路协议。 |
| `[SLIP|SLIP6|PPP|TERM]` | 设置解调器类型。 |
| `modem-name` | 指示要使用的网络地址。 |
| `netmask xxx.xxx.xxx.xxx` | 在 `dip` 退出后执行指定的命令。工作类似于 `shell` 命令，但仅在 `dip` 完成时执行。即执行 `exit` 命令。 |
| `onexit` | 设置类型。 |
| `parity` | 设置奇偶性。 |
| `password` | 请求密码。 |
| `proxy` | 设置代理。 |
| `print` | 打印输出。 |
| `reset` | 重置。 |
| `shell` | 执行 shell。 |
| `sleep` | 等待。 |
| `speed` | 设置速度。 |
| `term` | 进入终端。 |
| `timeout` | 设置超时时间。 |
| `wait` | 等待。 |

表 13.3 描述每个变量。注意变量以 `$` 符号开头。

| Variable | Description |
|---|---|
| `$servI1` | 上一个命令的结果 |
| `$localip` | 本地主机的点点 IP |
| `$local` | 完整的本地主机名 |
| `$rmtip` | 远程主机的点 IP |
| `$remote` | 完整的远程主机名 |
| `$mtu` | 最大传输单元（一次传输的最大字节数） |
| `$modem` | 解调器类型（目前唯一有效值为 HAYES） |
| `$Sport` | 要使用的终端端口 |
| `$speed` | 本地主机与解调器之间的传输速率，单位比特/秒 |

以下是一个 `dip` 脚本：

```
# bugs.dip

top:

# 为连接命名。"ren.stimpy.net"

get $local ren.stimpy.net

# 设置远程 "bunny.net"

# 设置掩码 255.255.255.0

netmask 255.255.255.0

# 定义串口端口和速度。

port config

speed 3840

# 清理解调器（重置）

reset

flush

# 如果你的解调器不正确响应

# 之前的 "reset"，将其注释掉

# 或者将其删除然后

# 取消以下行的注释。

send ATZ

wait OK 3

# 设置解调器的初始化字符串，然后拨号

get $Sim ATQ01!= 557

if $servI1 != 0 goto modem_ERR

connect 60

if $servI1 != 0 goto modem_ERR

# 如果我们到达这里，说明已连接

# ... 登录远程系统

login:

sleep 2

send \r\n\r

wait login: 10

if $servI1 != 0 goto login_ERR

send THE_USERNAME\nsleep 2

wait word: 10

if $servI1 != 0 goto pswrd_ERR

send THE_PASSWORD\n
```

# Linux 内部

```bash
log_success:

# 我们已经登录，现在等待提示符

wait SLEEP 15

if Serv1 != 0 goto prompt_ERR
```

```
# 如果我们到了这里，说明我们已经完成了

# SLIP 连接所需的所有任务

final:

# 设置 SLIP

get set 256

# 确保路由的执行

default:

print CONNECTED SLIP = $rtmip

mode SLIP

goto exit
```

```
prompt_ERR:

print 等待登录提示超时

goto error
```

```
login_ERR:

print 等待登录超时

goto error
```

```
pswd_ERR:

print 等待密码提示超时

goto error
```

```
modem_ERR:

print 调制调调器问题

goto general_ERR
```

```
general_ERR:

print 无法连接到远程系统

quit 1

exit

exit
```
