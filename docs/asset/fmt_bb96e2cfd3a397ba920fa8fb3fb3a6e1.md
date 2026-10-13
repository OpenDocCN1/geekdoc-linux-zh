
`root@main: rpm -q sendmail`

接下来，检查 Sendmail 是否运行。以下输出显示了 Sendmail 已安装以及其版本：

```bash
root@main: ps -au | grep sendmail
```

如果 Sendmail 没有运行，你可以通过以下命令启动它：

```bash
root@main: service sendmail
```

### 配置 Sendmail

许多系统管理员认为 Sendmail 很难配置。幸运的是，Red Hat 提供了适用于大多数站点的默认配置。在所有情况下，你都需要 `/usr/lib/sendmail` 中的预定义配置文件。基本流程是根据你的需求修改预定义配置文件，使用 `m` 宏处理器（见下节）重新生成 `/etc/sendmail.cf`，测试你的配置。这种方法允许你进行增量更改，最大限度地减少出现重大问题的风险。

列表 13-1：示例中继配置

|############################|
|#### |
| SENDMAIL 配置文件 |
|#### |
|############################|

# # 智能中继主机（可能为空）
更改此行以定义邮件中继机的名称（负责发送/接收互联网邮件的网关计算机）。注意无空格！

`DSmailrelay.tacttechnology.com`

### m 宏处理器

`宏` 是长字符串的符号名称，就像键盘是输入长系列按键的快捷方式一样。Sendmail 的规则来自 Sendmail 宏文件的条目。宏文件中的规则生成了默认的 Sendmail 配置 `sendmail.cf`。`m4` 是一个宏处理器，它读取宏文件并生成配置文件。如果你想在复杂的配置中使用你自定义的规则，可以保持宏文件和宏处理器不变。

## 第四部分：配置您的企业 Linux 互联网服务

`/etc/` 下的一个宏示例是用于命名操作系统的 `OTYPE` 宏。记住，Sendmail 运行在许多不同的操作系统上，而不仅仅是 Unix 和 Linux。在 Linux 系统上，如果你查看 Sendmail 的宏文件，你会看到下面这一行，它告诉 Sendmail 运行的是哪种操作系统：

在企业 Linux 上，`OTYPE` 宏是预定义的，因此你不需要担心它。

如果你真的想获取有关宏文件及其工作原理的完整技术信息，请阅读 `/usr/lib/sendmail-cf/README` 文件。

![](img/64d26e5c3406fc66f2dd833f0d7cc3af_231_0.png)

# 管理邮件队列

有时电子邮件无法立即发送，原因有很多种。也许是你的网络断了。也许是接收者的连接不可用。无论原因如何，用户都可以继续使用他们的 MUA 编写邮件。当他们发送邮件时，Sendmail 将消息放入邮件队列，并让 Sendmail 守护进程定期尝试发送该消息。你可以通过检查启动 Sendmail 的初始化脚本来确定这些间隔。

以下节选自文件 `/etc/rc.d/rc2.S80sendmail`。第一行将重试间隔定义为一小时（`1h`）。你可以用 `h`（小时）、`m`（分钟）或 `s`（秒）来指定间隔。这个 Red Hat 版本使用了变量 `QUEUE` 并将其设置为 `1h`。某些分发版将间隔硬编码在 Sendmail 命令中（`sendmail -q1h`）。列表 13-2 的最后两行显示了 Sendmail 的启动命令。最后一行行的 `-qQUEUE` 将重试时间设置为一小时。它倒数第二行的 `-bd` 选项将 Sendmail 导出为守护进程。

```
Listing 13-2: /etc/rc.d/rc2.S80sendmail 节
QUEUE=1h

fi

# 检查网络是否正常。
$ [ ($NETWORKING) = "no" ] && exit 0

[ -f /usr/sbin/sendmail ] || exit 0

RETVAL=0

start() (
```

# 第 13 章：配置和管理电子邮件服务器

