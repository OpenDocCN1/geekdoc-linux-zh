
`root@kali~$` `airmon-ng`

Interface mode  Driver  Chip

`wlan0`            80211       Realtek RTL8188EUS

```
图 8.10：查看无线网卡详情
```

- 廉价 Wi-Fi 适配器：Edimax EW-7811 (https://www.amazon.com/dp/B003S6S8S0) 这种 Kali 自带了驱动程序。
- 一个支持不同协议的接入点：测试工作

一旦将 Wi-Fi 适配器插入 Kali，并通过 `ifconfig` 就可以看到它的工作状态（如图 8.12）：

![](img/5cafe5b4b24a423ad005874773aac823_302_0.png)

图 8.12：`ifconfig` 输出

在之前的截图中，`wlan0` 是无线接口。输入 `ifconfig wlan0 up` 启用接口。然后通过 `ifconfig wlan0` 查看实际状态（如图 8.13）：

```
root@kali:~ ifconfig wlan0

wlan0: flags=BROADCAST,MULTICAST,UP,RUNNING  mtu=1500

  ether aa:95:e6:3a:fc:60  txlen:100

  RX packets:0  bytes:0    errors 0  dropped 0 coll 0

  TX packets:0  bytes:0    errors 0  overruns 0 frame 0
```
图 8.13：查看接口状态

让我们找出周围的无线网络。为了找到它们，我们使用 `iwlist wlan0 scanning` 命令，你应该 Wi-Fi 网络列表（如图 8.14）：

```
kali@kali~$ iwlist wlan0 scanning

  Cell 0 - Address: 04:95:e6:3a:fc:60

    Channel:6

    Frequency:2.47 GHz (Channel 6)

    Quality=70/70 Signal level=-30dBm

    Encryption:none

    ESSID="Debashish wifi"

    Bit Rates:1 Mb/s; 2 Mb/s; 5.5 Mb/s; 11 Mb/s; 6 Mb/s

      9 Mb/s; 12 Mb/s; 18 Mb/s

      24 Mb/s; 36 Mb/s; 48 Mb/s; 54 Mb/s

    Mode:Master
```
图 8.14：从 Kali 扫描 Wi-Fi

## 嗅探无线数据包的艺术

记住，如果我们想要入侵 Wi-Fi 网络，我们需要在空中捕获之前看到的握手包。这个握手指的是受害者计算机与无线网络之间的连接。

```bash
ifconfig wlan0 down

airmon-ng check kill

iwconfig wlan0 mode monitor

ifconfig wlan0 up
```
