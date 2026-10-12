
Once the handshake has been established, all packets in this particular session between client and server will use sequence numbers to make sure they stay in order. However, from now on, these packets will be incremented by the size of the data frame being transmitted, rather than by one. (To learn more about how TCP packets stay organized, have a look at `RFC 793`.)

# HTTP Request and Transmission

Once the communication session has been established, it's time for the actual request and transmission of the web page you are trying to view. This involves both `HTTP` and `TCP`.

The process begins in packet 4, our first `HTTP` packet, which asks the server to transmit the web page to the client. Go ahead and expand the section of this packet in the Packet Details pane to view the protocol-specific information related to it (as shown in Figure 6-7).

```
GET /download.html HTTP/1.1
Request Method: GET
Request URI: /download.html
Host: www.ereal.com
User-agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) Gecko/20101011 Firefox/114.0
Accept: text/xml,application/xml,text/html;q=0.9,text/plain,image/*
Accept-Language: en,q=0.5
Accept-Charset: ISO-8859-1,utf-8;q=0.7
Keep-alive: 300
connection: keep-alive
Refer: http://www.ereal.com/development.html
```

Figure 6-7: The Packet Details pane shows all you would want to know about the request.

As you can see, this packet invokes a `GET` command (Request Method: `GET`) for the web page `/download.html` on the domain `www.ereal.com`. (Request URI: `/download.html` and Host: `www.ereal.com`). You will also notice other information that may be useful, as character encoding (Accept-Charset: `ISO-8859-1`), and the referrer (Referrer: `http://www.ereal.com/development.html`).

Once `HTTP` has made this initial `GET` request, `TCP` takes over the data transfer. Throughout the capture you will see this repeated `HTTP` request from the server, and the server will use `TCP` to transmit this data back.

# SYN 数据包

要开始握手过程，客户端向服务器发送一个 `SYN` 数据包；该数据包表示要与服务器建立同步，这确保了客户端和服务器的通信按正确的顺序进行。`SYN` 数据包包含一个 32 位的序列号，位于 `TCP` 数据包的头部中。

要查看数据包的 `TCP` 信息（包括其序列号），请展开 Wireshark “数据包详情（Packet Details）”下的栏目。（你将会引用此部分，因为它包含了各种有用信息，包括源端口和目的端口、序列号、数据包类型以及其他 `TCP` 特定的选项。）在捕获文件中，第一个 `SYN` 数据包的序列号为 0，如图 6-6 所示。

Frame 1 (线路上 64 字节，82 字节)

Ethernet II, Src: 00:00:00:00:01:00, Dst: ff:ff:ff:ff:ff:ff (ff:ff:ff:ff:ff:ff)

Internet Protocol V4, Src: 145.254.160.237, Dst: 65.208.208.223 (65.208.208.223)

Transmission Control Protocol (372), Src Port: 3372 (3372), Dst Port: http (80), Seq: 0, Len: 0

Source port: 3372 (3372)

Destination port: http (80)

Sequence number: 0 (相对序列号)

header length: 28 bytes

window size: 8760

checksum: [correct]

options: (8 bytes)

Maximum segment size: 1460 bytes

NOP

NOP

ACK permitted

图 6-6: 数据包详情提供了你关于此数据包所需的所有信息。

> 在 Wireshark 中，`TCP` 序列号默认被处理为“相对”句号。Wireshark 会调整通信流中的第一个序列号，使其变为 0 而不是其真实值。这样做使得序列号更容易追踪。

# SYN/ACK，服务器的响应

握手过程的下一步是服务器的响应。一旦服务器收到来自客户端的初始 `SYN` 数据包，它会读取该数据包的序列号，并在返回的数据包中使用该数字。响应被称为 `SYN/ACK` 数据包，在示例文件的第 2 个数据包可以看到。

数据包的 `ACK` 部分确认了 `SYN` 数据包——换句话说，它告诉计算机服务器已收到了 `SYN` 数据包。它通过将原始 `SYN` 数据包中发送的序列号加 1，并将其作为 `ACK` 数据包中的确认号来实现。当客户端收到这个包含原始 `SYN` 序列号的确认号时，它知道服务器可以接收其通信，反之亦然。`SYN/ACK` 中 `SYN` 部分的目的与原始 `SYN` 数据包相同。它用于传输一个客户端系统可以用来确认的序列号。

# 最终的 ACK 数据包

最后，客户端向收到其 `SYN/ACK` 数据包的服务器发送 `ACK` 数据包。在过程的第二步中，序列号加 1 并作为确认号发送给服务器。一旦接收到最后一个数据包，通信即可开始。

# 流数据的开始

一旦握手建立，客户端和服务器之间此会话中的所有数据包将使用序列号来确保它们顺序正确。然而，从现在起，这些数据包将根据传输的数据帧的大小进行增加，而不是加 1。（要了解更多关于 `TCP` 数据包如何保持有序，请参考 `RFC 793`。）

# HTTP 请求与传输

一旦通信会话建立，就可以对你尝试查看的网页进行实际请求和传输。这涉及到 `HTTP` 和 `TCP`。

过程始于第 4 个数据包，这是我们的第一个 `HTTP` 数据包，它请求服务器将网页发送给客户端。继续展开“数据包详情”面板中此数据包的章节，以查看与其相关的协议信息（如图 6-7 所示）。

```
GET /download.html HTTP/1.1
Request Method: GET
Request URI: /download.html
Host: www.ereal.com
User-agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) Gecko/20101011 Firefox/114.0
Accept: text/xml,application/xml,text/html;q=0.9,text/plain,image/*
Accept-Language: en,q=0.5
Accept-Charset: ISO-8859-1,utf-8;q=0.7
Keep-alive: 300
connection: keep-alive
Refer: http://www.ereal.com/development.html
```
