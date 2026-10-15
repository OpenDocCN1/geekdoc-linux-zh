

你可以使用 `no -a` 来查看所有可用变量的列表——目前有超过 125 个。表 14.14 列出了其中一些具有安全影响的变量。

## 表 14.14 AIX 的安全相关 TCP/IP 调优变量

| Variable | Meaning | Default |
|---|---|---|
| bcastping | Respond to broadcast pings | 0 |
| directed_broadcast | Allow forwarding of broadcast packets | 0 |
| ipforwarding | Allow IP forwarding | 0 |
| ipignoreredirects | Ignore ICMP redirects | 0<sup>a</sup> |
| ipsrcrouteforward | Forward source-routed IP packets | 1<sup>a</sup> |
| ipsrcrouterecv | Accept source-routed IP packets | 0 |
| ipsrcroutesend | Block sending of source-routed packets | 1 |

a. Probably advisable to change

要设置一个变量，请使用

```
no -p -o variable=value
```

例如，要阻止 TCP/IP 协议栈转发源路由数据包，你可以使用命令

```
aix$ sudo no -p -o ipsrcrouteforward=0
```

`-p` 选项使更改在立即生效并在重启后仍然有效。

## 14.16 推荐阅读

- STEVENS, W. RICHARD. *TCP/IP Illustrated, Volume One: The Protocols*. Reading, MA: Addison-Wesley, 1994.

- WRIGHT, GARY R., AND W. RICHARD STEVENS. *TCP/IP Illustrated, Volume Two: The Implementation*. Reading, MA: Addison-Wesley, 1995.

这两本书是对 TCP/IP 协议栈的优秀且全面的指南。有些年代久远，但依然扎实。

- STEVENS, W. RICHARD. *UNIX Network Programming*. Upper Saddle River, NJ: Prentice Hall, 1990.

- STEVENS, W. RICHARD, BILL FENNER, AND ANDREW M. RUDOFF. *UNIX Network Programming, Volume 1, The Sockets Networking API* (3rd Edition). Upper Saddle River, NJ: Addison-Wesley, 2003.

- STEVENS, W. RICHARD. *UNIX Network Programming, Volume 2: Interprocess Communications* (2nd Edition). Upper Saddle River, NJ: Addison-Wesley, 1999.

这些书籍是涉及编程的网络课程中的学生圣经。如果你只需要 Berkeley sockets 接口，原版仍然是一个很好的参考。如果还需要 STREAMS 接口，那么包含 IPv6 的第三版是不错的选择。全部三本都以典型的 Rich Stevens 风格清晰地写成。

- TANENBAUM, ANDREW. *Computer Networks* (4th Edition). Upper Saddle River, NJ: Prentice Hall PTR, 2003.

这是第一本网络教材，至今仍是经典。它包含了协议栈物理层和链路层发生的各种细枝末节的详尽描述。最新版包括对无线网络、千兆以太网、点对点网络、IP 语音等的覆盖。

- SALUS, PETER H. *Casting the Net: From ARPANET to Internet and Beyond*. Reading, MA: Addison-Wesley Professional, 1995.

这是一部关于 ARPANET 发展成为互联网的美丽历史，由一位长期与 UNIX 人们交往、足以听起来像他们中的一员的历史学家撰写！

- COMER, DOUGLAS. *Internetworking with TCP/IP Volume 1: Principles, Protocols, and Architectures* (5th Edition). Upper Saddle River, NJ: Prentice Hall, 2006.

Doug Comer 的 *Internetworking with TCP/IP* 系列很长一段时间以来都是 TCP/IP 协议的标准参考书。这些书籍设计为本科教材，是背景资料的良好入门来源。

- HUNT, CRAIG. *TCP/IP Network Administration* (3rd Edition). Sebastopol, CA: O'Reilly Media, 2002.

像 nutshell 系列中的其他书籍一样，这本书面向 UNIX 系统管理员。书的一半内容是关于 TCP/IP，其余部分涉及电子邮件和远程登录等更高层的 UNIX 设施。

- FARREL, ADRIAN. *The Internet and Its Protocols: A Comparative Approach*. San Francisco, CA: Morgan Kaufmann Publishers, 2004.

- KOZIERAK, CHARLES M. *The TCP/IP Guide: A Comprehensive, Illustrated Internet Protocols Reference*. San Francisco, CA: No Starch Press, 2005.

关于互联网历史及其各种技术的优秀文档集合可以在 isoc.org/internet/history 找到。

## 14.17 练习

E14.1 如何通过监听（即遵守）ICMP 重定向允许未经授权的用户破坏网络？

E14.2 网络链路的 MTU 是什么？如果给定链路的 MTU 设置过高会发生什么？过低呢？

