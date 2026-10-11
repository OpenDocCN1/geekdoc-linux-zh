
# 查看 `/usr/share/doc/sendmail/README.cf` 以获取关于此文件格式的描述（在该文件中搜索 `access_db`）

`/usr/share/doc/sendmail/README.cf` 是 `sendmail-doc` 软件包的一部分。

`#n#` 默认情况下，我们允许从 `localhost` 进行中继：

`localhost.localdomain` `RELAY`
`localhost` `RELAY`
`127.0.0.1` `RELAY`

`#n#` 想要拦截的发送者

`evilmailer@yahoo.com` `REJECT`
`stimpy.glaci.com` `DISCARD`
`cyberpromo.com` `DISCARD`
`199.170.196` `ERROR:*550 The Spam Scum!\n`

```
# 226 196 第二部分 ♦ 运行控制

# 查看 /usr/share/doc/sendmail/README.cf 以获取关于
# 此文件格式的描述（在该文件中搜索 access_db）
# /usr/share/doc/sendmail/README.cf 是 sendmail-doc
## 软件包的一部分。
#n# 默认情况下，我们允许从 localhost 进行中继：
localhost.localdomain RELAY
localhost RELAY
127.0.0.1 RELAY
#n# 想要拦截的发送者
## evilmailer@yahoo.com REJECT
stimpy.glaci.com DISCARD
cyberpromo.com DISCARD
199.170.196 ERROR:*550 The Spam Scum!\n
```

## 烟雾攻击放大攻击 (Smurfing Amplification Attack)

该攻击利用 `ICMP` 协议，这是一个用于检查网络连接速度和可用性的服务。使用 `ping` 命令，你可以从你的计算机向另一台计算机发送数据包。远程计算机确认该数据包为 `ICMP` 请求，并向你的计算机回显响应数据包，你的计算机可以打印出消息，显示系统已在线并告诉你回复花费了多长时间。

烟雾攻击（`smurfing attack`）利用恶意（`malformed`）的 `ICMP` 请求来通过网络流量淹没你的计算机。攻击者将 `ping` 请求重放给一个无辜的第三方，方式使得复制的数据包被放大了几十倍甚至上百倍。使用一个拥有快速连接和大量计算机的机构作为中继。`ping` 的目标地址被设置为一个子网而不是单个主机。返回地址被伪造为你的机器地址，而不是真实的发送者。当 `ICMP` 数据包到达无辜的中继网络时，该网络上的每个主机都会回复 `ping`！它们回复的是你的计算机，而不是真实的发送者。如果中继机构拥有数百台计算机，你的 Internet 连接可能会迅速被淹没。最好的修复方法是配置被用作中继的机构，告知其滥用行为。该机构通常需要重新配置其路由器以阻止未来的攻击。如果该机构不配合，你可以通过在路由器上拦截 `ICMP` 协议来减少攻击的影响，这至少可以防止流量进入你的内部网络。即使你说服了 `ISP` 在你的网络处拦截 `ICMP` 数据包，这也有帮助。

# 227 第 6 章 Linux 安全防护 197

通过将发送者添加到 `/etc/mail/access` 并使用关键字 `RELAY`，你可以允许特定的主机或域名通过你的系统中继邮件。默认情况下，只允许从主机中继。更多信息请参阅 `sendmail` 文档。

> 你可能考虑使用 `spamassin` 包来过滤服务器的垃圾邮件，它会检查传入邮件的文本，并尝试过滤掉它判定为垃圾邮件的消息。`spamassin` 在第 24 章中有描述。

## 防御分布式拒绝服务攻击 (DDoS)

`DDoS` 攻击难以发起得多，且几乎无法停止。它始于渗透数百或数千台安全防护薄弱的机器。然后根据攻击者的意图，将这些机器指向单一主机。

## 198 第二部分 ♦ 运行 DSL