```
# 守护进程。
echo -n "Starting sendmail: *"
/usr/bin/newaliases > /dev/null 2>&1

for i in virtuasable access domaintable mailertable; do
  if [ -f /etc/mail/$i ]; then
    makemap hash /etc/mail/$i < /etc/mail/$i
  fi
done

/usr/sbin/sendmail $[ [[ "$DAEMON" = yes ]] && echo -bd ] \ \
$[ -n "$QUEUE" ] && echo -q$QUEUE ]
```

# 配置 POP3

设置 POP3 涉及步骤包括：

1. 安装包含 POP3 守护进程的包。
2. 编辑文件 `/etc/xinetd.d/pop3` 使 POP3 服务可用。要编辑此文件，请使用你喜欢的文本编辑器更改该行：
   ```
   disable = yes
   disable = no
   ```
3. 在命令行提示符处输入以下命令重启 xinetd 守护进程，使步骤 2 中的更改生效：
   ```
   Service xinetd restart
   ```
4. 检查 POP3 守护进程是否接受连接。你可以 `telnet` 到你自己的计算机的 `110` 端口（所示），以查看 POP3 是否接受连接：

```
terry@main# telnet localhost 110
Trying 127.0.0.1...
telnet:Connected to localhost.
Esc character is '*'
* OK POP3 localhost v76.64 server ready
```

你的企业 Linux 操作系统安装程序可能已经为你设置了 POP3。在启动 POP3 之前，你应该使用你喜欢的包管理器查询 POP3 是否已经安装。

Red 将 IMAP4 和 POP3 软件捆在一起。当你查询 RPM 数据库获取 POP3 时，你需要在 IMAP 名称下查找它：

```
root@main# rpm -q imap
```

![](img/64d26e5c3406fc66f2dd833f0d7cc3af_232_0.png)

# 第四部分：配置您的企业 Linux 互联网服务

# 配置 IMAP4

要配置 IMAP4，你遵循与 POP3 相同的步骤步骤：

1. 安装包含 IMAP4 守护进程的包。
2. 编辑文件 `/etc/xinetd.d/imapconf` 使 IMAP4 服务可用。对于此文件，使用你喜欢的文本编辑器更改该行：
   ```
   disable = yes
   ```
3. 在命令行提示符处输入以下命令重启 xinetd 守护进程，使步骤 2 中的更改生效：
   ```
   Service xinetd restart
   ```
4. 检查 IMAP 守护进程是否接受连接。你可以 `telnet` 到你自己的计算机的 `143` 端口（所示），以查看 IMAP4 是否接受连接：

```
try@main# telnet localhost 143
trying 127.0.0.1...
telnet:Connected to localhost.
esc character is '.'.
OK localhost IMAP4rev1 v1.26 server ready
```

你的企业 Linux 操作系统安装程序可能已经为你设置了 POP3。在启动 POP3 之前，你应该使用你喜欢的包管理器查询 POP3 是否已经安装。

Red 将 IMAP4 和 POP3 软件捆在一起。当你查询 RPM 数据库获取 POP3 时，你需要在 IMAP 名称下查找它：

```
root@main# rpm -q imap
```

要配置 IMAP4，你遵循与 POP3 相同的步骤：

1. 安装包含 IMAP4 守护进程的包。
2. 编辑文件 `/etc/xinetd.d/imapconf` 使 IMAP4 服务可用。对于此文件，使用你喜欢的文本编辑器更改该行：
   ```
   disable = yes
   ```
3. 在命令行提示符处输入以下命令重启 xinetd 守护进程，使步骤 2 中的更改生效：
   ```
   Service xinetd restart
   ```
4. 检查 IMAP 守护进程是否接受连接。你可以 `telnet` 到你自己的计算机的 `143` 端口（所示），以查看 IMAP4 是否接受连接：
```
try@main# telnet localhost 143
trying 127.0.0.1...
telnet:Connected to localhost.
esc character is '.'.
OK localhost IMAP4rev1 v1.26 server ready
```
