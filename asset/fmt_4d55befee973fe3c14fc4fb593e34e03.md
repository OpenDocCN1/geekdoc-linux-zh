
`admin` 和 `tester` 是受害者尝试登录路由器的错误凭据。当输入 `rootshill:rootshill` 时，所有页面都可以通过受害者的浏览器访问，其流量以未加密的明文格式（HTTP）通过攻击者系统。

Etercap 不会捕 SSL 网站的凭据。在启用 SSL 的网站上进行嗅探需要许多问题，如`签名证书`、SSL、HSTS 等。我们将在稍后的另一文中学习。

因此，我们能够在没有物理接触受害者的情况下获取路由器的 Web 登录凭据。

很酷，不是吗？好吧，这仅仅是开始。你可以使用路由器凭据进行各种操作，例如：

- 1. 过滤其他 MAC 地址以访问或或路由器 Web 界面。
- 2. 限制你之外所有用户的上网网速。
- 3. 如果对你或其他用户应用了上网限制，则将其移除。
- 4. 修改 DNS 地址以进行全球嗅探。
- 5. 以及许多其他。去探索吧！

嗅探路由器只是你探索的内容之一，我们还有许多其他技术可以学习来测试网络或设备的强度。我们将逐一详细介绍。请随时告诉你的观点，以便我继续下去并不断提高每篇文章的质量。

看看攻击者系统中的路由器界面是什么样的。

![](img/ac8a7ada56be8fa0ece47a14bb6f46cd_123_0.png)

目前关于子网嗅探的内容就到此。

## 防止嗅探攻击

受害者只有一种方法可以确认其在 W/LAN 上被嗅探。检查 ARP 表并查看设备的 MAC 地址是否与路由器 MAC 地址匹配。

```
arp -a  //Windows, MAC 或 *nix
```

看一眼：

```
C:\Users\rootshell31\arp -a

Interface: 192.168.0.100     0x11

Internet Address      Physical Address      Type

192.168.0.100         64-66-b3-6e-b0-ba      dynamic

192.168.0.100         00-c0-ca-5a-34-b6      dynamic

224.0.0.2             01-00-se-00-02      static

224.0.0.22            01-00-se-16      static

224.0.0.252           01-00-se-fb      static

239.255.255.250      01-00-se-7f-fa      static

255.255.255.255      ff-ff-ff-ff      static
```
![](img/ac8a7ada56be8fa0ece47a14bb6f46cd_124_0.png)

```
C:\Users\rootshell31\arp -a

Interface: 192.168.0.102     0x11

Internet Address      Physical Address      Type

192.168.0.100         00-c0-ca-5a-34-b6      dynamic

192.168.0.100         ff-ff-ff-ff      dynamic

192.168.0.255         01-00-se-02      static

224.0.0.2             01-00-se-16      static

224.0.0.251           01-00-se-fb      static
```
![](img/ac8a7ada56be8fa0ece47a14bb6f46cd_124_1.png)

如果你注意到第一次执行时的路由器 MAC 地址 (01) 与攻击者的 MAC 地址（即 .100）不同。当我启动 MITM 攻击后再次执行命令，从受害者的角度来看，路由器是 192.168.0.100。数据使用连接设备的 MAC 地址传输。由于路由器的 MAC 被伪造了，受害者开始向攻击者的 MAC 发送流量。

希望现在清楚了，我们将涵盖网络的不同方面。

## 干扰 Wi-Fi 网络

干扰网络（即网络上的每个用户），你不需要连接网络或知道网络密码。你只需要构造一些包并在空中广播，包括 AP 的 MAC 地址和 SSID 以及让连接用户断线的认证包。

### 它是如何工作的？

我们使用 `aircrack-ng` 套件中的 `airplay-ng` 构造一个包并在空中广播，然后由用户接收。检查数据包的源，即可以更改其 MAC 地址的地方。我们将使用 `airplay-ng` 执行。稍后我们将学习如何使用编程来实现。

| | 0-3 | 4-7 | 8-13 | 14-15 | 16-18 | 19-31 |
|---|---|---|---|---|---|---|
| 0 | Version | Internet Header Length | Differentiated Services Point | Explicit Congestion Notification | Total Length | |
| 32 | | | | | Fragment Offset |
| 64 | Time to Live | | | | Flags | Header checksum |
| 96 | | | Source IP Address | | | |
| 128 | | | Destination IP Address | | | |
| 160 | | | Options (if Header Length > 5 ) | | | |
| 160 or 192+ | | | Data | | |

来源：Wikipedia

在终端运行：
语法：`aireplay-ng -0 <请求数> -a <BSSID> -e <ESSID> <监控模式接口>`

```bash
sudo aireplay-ng --deauth 0 -a 64:66:B3:6E:00:8A -e "rootsh31" wlan0
```

> 零 (0) 可以代替 `-deauth` 和带引号的 SSID 以避免冲突。
`-0`: 去认证请求代码，1 为伪造-ARP，依此类推。

| 攻击 # | 攻击名称 |
|---|---|
| 0 | 去认证 (Deauthentication) |
| 1 | 伪造认证 (Fake Authentication) |
| 2 | 交互式包重放 |
| 3 | ARP 请求重放攻击 |
| 4 | Korek's ChopChop 攻击 |
| 5 | 分段攻击 |
| 6 | Café-Latte 攻击 |
| 7 | 面向客户端的分段攻击 |
| 8 | 注入测试 |

`-0` 或 `--deauth 0` 表示无限的去认证请求，`--deauth 5` 意味着 `aireplay-ng` 将发送 5 个认证包并退出。

这是通过广播认证包来干扰网络，如果攻击者只想干扰一个或某些特定用户的网络访问怎么办？

只需使用 `-c` 选项告诉 `aireplay-ng` 你想要对哪个客户端进行 DoS。

## 剖析无线客户端

这是一个被称为单播（Unicast）的请求，因为我们正在向特定的客户端发送包。你也可以将其称为 DoS（拒绝服务）攻击。

```bash
aireplay-ng --deauth 0 -a 64:66:B3:6E:00:8A -e "rootsh31" -c 00:c0:ca:5a:34-b6 wlan0
```
