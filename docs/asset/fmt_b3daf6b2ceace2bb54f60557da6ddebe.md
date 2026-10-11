
| 1327 | Td-Link-6e:b0:8a | EAPOL | Apple_3a:c4:2f | 密钥 (Message 3 of 4) |
| 1331 | Td-Link-6e:b0:8a | EAPOL | Apple_3a:c4:2f | 密钥 (Message 4 of 4) |
| 1333 | Td-Link-6e:b0:8a | EAPOL | Apple_3a:c4:2f | 密钥 (Message 1 of 4) |
| 1337 | Td-Link-6e:b0:8a | EAPOL | Apple_3a:c4:2f | 密钥 (Message 2 of 4) |
| 1339 | Td-Link-6e:b0:8a | EAPOL | Apple_3a:c4:2f | 密钥 (Message 3 of 4) |
| 1369 | Td-Link-6e:b0:8a | EAPOL | Apple_3a:c4:2f | 密钥 (Message 4 of 4) |

`pyrit` 说握手不是好的。

`pyrit -r rootsh331-0.cap analyze`

Pyrit 0.5 (1)-2000-2018 Linux June 2015

https://github.com/JPaul/Pyrit

此代码根据 GNU 公用许可证 v3 发布：

解析文件 '`rootsh331-0.cap`' (1/1)...

解析 12 个包 (1802.11 包)，获取 1 个 AP。

```
#1: AccessPoint 64:66:b3:6e:b0:8a ('rootsh331')
未检测到有效的 EAPOL-handshake + ESSID。
```

主密钥 : 1F 48 02 2E 4C 82 F4 0E 26 60 97 E7 8A D1 F1

92 83 6B 68 7F 08 47 33 1D 88 6C 29 8B 40

临时密钥 : D9 E6 11 6B 8C F0 0D 75 8B 36 E3 38 F2 8A 22

BA DA 55 F 97 2C 6F 81 49 3A 53 2B 45 78 7C 0C

56 C8 ED 53 64 94 99 04 E7 0C 1A 7C 2C 07 87 C4

D5 90 55 50 E6 D0 68 94 BB C9 06 AA 55 35 FF 88

EAPOL HMAC : 99 92 11 87 16 7C 8D F2 D1 9F 8E 8D 6F 4D 86

### 示例 2：

Pyrit 喜欢它的消息 3 和 4 数据包，因此我们将为它提供一些，当然是来自与消息 1 和 2 相同的序列。

Pyrit 对手握的四个部分感到很高兴，但将捕获文件标记为“workable（可用的）”。Aircrack 能够像以前一样破解它。

```
pyrit -r clean.cap analyze
pyrit 0.5.1 (C) 2008-2011 Lukas Leer - 2015 John Mora
https://github.com/3PaulMora/Pyrit
This code is distributed under the GNU General Public License v3+
Parsing file 'clean.cap' (1/1)...
Parsed 5 packets (802.11-packets), got 1 AP(S)
#1: AccessPoint 64:66:b3:6e:b0:8a ('rootsh31')
#1: Station 2c:33:61:3a:c4:2f, 1 handshake(s)
#1: HMAC_SHA1_AES, workable, spread 1
```

### 示例 3：

通过选择位置更靠近的包，Pyrit 现在将捕获结果报告为“good（良好的）”而不是“workable”。

Pyrit 更喜欢这种……

```
pyrit -r clean.cap analyze
pyrit 0.5.1 (C) 2008-2011 Lukas Leer - 2015 John Mora
https://github.com/3PaulMora/Pyrit
This code is distributed under the GNU General Public License v3+
Parsing file 'clean.cap' (1/1)...
Parsed 5 packets (802.11-packets), got 1 AP(S)
#1: AccessPoint 64:66:b3:6e:b0:8a ('rootsh31')
#1: Station 2c:33:61:3a:c4:2f, 1 handshake(s)
#1: HMAC_SHA1_AES, good, spread 1
```

### 示例 4：

在这个示例中，我选择了与 1、2 和 3 不同的序列中的消息 4。

| 编号 | 源 | 协议 | 目的地 |
|---|---|---|--|
| 331 | Tp-Link_t6ge:b0:8a | EAPOL | Apple_3a:c4:2f |
| 333 | Tp-Link_t6ge:b0:8a | EAPOL | Apple_3a:c4:2f |
| 336 | Apple_3a:c4:2f | EAPOL | Tp-Link_t6ge:b0:8a |
| 338 | Apple_3a:c4:2f | EAPOL | Tp-Link_t6ge:b0:8a |
| 862 | Tp-Link_t6ge:b0:8a | EAPOL | Apple_3a:c4:2f |
| 1326 | Tp-Link_t6ge:b0:8a | EAPOL | Apple_3a:c4:2f |
| 1329 | Tp-Link_t6ge:b0:8a | EAPOL | Apple_3a:c4:2f |
| 1335 | Apple_3a:c4:2f | EAPOL | Apple_3a:c4:2f |
| 1336 | Tp-Link_t6ge:b0:8a | EAPOL | Apple_3a:c4:2f |
| 1338 | Apple_3a:c4:2f | EAPOL | Apple_3a:c4:2f |
| 1370 | Apple_3a:c4:2f | EAPOL | Apple_3a:c4:2f |
| 1372 | Apple_3a:c4:2f | EAPOL | Tp-Link_t6ge:b0:8a |
| 1376 | Apple_3a:c4:2f | EAPOL | Tp-Link_t6ge:b0:8a |

```
pyrit -r clean.cap analyze
pyrit 0.5.1 (C) 2008-2011 Lukas Leer - 2015 John Mora
https://github.com/3PaulMora/Pyrit
This code is distributed under the GNU General Public License v3+
Parsing file 'clean.cap' (1/1)...
Parsed 5 packets (802.11-packets), got 1 AP(S)
#1: AccessPoint 64:66:b3:6e:b0:8a ('rootsh31')
#1: Station 2c:33:61:3a:c4:2f, 1 handshake(s)
#1: HMAC_SHA1_AES, workable, spread 1
```

![img/ac7a560fa0.png](img/ac7a560fa0.png)

## 结论：

Pyrit 将良好的文件报告为坏的，这是一件坏事。Aircrack-ng 可能会将坏的文件报告为良好的，这更糟糕。

并且记住，保持顺序一致。
