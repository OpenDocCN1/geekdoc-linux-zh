
一旦你安装了 `dsniff`，你应该注意两个文件：

`usr/lib/dsniff.magic` 该文件包含对应特定协议密码数据包的正则表达式。例如，行 `0 *string AUTH pop*` 指定数据包偏移量为 0，类型为 `*string*`，搜索字符串 `AUTH` 并显示 `pop` 消息。这是一个标准文件定义。要需更多信息，你可以在 UNIX/Linux 主机上输入 `man 5 magic`。

`usr/lib/dsniff.services` 该文件描述了 `dsniff` 使用的服务，其结构类似于任何 UNIX/Linux 主机上的 `/etc/services` 文件。

通过修改这两个文件并使用 `-m` 参数运行 `dsniff`，你可以从许多不同的协议中获取用户名和密码。让我们看看如何运行 `dsniff` 来通过我们的热点（或任何其他 WRT54G）收集明文用户名和密码：

```
# dsniff -dmn -s5100 -i eth1
```

<snip>

`dsniff: trigger_set_cap: port 8080 -> http`

`dsniff: trigger_set_cap: port 8888 -> napster`

`dsniff: trigger_set_cap: port 9898 -> aim`

`dsniff: trigger_set_cap: port 65301 -> pcanywhere`

`dsniff: trigger_set_rpc: program 100005 -> mountd`

`dsniff: listening on eth0`

`[ 0 belong=0,""]`

`dsniff: trigger_cap: decoding port 23 as telnet`

----------------------------------------------------------------------

01/13/00 23:16:35 tcp 192.168.1.249.39866 192.168.1.1.23 (telnet)

root

admin

----------------------------------------------------------------------

01/13/00 23:18:26 tcp 192.168.1.249.58937 192.168.1.42.80 (http)

GET /cgi-bin/webif/ HTTP/1.1

```
Host: wrt-office

Authorization: Basic cm9vdDphZG1bg= [root:admin]
```

```
GET /cgi-bin/webif/ HTTP/1.1
Host: wrt-office

Authorization: Basic Og= [:]
```

`dsniff: trigger_tcp: decoding port 80 as http`

在前面的输出中，我们使用 `-d` 标志以调试模式运行 `dsniff`，`-m` 告诉 `dsniff` 读取 `dsniff.magic` 文件，`-n` 禁用解析，`-s1500` 指定以太网的最大传输单元（MTU）大小，以及接口 `-eth1`，它是我们路由器的 WAN 接口。接口取决于你如何设置路由器；某些情况下，`br0` 也可以。在输出中，你可以看到某人（来自 192.168.1.249）正使用 Telnet 登录 192.168.1.1，用户名为 root，密码为 admin。你还可以使用 `dsniff` 捕获 HTTP Basic 认证，因为它捕捉到了同一用户使用 root 用户名和 admin 密码访问另一个名为 wrt-office 的路由器（192.168.1.42）。

`dsniff` 是一个非常强大的工具，事实上，它还带了许多用于审计网络的工具，例如 `filesnap` 可以捕获通过网络文件系统 (`NFS`) 发送的文件，`msgnart` 可以记录嗅探到的 AOL 即时通讯（AIM）、ICQ 2000、IRC 和雅虎 Messenger 聊天会。在你的网络上运行这些工具之前，请确保你已获得相应的许可。

`www.syngress.com`

## 总结

WRT54G 平台可以成为渗透测试人员极具价值的工具，因为它提供了连接到远程网络的替代方法，无需亲身旅行即可进行测试。VPN 可用于各种目的的流量隧道，例如远程嗅探。对于在网络中创建后门，CDMA 连接是最有用的，它允许你绕过本地网络进行远程连接。

你可以使用 WRT54G 远程监控无线频谱和蓝牙流量。这些服务将允许你排查用户问题、检测流氓设备，并监控可能包含敏感信息的手机等易受攻击的蓝牙设备。

最后，你可以使用 Airsnn Rogue Squadron 创建伪热点用于渗透测试，或者仅仅是和朋友一起玩玩玩。

## 解决方案快速通道

### 隧道与 VPN

- `OpenVPN` 是一个非常好的开源项目，可以使用 SSL/TLS 隧道提供路由或桥接 VPN 连接。
- `OpenVPN` 要求你拥有一个 CA 来为客户端和服务器生成证书。
- 在使用 `OpenVPN` 进行远程渗透测试时存在局限性。具体来说，为了在客户端和渗透测试者站点之间提供真正的桥接，你需要将 `OpenVPN` 服务器放置在客户端现场，以便完全访问所有可用系统。

