
![](img/a3584dae761d2e3abed8bf40d7637389_361_0.png)

> **注意**
>
> 别忘了在上一行末尾添加 `\`，以便 chat 仍然认为整个行脚本是在一行中。

不幸的是，一些服务器会产生非常多变的提示符。你可能需要使用 *minicom* 登录几次以了解发生了什么，并挑选稳定的 *期望* 字符串。

### 用于 PAP/CHAP 认证连接的 Chat 脚本

如果你的 ISP 使用 PAP/CHAP，那么你的 chat 脚本要简单得多。你的 chat 脚本所需要做的只是拨号，等待连接，然后让 `pppd` 处理登录。

```
#!/bin/sh

#
###### This is part 2 of the ppp-on script. It will perform the
###### connection protocol for the desired connection.
#
exec /usr/sbin/chat -v
TIMEOUT         3
ABORT	'\nBUSY\r'
ABORT	'\nNO ANSWER\r'
ABORT	'\nRINGING\r\n\n\nRINGING\r'
"\n\n\n\nPAT" 'OK\n++\n\c-OK'	ATHO
TIMEOUT	30
OK	ATDT$TELEPHONE
CONNECT	''
```

### pppd 的 debug 和 file 选项

正如我们已经看到的，你可以使用 `pppd` 的 `-d` 选项开启调试信息日志记录。`debug` 选项与此等效。

由于我们正使用新脚本建立新连接，暂时保留 `debug` 选项。

**警告**

如果你的磁盘空间紧张，记录 `pppd` 交换可能会迅速扩大你的 syslog 文件并给你造成麻烦（但要做到这一点，你必须连接失败并持续尝试好几分钟）。

一旦你确信一切正常工作，你就可以移除此选项。

如果你的 PPP 选项文件名不是 `/etc/ppp/options` 或 `/etc/ppp/options.ttySx`，请使用 `pppd` 的 `file` 选项指定文件名——例如：

```
exec /usr/sbin/pppd debug file options.myserver /dev/ttyS0 38400
```

### 测试你的连接脚本

打开一个新的 root Xterm（如果你在 X 环境下）或打开一个新的虚拟控制台并以 root 身份登录。

在这个新会话中，发出命令：

```
tail -f /var/log/messages
```

（或者你的系统日志文件）。

在第一个窗口（或虚拟控制台）中发出命令：

```
ppp-on
```

（或者你编辑后的 `/usr/sbin/ppp-on` 版本的名字）。如果你不在命令末尾指定 `&` 将脚本放入后台，你将无法取回终端提示符，直到 PPP 退出（当链接终止时）。

现在切回到跟踪系统日志的窗口。

你会看到类似以下内容（前提是你给 `chat` 指定了 `-v` 并且给 `pppd` 指定了 `-d`）这是 `chat` 脚本和响应被记录到系统日志文件中，接着是 `pppd` 的启动信息：

```
Oct 21 16:09:58 hwlin chat[98668]: abort on (NO CARRIER)
Oct 21 16:09:59 hwlin chat[98668]: abort on (BUSY)
Oct 21 16:09:59 hwlin chat[98668]: send (ATZ\*M)
Oct 21 16:09:59 hwlin chat[98668]: expect (OK)
Oct 21 16:10:00 hwlin chat[98668]: ATZ\*\*M
Oct 21 16:10:00 hwlin chat[98668]: OK -- got it
Oct 21 16:10:00 hwlin chat[98668]: send (ATDT722298\*M)
Oct 21 16:10:00 hwlin chat[98668]: expect (CONNECT)
Oct 21 16:10:22 hwlin chat[98668]: \*M
Oct 21 16:10:22 hwlin chat[98668]: ATDT722298\*\*M
Oct 21 16:10:22 hwlin chat[98668]: CONNECT -- got it
Oct 21 16:10:22 hwlin chat[98668]: send (\*M)
Oct 21 16:10:22 hwlin chat[98668]: expect (login)
Oct 21 16:10:23 hwlin chat[98668]: kepler login: -- got it
Oct 21 16:10:23 hwlin chat[98668]: send (harrt\*M)
Oct 21 16:10:23 hwlin chat[98668]: expect (ssword:)
Oct 21 16:10:23 hwlin chat[98668]: harrt\*M
Oct 21 16:10:23 hwlin chat[98668]: Password: -- got it
Oct 21 16:10:23 hwlin chat[98668]: send (?????\*M)
Oct 21 16:10:23 hwlin chat[98668]: expect (harrt)
Oct 21 16:10:24 hwlin chat[98668]: [harrt -- got it
Oct 21 16:10:24 hwlin chat[98668]: send (ppp\*M)
Oct 21 16:10:27 hwlin pppd[98723]: pppd 2.1.2 started by root, uid 0
Oct 21 16:10:27 hwlin pppd[98723]: Using interface ppp0
Oct 21 16:10:27 hwlin pppd[98723]: Connect: ppp0 <>->/dev/cua1
Oct 21 16:10:27 hwlin pppd[98723]: fsm_sdslat(LCP): Sent code 1, id 1.
Oct 21 16:10:27 hwlin pppd[98723]: LCP, sending Configure-Request, id 1
Oct 21 16:10:27 hwlin pppd[98723]: fsm_rconfigure(LCP): Rcvd id 1.
Oct 21 16:10:27 hwlin pppd[98723]: lcp_reqci: rcvd MRU (1500) (ACK)
Oct 21 16:10:27 hwlin pppd[98723]: lcp_reqci: rcvd ASYNCMAP (0) (ACK)
Oct 21 16:10:27 hwlin pppd[98723]: lcp_reqci: rcvd MAGICNUMBER (a098B898) (ACK)
```

##### 10 月 21 日 16:10:27 hwfin pppd[19873]:

lcp-reqi: rcvd PCONPRESSION

(ACK)

lcp-reqi: rcvd ACOMPRESSSION

(ACK)

lcp-reqi: returning CONFACK.

fsm-data(IPCP): Sent code 2, id 1.

fsm_rconfack(LCP): Rcvd id 1.

fsm_rconfreq(IPCP): Sent code 1, id 1.

IPCP: sending Configure-Request, id 1

IPCP: Rcvd id 1.

1CP: received ADDR

(10.144.153.51)

(ACK)

IPCP: received COMPRESSTYPE

(45)

(ACK)

IPCP: returning Configure-ACK

fsm-data(IPCP): Sent code 2, id 1.

fsm-sdata(IPCP): Sent code 1, id 1.

IPCP: sending Configure-Request, id 1

fsm_rconfreq(IPCP): Rcvd id 255.

IPCP: received ADDR

(10.144.153.51)

(ACK)

IPCP: received COMPRESSTYPE

(45)

(ACK)

IPCP: returning Configure-ACK

fsm-sdata(IPCP): Sent code 2, id 255.

fsm_rconfupck(IPCP): Rcvd id 1.

IPCP: up

local IP address 10.144.153.104

remote IP address 10.144.153.51
