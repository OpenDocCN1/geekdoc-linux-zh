

# 高级 Bash 脚本编写指南

sz 和 rz 命令集用于通过 zmodem 协议在远程主机之间传输文件。Zmodem 相比 xmodem 具有某些优势，例如更高的传输速率和支持中断传输的恢复。与 sx 和 rx 一样，这些命令通常是通信包的一部分。

# ftp

用于向远程主机上传/下载文件的工具和协议。ftp 会话可以在脚本中实现自动化（参见示例 17–7、示例 A–4 和示例 A–11）。

# cu

调用远程系统并作为简单终端进行连接。这是 telnet 的一种精简版本。

# uucp

UNIX 到 UNIX 拷贝（UNIX to UNIX copy）。这是一个用于在 UNIX 服务器之间传输文件的通信包。使用 shell 脚本处理 uucp 命令序列的有效方法。

自从互联网和电子邮件出现以来，uucp 似乎已经淡出舞台，但在没有互联网连接或不便连接互联网的情况下，它仍然存在并可以完美运行。

# telnet

用于连接远程主机的工具和协议。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_189_0.png)

telnet 协议包含安全漏洞，因此应避免使用。

# rlogin

远程登录，在远程主机上启动会话。此命令存在安全问题，请改用 ssh。

# rsh

远程 shell（Remote shell），在远程主机上执行命令。此存在安全问题，请改用 ssh。

# rcp

远程拷贝（Remote copy），在两个不同的网络机器之间拷贝文件。在脚本中使用具有安全影响的 rcp 及类似工具可能并不明智。相反，请考虑使用 ssh 或 expect 脚本。

# ssh

安全 shell（Secure shell），登录远程主机并在上面执行命令。作为 telnet、login、rcp、rsh 的安全替代方案，它使用身份验证和加密。详情请参其 man 手。

## 12.6. 通信命令

# write

write

这是一个终端与终端之间通信的工具。它允许从你的终端（控制台或 xterm）向另一个用户的终端发送行。当然，可以使用 msg 命令来禁用对终端的写访问。

由于 write 是交互式的，它通常不会在脚本中使用。

# mail

mail

向用户发送电子邮件。

这个精简的命令行邮件客户端可以作为脚本中的命令工作。

## 示例 1–29. 一个给自己发邮件的脚本

```bash
#!/bin/sh
# self-mailer.sh: 自发邮件脚本
ARGCOUNT=1      # 需要收件人姓名。
E_WRONGARGS=6
if [ $# -ne $ARGCOUNT ];
then
  echo "Usage: `basename $0` addressee"
  exit $E_WRONGARGS
fi

cat $0 | mail -s "Script `basename $0` has mailed itself to you." "$1"

# 来自自发邮件脚本的问候。
# 一个调皮的人运行了这个脚本，
# 导致它将自己邮件给了你。
# 显然，有些人时间空闲得没正事做了。
#
exit 0
```

此工具会自动回复那些收件人正在休假且暂时不可用的电子邮件。它在网络上结合 sendmail 运行，不适用于拨号 POP 账户。

## 12.7. 终端控制命令

### 命令列表

### tput

初始化终端并/或从 terminfo 数据中获取信息。各种选项允许某些终端操作。**tput clear** 等同于下方的 **clear**。**tput reset** 等同于下方的 **reset**。

```bash
bash$ tput longterm
xterm terminal emulator (XFree86 4.0 Window System)
```

注意 stty 提供了更强大的命令集来控制终端。

### reset

重置终端参数并清除文本屏幕。与 **clear** 一样，光标和提示符会重新出现在终端的左上角。

### clear

**clear** 命令只需清除控制台或 xterm 中的文本屏幕。提示符和光标重新出现在屏幕或 xterm 窗口的左上角。此命令既可以在命令行中使用，也可以在脚本中使用。参见示例 10–24。

### script

此工具记录（保存到文件）控制台或 xterm 窗口命令行中的所有用户按键。这在实际上创建了一个会话记录。

## 12.8. 数学命令

### 命令列表

### factor

将整数分解为质因数。

```bash
bash$ factor 27417
27417: 3 13 19 37
```

### bc, dc

这些是灵活的任意精度计算工具。

bc 的语法模糊类似于 C 语言。

dc 使用 RPN（逆波兰表示法）。

在两者中，bc 在脚本中似乎更有用。它是一个非常良好的 UNIX 工具，可以在管道中使用。

Bash 无法处理浮点数计算，并且缺乏某些重要数学函数的运算符。幸运的是，bc 出现来救了救场。

这里有一个使用 bc 计算脚本变量的简单模板。它使用了命令替换。

```
variable=$(echo "OPTIONS; OPERATIONS" | bc)
```