### 使用 OpenWrt 的无线安全工具

- `Kismet Drone` 有助于定位接入点并确定有关无线环境的信息。
- 无线芯片组不支持跳频功能，但可以使用 shell 脚本代替进行跳频。
- 为了在 WAN 口上连接 `Kismet Drone`，你必须修改防火墙规则集。
- 修改廉价的 USB 蓝牙适配器可以提供远距离蓝牙扫描。
- `BlueZ` 工具已移植到 OpenWrt，它们可以提供基本的蓝牙发现。
- 通过一些脚本，你可以进行持续蓝牙扫描，并将其电子邮件发送到场外进行进一步分析。

你可以使用 `WRTLS54GS` 和 `Wi-Spy` 适配器进行远程 2.4GHz 频谱分析。

`Eakiu` 是用于配合连接到 `WRTLS54GS` 的远程 `Wi-Spy` 适配器使用的客户端工具。

### WRTLS54GS 和 CDMA 网络连接

你可以使用连接到网络的 CDMA 设备来绕过外部防火墙。

你可以将 CDMA 调制器与 PPP 接口。

你使用 NVRAM 变量将默认 WAN 连接更改为 CDMA USB 适配器。

### WRT54G 无线强制门户密码嗅器

Shmoo Group 的 `Rogue Squadron` 提供了一个可自定义的伪门户，用于获取密码。

使用 `Rogue Squadron` 门户获取的密码存储在设备上，必须定期提取。

## 常见问题

以下由本书作者回答的常见问题旨在衡量你对本章所介绍概念的理解程度，并帮助你在现实生活中实施这些概念。如果你想让作者回答你关于本章的问题，请访问 `www.syngress.com/solutions` 并点击“Ask the Author”表单。

问：为什么 `Kismet Drone` 不支持原生跳频？

答：Broadcom 无线驱动程序的专有性质阻止了原生跳频。由于缺乏制造商提供的文档，尚无法确定是否支持原生跳频。

问：OpenWrt 下是否有其他蓝牙工具可用？

答：截至本文编写时，OpenWrt 没有其他蓝牙工具。但是，可能可以将某些现有工具移植到此平台。

问：为什么我应该选择 USB CDMA 调制器而不是 PCMCIA 接口？

答：许多移动技术已经放弃了对 Express/34 插槽的支持，这些槽之间是不兼容的。USB 端口几乎出现在所有现代（以及不现代）的计算设备（包括路由器）上，USB 将最大化同一台 CDMA 调制器的潜在替代应用。

问：当我使用 Wi-Spy 适配器时遇到了很多干扰。我能做什么？

答：使用 USB 延长线让 `WRTLS54GS` 和 `Wi-Spy` 适配器之间保持一定距离。

问：我看不到我的 USB 蓝牙适配器。发生了什么？

答：确保你已安装了所有适当的内核模块，特别是 `hci-usb`。

问：为什么通过 SSH 连接到 Rogue Squadron WRT54G 需要花费长时间？

答：Rogue Squadron 的设置似乎存在一些问题。这种延迟可能是由于 SSH 需要为每个连接重建会话密钥，这在功率有限的设备上可能需要一些时间。

# 第 7 章：WRT54G 硬件破解

本章中的解决方案：

- 无线天线的乐趣
- 添加端口：SD 卡、串口和 JTAG
- 使用替代电源为你的 WRT54G 供电
- 总结
- 解决方案快速通道
- 常见问题

## 引言

在本章中，我们将涵盖需要对 WRT54G 路由器进行硬件修改的破解方法。尽管许多人认为这些破解中的某些属于高级，但我们在这里是为了向你展示，专家和普通人士都可以轻松完成它们。在本章的过程中，具备一些电烙铁和电源工具的经验将会有帮助。即使只有很少或没有练习，你也可以掌握一些基本的焊接技术。Make 杂志也发布了一些关于焊接的精彩教程。这些教程将让你迅速成为一个专家，而且它们非常易懂。你可以在博客 `www.makezine.com/archive/2007/01/learn_to_s.html` 上找到这些教程和其他优秀的链接。

## 无线天线的乐趣
