
```bash
#!/bin/sh
#
###### This is part 2 of the ppp-on script. It will perform the
###### connection protocol for the desired connection.
#
/usr/sbin/chat -v
    TIMEOUT     3
    ABORT       '\nBUSY\r'
    ABORT       '\nNO ANSWER\r'
    ABORT       '\nrINGING\r\n\nrRINGING\r'
    ABORT       '\r'
    '\rAT'
    'OK-\+c0:'  'ATH0'
    TIMEOUT     30
    OK          'ATDT$TELEPHONE'
    CONNECT     ''
    login:--     $ACCOUNT
    asword:--    $PASSWORD
```

对于 `PPP-2.2`，`ppp-off` 脚本看起来像这样：

```bash
#!/bin/sh
#####################################################################
#
##### Determine the device to be terminated.
if [ "$1" = "" ]; then
    DEVICE=ppp0
else
    DEVICE=$1
fi
#####################################################################
#
##### If the ppp0 pid file is present then the program is running.
##### Stop it.
if [ -r /var/run/$DEVICE.pid ]; then
	kill -INT `cat /var/run/$DEVICE.pid`
##### If the kill did not work then there is no process running for
##### this pid. It may also mean that the lock file will be left. You
##### may wish to delete the lock file at the same time.
	if [ ! "$?" = "0" ]; then
		rm -f /var/run/$DEVICE.pid
		echo "ERROR: Removed stale pid file"
		exit 1
	fi
fi
##### Success. Let pppd clean up its own junk.
	echo "PPP link to $DEVICE terminated."
	exit 0
fi
##### The ppp process is not running for ppp0
echo "ERROR: PPP link is not active on $DEVICE"
exit 1
```

## 编辑提供的 PPP 启动脚本

由于新脚本分为两部分，我们将依次编辑它们。

### `ppp-on` 脚本

你需要编辑脚本以反映你在 ISP 的*用户名*、你在 ISP 的*密码*以及你 ISP 的电话号码。

诸如 `TELEPHONE=` 这样的每一行实际上都设置了 shell 变量，其中包含“=”右边的信息（当然不包括注释）。因此，编辑这些行中的每一行，使其适用于你的 ISP 和连接。

此外，由于你在 `/etc/ppp/options` 文件中设置 IP 号（如果需要），请*删除*说明如下的一行：

`LOCAL_IP=$REMOTE_IP \`

此外，确保 shell 变量 `DIALERSCRIPT` 指向你实际要使用的拨号脚本的完整路径和名称。因此，*如果*你移动或重命名了该脚本，请确保在 `ppp-on` 脚本中正确编辑此行！

### `ppp-on-dialer` 脚本

这是实际建立我们 PPP 链接的脚本中的第二个。

![](img/a3584dae761d2e3abed8bf40d7637389_359_0.png)

**注意**

Chat 脚本通常都是单行写的；反斜杠用于允许跨多个物理行进行续行（为了便于人类阅读），它们不属于脚本本身的一部分。但是，详细查看它非常有用，这样我们才能理解它实际上（应该）在做什么！

#### 什么是 Chat 脚本

Chat 脚本是一系列 *期望字符串 发送字符串* 的配对。特别注意，我们在发送任何内容之前*总是期望某些东西*。

如果我们希望在*未*先接收任何内容的情况下发送某些内容，我们必须使用一个空的 *期望* 字符串（用 `""` 表示）；同样地，如果我们希望在不发送任何内容的情况下期望某些东西！此外，如果字符串包含多个单词（例如 NO CARRIER），你必须给字符串加上引号，以便 `chat` 将其视为一个单一实体。

我们模板中的 `chat` 行是：

```
exec /usr/sbin/chat -v
```

调用 `chat`，`-v` 告诉 `chat` 将*所有*输入/输出复制到系统日志中（通常是 `/var/log/messages`）。一旦你确信 `chat` 脚本能可靠工作，请编辑该行以移除 `-v`，从而避免在 syslog 中产生不必要的杂乱信息。

```
TIMEOUT 3
```

这将接收预期输入的超时时间设置为三秒。如果你使用的是速度极慢的调制解调器，可能需要将此值增加到五秒或十秒！

```
ABORT '\nBUSY\r'
```

如果接收到 *BUSY* 字符串，则中止操作。

```
ABORT '\nNO ANSWER\r'
```

如果接收到 *NO ANSWER* 字符串，则中止操作。

```
ABORT '\nRINGING\r\n\r\n\nRINGING\r'
```

如果接收到（重复的）*RINGING* 字符串，则中止操作。这是因为有人在拨打你的电话线！

```
""\rAT"
```

从调制解调器处不期望任何内容，并发送字符串 `AT`。

```
OK---+++\c--OK ATH0
```

这一行稍微复杂一些，因为它使用了一些 `chat` 的错误恢复功能。

它的含义是... 期望 `OK`；如果没有接收到（因为调制解调器不在命令模式下），则发送 `+++`（这是标准的兼容 Hayes 的调制解调器字符串，用于将调制解调器返回到命令模式），并期望 `OK`。然后发送 `ATH0`（调制解调器的挂断字符串）。这使得你的脚本能够应对调制解调器卡在在线状态的情况。

```
TIMEOUT        30
```

将脚本剩余部分的超时时间设置为 30 秒。如果你遇到 `chat` 脚本因超时而中止的问题，请将其增加到 45 秒或更多。

```
OK             ATDT$TELEPHONE
```

期望 `OK`（这是调制解调器对 `ATH0` 命令的响应）并拨打我们要呼叫的号码。

```
CONNECT
```

期望 `CONNECT`（我们的调制解调器在远程调制解调器应答时发送）并不回复任何内容。

```
login::--login:    $ACCOUNT
```

同样，这里也内置了一些错误恢复功能。期望登录提示符（`...login:`），但如果未在超时前接收到，则发送一个回车并再次查找登录提示符。当接收到提示符时，发送用户名（存储在 shell 变量 `ACCOUNT` 中）。

```
assord:        $PASSWORD
```

期望密码提示符并发送我们的密码（同样，存储在 shell 变量中）。

这个 `chat` 脚本具有合理的错误恢复能力。`Chat` 具有比这里展示的更多功能。更多信息请参阅 `chat` 手册页（`man 8 chat`）。

#### 在服务器端启动 PPP

虽然 `ppp-on-dialer` 脚本对于在登录后自动在服务器端启动 `pppd` 的服务器来说没问题，但有些服务器要求你明确地在服务器上启动 PPP。

如果你需要发出一个命令来启动服务器上的 PPP，*确实*需要编辑 `ppp-on-dialer` 脚本。

在脚本的末尾（在密码行之后）添加额外的 *期望 发送* 配对——这一对将查找你的登录提示符（注意在 Bourne shell 中具有特殊含义的字符——例如 `[` 和 `]`（左方括号和右方括号））。

一旦找到 shell 提示符，`chat` 必须发出你的 ISP PPP 服务器所需的**PPP 启动**命令。

在我的情况下，我的 PPP 服务器使用标准的 Linux Bash 提示符 `[harrt@kepler harrt]$`，并且需要我输入

`ppp`

来启动服务器上的 PPP。

在这里允许一点错误恢复是个好主意，所以在我的情况下我使用 `harrt--harrt    ppp` 这表示，如果我们在超时前未接收到提示符，则发送一个回车并再次查找提示符。

一旦接收到提示符，则发送字符串 *ppp*。
