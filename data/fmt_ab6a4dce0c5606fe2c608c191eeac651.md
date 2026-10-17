
$ user1@localhost:~/Desktop

Help

[user1@localhost]$ `ifconfig enp0s`

`enp0s`: flags=63<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

      inet 192.168.0.190 mask 255.255.255.0 broadcast 192.168.0.255

      inet6 fe80::20c:27ff:fe6:9af prefixlen 64 scope 0x20<link>

      ether 00:08:27:fe6:9af txqueuelen 160 (Ethernet)

          RX packets 140 bytes 12832 (12.5 KiB)

          RX errors 0 dropped 0 overruns 0 frame 0

          TX packets 155 bytes 15369 (15.0 KiB)

          TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

```
**图 11-9** 来自 ifconfig 终端窗口的网络配置

来源：CentOS$Terminal
```

- 1. 如必要，使用活动 1-1 中相应的说明启动虚拟机。
- 2. 要显示以太网设备设置，点击“应用程序”，点击“系统工具”，点击“设置”，然后点击“网络”。
- 3. 高亮活动网络接口。
- 4. 记录 IP 地址、IP 网关和 DNS IP 地址以备后之用。
- 5. 关闭已打开的窗口。
- 6. 使用 `ifconfig` 工具查看 TCP/IP 设置，右键点击“开始”，然后点击“命令提示符”。
- 7. 要查看 IP 配置，输入 `IPCONFIG /ALL` 并按回车。
- 8. 将你的设置与步骤 3 中记录的设置进行比较。
- 9. 关闭命令提示符窗口。
- 10. 保持虚拟机登录状态以供后续活动。

## 访问网络资源

在 Windows 10 中，你可以通过“网络”文件夹访问网络资源。要打开此文件夹，点击“开始”，点击“网络”。这会显示本地网络上所有可用计算机和设备。

如果你想访问未列出的特定资源，可以使用通用命名规范 (UNC) 符号。UNC 路径遵循格式为 `\\computername\sharename`。例如，`\\192.168.1.10\Shared`。你可以将此路径输入到文件管理器的地址栏中直接访问文件夹。

访问网络资源的另一种方法是将其映射为驱动器。这允许网络文件夹看起来就像是你计算机上的一个驱动器一样。要映射网络驱动器，打开文件资源管理器，右键点击“此电脑”，并选择“映射网络驱动器”。按照提示分配驱动器号并输入 UNC 路径。

![](img/290e46d5832f20e3707f4841e4e6d75a_523_0.png)

图 11-10 Windows 中的网络资源

来源：Windows 10

### 访问网络资源

505

你可以指定驱动器号，或允许 Windows 10 为提供一个。如果你不提供驱动器号，Windows 10 将从 Z: 开始反向分配驱动器号。例如，要将 N: 驱动器连接到 Windows 10 虚拟机和 Drivers 共享，请输入：

```
NET USE N: \Windows10\Drivers
```

在 Windows 资源管理器中可以使用 N: 驱动器。当然，你也可以 `DIR` 目录命令查看文件。

## 活动 11-3：连接到 Windows 10 中的网络共享

所需时间：10 分钟

目标：使用 Windows 10 连接到网络共享。

描述：在此活动中，你将探索连接到共享文件夹的方法。首先，你需要确定宿主机的 IP 地址。你将使用搜索框找到并连接到宿主机上的 TextShare 文件夹。当你按照虚拟化软件的附录 B、C 或 D 中的说明操作时，TextShare 文件夹已安装在宿主机上。在活动稍后的部分，你将使用 UNC 连接到该共享。如果你想访问网络数据，此活动将非常有用。

