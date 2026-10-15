
# 活动捕获（控制路径）

进程间通信禁用

系统消息禁用

TCP 禁用

UDP 禁用

其他禁用

# 活动捕获（数据路径）

Wi-Fi 客户端启用 MAC: `00:24:d7:6a:71:24` 过滤器: 所有

Ipsec 启用 对等端: `10.1.80.100`

最后三个命令禁用了本节中解释的设置。完成故障排除后，*务必*禁用数据捕获设置，因为会给控制器增加不必要的 CPU 处理。这一步经常被忽略。

```
#no packet-capture datapath ipsec
#no packet-capture datapath wifi-client
#no packet-capture destination
```

## Destination

`packet-capture` 命令允许您定义一个目标，指定任何数据路径捕获发送或存储到何处。该目标不仅在 `packet-capture` 命令配置捕获数据包时使用，在配置防火墙镜像（会话镜像）时也会使用。本章稍后将解释防火墙镜像。

数据包捕获可以发送到控制器的接口、远程设备的 IP 地址或控制器的本地文件系统。`packet-capture` 命令后跟问号会显示定义不同选项的参数。捕获目标是其中之一：

```
#packet-capture ?
```

- `controlpath` 启用控制路径。捕获的数据包存储在 `/var/oslog/filter.pcap`。仅支持导出到本地文件系统。
- `copy-to-flash` 将捕获的数据包拷贝到 flash。
- `datapath` 启用数据路径捕获。捕获的数据包存储在 `/var/oslog/datapath.pcap` 或从控制器镜像。
- `destination` 配置捕获目标。
- `reset-pcap` 删除旧 pcap 文件并重启捕获。控制路径始终输出到日志 filter.pcap。此文件位于控制器上。

以下 CLI 输出显示了使用 `packet-capture` 命令定义三个可用捕获目标的示例。一次只能定义一个目标：

```
#packet-capture destination interface 0/0
#packet-capture destination ip-address 1.2.3.4
#packet-capture destination local-filesystem
```

### 导出到接口

当数据捕获目标设置为接口时，捕获的数据流量将发送到控制器的物理端口，通常是千兆以太端口。您需要将运行包分析软件的计算机物理连接到该接口。连接后，运行包分析软件，如 Omnipeek 或 Wireshark。配置包分析软件使用您用于连接接口的以太适配器。

### 导出到 IP 地址

当数据捕获目标设置为 IP 地址时，数据包将直接跨网络传输到指定设备的地址。确保该 IP 地址对应配置了包分析软件的计算机。控制器可以配置为将数据路径流量或 IPsec 转发到该 IP 地址的计算机。强烈建议目标使用有线计算机。如果目标计算机是无线设备，可能会在捕获所需数据包的同时再次捕获发送到您计算机的数据。为了传输这些数据，捕获的流量必须放在单独包中，以便重定向到包分析计算机。控制器通过将其封装在 GRE 隧道中来实现。每个帧都封装在 GRE 帧中并跨网络传输到执行分析的计算机。GRE 帧定义为 IP 协议 47。

当运行分析软件的计算机接收到 GRE 帧时，软件需要配置为解释 GRE 帧，以显示隧道数据。幸运的是，许多包捕获程序（如 Wireshark 和 Omnipeek）都能识别 GRE 帧。这些程序理解 GRE 帧封装并转发其他帧。它们获取封装的数据并以解码后的形式显示，这在本质上就是实际的数据流。

请记住，当数据传输时，帧中会添加一个头部，用于标识它的来源和去向。当该帧正在被封装时，GRE 只是在帧上添加了一个额外的头部。这类似于给某人写信。当你写好信后，你会将信件放入信封并在信封上写上地址。封装只是将这封信和信封放入另一个信封中。就像你信件的接收者意识到有两个信封且内容是信件一样，数据包分析程序能够识别出实际负载是内部帧的内容。

### 捕获到本地文件系统

当数据包捕获发送到本地文件系统时，它存储在控制器的两个日志文件之一：`filter.pcap` 或 `datapath.pcap`。捕获到控制器的文件系统的优势是，可以在没有数据包分析器的情况下捕获数据。该文件可以在以后或从另一个系统导出并查看。这对于从远程站点收集故障排除数据或与技术协助中心 (TAC) 工作时非常有帮助。捕获到控制器文件系统的一个潜在问题是捕获文件可能会超过可用存储空间。

如之前指定的，如果正在捕获控制路径流量，它仅输出到文件系统，并存储在文件 `/var/log/oslog/filter.pcap` 中。如果正在捕获数据路径流量，且其输出被发送到文件系统，则存储在文件 `/var/log/oslog/datapath.pcap` 中。

这些文件名无法在控制器上查看，但可以使用多种选项访问这两个文件。第一种方法直接从 CLI 提示符显示文件内容。这两个文件都可以执行此操作。以下 CLI 输出显示了来自控制路径文件和数据路径文件的示例捕获内容：

```bash
#show packet-capture controlpath-pcap
15:39:00.748600 IP 127.0.0.1.8210 > 127.0.0.1.8210: UDP, length 85
15:39:00.816879 IP 127.0.0.1.8210 > 127.0.0.1.8210: UDP, length 84
15:39:00.816998 IP 127.0.0.1.8210 > 127.0.0.1.8210: UDP, length 88
15:39:02.819748 IP 127.0.0.1.8210 > 127.0.0.1.8210: UDP, length 84
15:39:02.819826 IP 127.0.0.1.8210 > 127.0.0.1.8210: UDP, length 88
15:39:04.823459 IP 127.0.0.1.8210 > 127.0.0.1.8210: UDP, length 84
15:39:04.823575 IP 127.0.0.1.8210 > 127.0.0.1.8210: UDP, length 88

#show packet-capture datapath-pcap
16:17:08.838489 ARP, Request who-has 10.1.90.153 tell 10.1.90.100, length 42
16:17:08.838536 IP 10.1.90.100 > 10.1.90.152: GREv0, length 98: gre-proto-0x8280
16:17:08.840229 IP 10.1.90.152 > 10.1.90.100: GREv0, length 84: gre-proto-0x8280
16:17:08.840275 ARP, Reply 10.1.90.153 is-at 00:24:d7:6a:71:24, length 28
16:17:41.346013 IP 10.1.90.152 > 10.1.90.100: GREv0, length 96: gre-proto-0x8280
16:17:41.346109 IP 10.1.90.153.60431 > 52.170.24.150.443: Flags [F.], seq 2879408985, ack 2059848798, win 59, length 0
16:17:41.420225 IP 52.170.24.150.443 > 10.1.90.153.60431: Flags [F.], ack 1, win 507, length 0
16:17:41.43 IP 10.1.90.100 > 10.1.90.152: GREv0, length 102: gre-proto-0x8280
```

`packet-capture` 命令也提供了将控制路径文件或数据路径捕获文件复制到 flash 分区的方法，你可以在那里查看并复制文件。生成的文件名为 `controlpath-pcap.gz` 或 `datapath-pcap.gz`。一旦文件位于 flash 分区，就可以通过 FTP 或 TFTP 轻松地复制到计算机。以下 CLI 输出显示了将控制路径和数据路径文件复制到控制器 flash 分区的命令。`dir` 命令及其输出了文件信息。

```bash
#packet-capture copy-to-flash controlpath-pcap
#packet-capture copy-to-flash datapath-pcap
#dir
-rw-r---- root 17275 Mar 9 23:22 controlpath-pcap.gz
-rw-r---- root 325902 Mar 9 23:22 datapath-pcap.gz
```