随着 `DSL` 和电缆调制解调器的出现，数以百万计的人正在几乎没有速度限制的情况下享受互联网访问服务。在急于上线的过程中，许多人甚至忽视了最基本的安全。由于这些人中的绝大多数运行的是微软操作系统，他们往往很快就会遭受病毒攻击。直到最近，微软系统的常见做法是让许多服务对网络开放，而这些服务并未意识到这一点，也不强调使用防火墙功能来阻止入侵者。

一旦机器被入侵，蠕虫或病毒通常会在受害者的机器上安装一个程序，指令其“拨号”并宣布它现在已准备好为主者效力。根据主者的意愿，这些被感染的机器现在可以用来向选定的主机发送大量的垃圾数据流。与其他成千上万台受感染机器配合，攻击者有能力击垮互联网上的任何网站。

检测 `DDoS` 与检测 `DoS` 攻击类似。可能会出现以下一个或多个迹：

- 持续饱和的数据链路
- 非峰值期间链路饱和度没有降低
- 数百甚至数千个并发网络连接
- 系统性能极慢

`ping` 外部主机可以告诉你许多关于数据链路饱和的信息：比通常高得多的延迟是一个明显的信号。正常的 `ping` 延迟（即从远程主机返回 `ping` 响应所需）看起来如下：

```
## ping www.example.com

PING www.example.com (192.0.34.166) from 10.0.0.11: 56(84) bytes of data

64 bytes from 192.0.34.166: icmp_seq=1 ttl=40.0 ms

64 bytes from 192.0.34.166: icmp_seq=2 ttl=42.5 ms

64 bytes from 192.0.34.166: icmp_seq=3 ttl=39.5 ms

64 bytes from 192.0.34.166: icmp_seq=4 ttl=38.4 ms

64 bytes from 192.0.34.166: icmp_seq=5 ttl=39.0 ms
```

```
www.example.com ping statistics ---

5 packets transmitted, 5 received, 0% loss, time 4035ms

r min/avg/max/mdev = 38.472/39.971/42.584/1.432 ms
```

在这个示例中，`ping` 的往返平均时间大约是三万分之一秒。

对几乎饱和的链路进行 `ping` 看起来如下：

## 第6 章 - 加固 Linux 199

```
## ping www.example.com

PING www.example.com (192.0.34.166): from 10.0.0.11: 56(84) bytes of data

64 bytes from 192.0.34.166: icmp_seq=1 ttl=62 time=122 ms

64 bytes from 192.0.34.166: icmp_seq=2 ttl=62 time=1218 ms

64 bytes from 192.0.34.166: icmp_seq=3 ttl=62 time=1290 ms

64 bytes from 192.0.34.166: icmp_seq=4 ttl=62 time=1288 ms

64 bytes from 192.0.34.166: icmp_seq=5 ttl=62 time=1241 ms

---

www.example.com ping statistics

6 packets transmitted, 5 received, 0% loss, 5032ms

r min/avg/mdev = 1218.059/1258.384/1280.00 ms
```

从第一个示例到第二个示例，延迟增加了 31 倍！数据链路从正常变为变慢 31 倍，这是链路利用率可能需要调查的显而迹象。

为了更准确地测量数据吞吐量，可以使用如 `ttcp` 等工具。要使用 `ttcp` 测试你的连接，你必须在网络内外都安装 `ttcp` 包。如果你不确定是否安装了该包，只需在命令提示符中输入 `ttcp`。你应该看到类似以下的内容：

```
@ ttcp

Usage: ttcp -t [-options] host [<in>]

Common options:

-i length of read or written to network (default 8192)

-u use UDP instead of TCP

-p port number to send or listen to (default 5001)

-s discard all data from network

-A align the start of buffers to this (default 16384)

-r start these buffers at offset (default 0)

-v print more statistics

-b set buffer size (if supported)

-x format for rate: k=kilobytes; m=mega; g=giga
```