- 1. 如果必要，使用活动 1-1 中的相应指令启动你的虚拟机。
- 2. 在宿主机上执行活动 11-1 中的第 2 至 4 步，确定访问计算机的地址。
- 3. 最小化你的虚拟机。
- 4. 要显示网络连接详细信息窗口，在宿主机上右键点击“开始”，点击“网络连接”，双击“以太网”（或其他连接）链接，然后点击“详细”。
- 5. 记录宿主机的 IPv4 地址。
- 6. 关闭打开的窗口。
- 7. 要显示宿主机 TextShare 文件夹上的共享文件，点击“开始”，在搜索文本框中输入 `\IPv4 Address\`，然后点击宿主机上的 TextShare 文件夹。

![](img/290e46d5832f20e3707f4841e4e6d75a_526_0.png)

如果你无法连接到 TextShare 文件夹，请联系你的导师。

- 8. 关闭文件资源管理器窗口。
- 9. 返回 Windows 10 虚拟机。要打开命令提示符，右键点击“开始”，然后点击“命令提示符”。

## 第 11 章 本地网络访问

- 10. 要使用 UNC 定位共享文件，输入以下内容并按回车：
`NET USE \\IPv4Address\TextShare`
- 11. 验证 Windows 10 是否为共享文件夹分配了 Z: 驱动器。
- 12. 要切换到 Z: 驱动器，输入 Z: 然后按回车。
- 13. 要查看文件名，输入 DIR 并按回车。
- 14. 关闭命令提示符窗口。
- 15. 要在大 Windows 资源管理器中查看 Z: 驱动器的内容，点击“开始”，点击“文件资源管理器”，然后点击 TextShare (\IPv4 Address) (Z):
- 16. 要在大记事本中查看 Article12.txt 文件的内容，双击它。
- 17. 关闭打开的窗口。
- 18. 保持虚拟机登录状态以供后续活动使用。

## 在 CentOS 7 中检查网络资源

设置网络连接后，检查计算机与相邻计算机之间的通信非常重要。要检查计算机是否能够与网络中的另一台计算机通信，可以使用 `ping` 命令。如果命令成功，屏幕上的消息将报告发送的数据包包含多少字节，以及请求和接收消息所需的时间。使用 `ping` 命令对于检查网络是否设置正确非常有用，特别是当手动输入网络信息时。

如果网络无法工作或找不到其他系统，`ping` 命令将返回一系列“目标主机不可达”（Destination Host Unreachable）消息，如图 11-14 所示。使用 `ping` 命令对于验证系统已连接并可以在网络上通信非常有帮助。当计算机可用时，`ping` 命令会返回一系列字节，如图 11-15 所示。你可能注意到在之前的示例中，`ping` 命令配合 IPv4 IP 地址使用。在图 11-16 中，你可以看到相同的命令用法，但使用的是 IPv6 可路由主机名（www.com）而不是 IP 地址。

另一个工具 `traceroute` 对于检查网络是否正常非常有用。可以使用 `traceroute` 查看形成连接的每一个“跳数”（见图 11-17），包括你为了到达请求主机而跨越通信的所有交换机、路由器、防火墙或其他计算机。有时使用 `traceroute` 时，通信会停止，你会看到一系列 ***\*** 符号，这表示路径中的设备不可用，或者某个设备被配置为不响应此类请求，如图 11-18 所示。

## 在 CentOS 7 中访问网络资源

CentOS 7 访问共享文件的方法与 Windows 10 中使用的方法相似。要访问共享，你必须挂载共享。在创建了挂载目的地的目录后，你可以输入 `mount` 命令并指定共享的 UNC、登录凭据和目标目录。共享完成后，将目录更改到挂载目标地并执行 `ls` 命令查看文件。

## 访问网络资源

```
File Edit View Search Terminal

[user@localhost:~/Desktop] ping 192.168.1.189

PING 192.168.1.189 (192.168.1.189) 56(84) bytes of data.

From 192.168.1.248 icmp_seq=1 Destination Host Unreachable

From 192.168.1.248 icmp_seq=2 Destination Host Unreachable

From 192.168.1.248 icmp_seq=3 Destination Host Unreachable

From 192.168.1.248 icmp_seq=4 Destination Host Unreachable

From 192.168.1.248 icmp_seq=5 Destination Host Unreachable

--- 192.168.1.189 ping statistics

5 packets transmitted, 0 received, 100% packet loss, time 4000ms
```
