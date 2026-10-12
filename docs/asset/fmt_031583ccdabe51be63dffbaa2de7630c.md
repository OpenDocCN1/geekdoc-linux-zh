
在我们转向输出之前，让我们再看几个包含 `ex` 的示例。在第一个示例中，我们都想要来自 `vivaldi` 的 `either` 或 `or`，但 TCP 头部中没有源为 `22` 的数据包。我们本应从 `bach` `ssh` 登录到 `vivaldi`，我们看到了一半 `ssh` 连接，即发送到端口 `22`（在 `/etc/services` 中是 `ssh`）的流量。我们使用了一个由 `vivaldi` 发出的 DNS 请求。如果你在纳奇，在现实世界中你不会经常使用 `-c`；当你看到它时，你会放弃计数并直接按 `CTRL-C`。它仅用于保持结果缓冲区，即 `-t`，用于抑制时间戳。

```
root@vivaldi: # tcpdump -c 3 vivaldi and not tcp src port 22
tcpdump: listening on eth0
bash.41509 > vivaldi.sh : \
  ack 166184878 win 63712 nop,nop,timestamp 58424771 8438456 (DF) [0x10]
bash.41509 > vivaldi.sh : \
  ack 65 63712 nop,nop,timestamp 5842478 843856 (DF) [0x10]
vivaldi.1026 > * java.domain: 11746+ PTR? 168.198.2-in-addr.arpa (43) (DF)
```

# Silicon—局域网路由器 第 3 章

在这个示例中，我们都想要来自 `vivaldi` 的 `either` 或 `or`，但 TCP 头部中没有源为 `22` 的数据包。我们本应从 `bach` `ssh` 登录到 `vivaldi`，我们看到了一半 `ssh` 连接，即发送到端口 `22`（在 `/etc/services` 中是 `ssh`）的流量。我们使用了一个由 `vivaldi` 发出的 DNS 请求。如果你在纳奇，在现实世界中你不会经常使用 `-c`；当你看到它时，你会放弃计数并直接按 `CTRL-C`。它仅用于保持结果缓冲区，即 `-t`，用于抑制时间戳。

## 3.3 IP 监控工具

- `-td` 不在每行上生成时间戳。

- `-tt` 显示 `32` 位时间戳值而非墙钟时间。（警告——仅在 `2038` 年之前有用！）。

- `-v` 显示更详细的输出，包括 `IP TTL` 和 `TOS` 头部信息。

- `-vv` 显示更详细的输出，当 `tcpdump` 识别该协议时，包含协议信息。

- `-x` 以十六进制形式打印数据包负载，多到由 `-s snaplen` 指定字节数。这是为什么 `tcpdump` 可能被认为比 ASCII 显示数据的其他嗅探器更“礼貌”的原因之一。如果不费力进行解码，你不会在十六进制数据中偶然发现某人的邮件内容或密码。如果你能读懂十六进制格式的 ASCII，那么你该多出门走走。

- `-A` 与 `-x` 结合使用时 `-x` 的更漂亮版本，它同时以十六进制和 ASCII 格式输出，以便在你单手查阅 `RFC` 规范而另一手不想看十六进制转 ASCII 表时使用。

- `-w file` 将输出写入文件。文件将是二进制格式，可以通过指定为 `tcpdump -r` 的输入来解析。这消除了写入终端的开销，因此在繁忙的机器上你可能更倾向于使用 `tcpdump -v` 然后使用 `tcpdump -r`。`tcpdump` 足够聪明，在模式下不会执行主机或服务名查找以进一步提高性能。如果不关闭它们，`-w` 在回读文件时会为你执行。指定 `-` 到标准输出。

如果你不能一次吸收所有这些选项，这里有更多示例说明了你的策略。第一个捕获除 `arp` 和 `ssh`（端口 `22`）之外的所有流量。如果我告诉你 `eth1` 连接到 `192.168.0.24` 子网，你可以从 `drone3` 作为网关的第三个数据包开始嗅探。在第二个示例中，我们将网段上的所有内容捕获到文件中，并使用 `tcpdump` 解析内容，如下：

```
#
### 示例 1
#
drone3: # tcpdump -nxq -i eth1 not arp and port ssh
tcpdump: listening on interface0
21:17:59.369273 192.168.15.103 > 192.168.13.21:230 tcp 0
00000 c0a8 4500 002a 00a4 0006 d512 c0a8 120f E.,M.,....
00010 c0a8 120d 0406 0015 65d6 97f7 0000 0000................g...
00020 c6002 0220 c0a8 0020 05b4 0000....................
21:17:59.369438 192.168.13.21 > 192.168.15.1030: tcp 0
00000 4500 0028 0000 f0fe d662 c0a8 120d E.,(....).....b...
00010 c0a8 120f 0015 0406 0000 0000 67d6 9800................g...
00020 5014 0000 0672 0000 .P.....r....
21:15:48.97152 192.168.1.1 > 192.168.16.55: icmp:192.168.1.1
port 123 unreachable
00000 45d0 0667 0000 00fe b1a4 c7a8 0101 E.hn.........t...
00010 c0a8 1307 0313 83fc 0000 4510 0050 01c4.......7.......E.L
0x0020 0000 3e11 aa08 c0a8 1037 c0a8 0101 ...>.......7...
0x0030 007b 007b 0038 ba2f e3d0 04f0 0000 0000 ..{8.//...
0x0040 0001 59d9 0000 0000 0000 0000 .{.{Y...
0x0050 0000 ..
```

### 示例 2

```
drone3:"# tcpdump -w /tmp/tcpdump.out -i eth1

tcpdump: listening on eth1

~C

1610 packets received by filter

0 packets dropped by kernel

# 现在让我们看看该网段上的 UDP 流量

drone3:"# tcpdump -r /tmp/tcpdump.out -Nq udp

14:48:14.27428 192.168.18.104 > java.domain: udp 37

14:48:14.27637 java.domain > 192.168.18.104: udp 84 (DF)

14:50:02.34053 vivaldi.1026 > java.domain: udp 32 (DF)

14:50:02.417371 java.domain > vivaldi.1026: udp 86 (DF)

14:50:02.42288 vivaldi.1026 > java.domain: udp 32 (DF)

14:50:02.50545 java.domain > vivaldi.1026: udp 394 (DF)

#  http 流量呢？

drone3:"# tcpdump -r /tmp/tcpdump.out -qt port http

192.168.18.104 > bigint.ech.umich.edu: tcp 0 (DF)

bigfoot.ech.umich.edu > 192.168.18.104: tcp 1460 (DF)

bigfoot.ech.umich.edu > 192.168.18.104: tcp 1460 (DF)

192.168.18.104 > bigint.ech.umich.edu: tcp 0 (DF)

bigfoot.ech.umich.edu > 192.168.18.104: tcp 1460 (DF)

bigfoot.ech.umich.edu > 192.168.18.104: tcp 569 (DF)

vivaldi.mancill.van.103 > klecker.debian.org.www: tcp 0 (DF)

klecker.debian.org.www > vivaldi.mancill.van.103: tcp 0 (DF)

(哎 - 太多了)

# http 流量如何？

drone3:"# tcpdump -r /tmp/tcpdump.out -qt port http and

host pandora.debian.org

192.168.18.104 > pandora.debian.org.www: tcp 0 (DF)

pandora.debian.org.www > 192.168.18.104: tcp 0 (DF)

pandora.debian.org.www > 192.168.18.104: tcp 0 (DF)
```
