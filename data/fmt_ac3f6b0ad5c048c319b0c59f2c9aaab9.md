
创建目录：`root/.john`

# 第 9 章 自定义安全现场 Linux 光盘

加载了 3 个密码哈值，带有 3 个不同的盐（FreeBSD MD5 [32/32]）`jake` (`jake`) `toor` (`root`)

在这个示例中，发现用户 `jake` 的密码简单就是 `jake`。发现 `root` 的密码是 `toor`。如果你能够在运行中的系统上破解用户的密码，你应该告诉他们更改密码。完成后，请务必移除 `mypasswd` 文件。

其他离线破解工具包括 `Rainbow Crack`、`OPHCrack`、`Rcrtdump`、`SAMDump` 和 `WebCrack`。`Rainbow` 使用彩虹表来加速密码破解。（更多信息请参阅 `www.rainbow.com/rainbowcrack`。）

## 在线密码攻击

在线密码攻击的执行可能更加困难。重复的暴力破解攻击很容易被发现。系统可以配置为防止人员反复尝试登录并失败。

`Hydra` (`www.hydra.org`) 是一款并行破解程序。它可以使用十多种以上的服务类型（`telnet`, `ftp`, `pop3`, `map` 等）来猜测密码。`CowPatty` 是另一种用于破解 `FTP`、`HTTP`、`IMAP`、`MySQL` 等其他服务密码的暴力破解工具。`Medusa` (`www.medusa.net`) 是另一种并行密码破解工具。

## 运行模糊器（Fuzzers）

模糊器（`fuzzer`）是一种向应用程序注入输入的程序，希望结果是应用程序崩溃或导致异常。这有助于确定服务器是否容易受到缓冲区溢出和拒绝服务攻击等影响。你可以在模糊器菜单（`Menu → BackTrack → Fuzzers`）中找到模糊器。`flood` 命令允许你识别要攻击的主机端口。你可以使用 `fuzz.py` 来帮助审计设置了 `setuid` 的二进制文件。`BackTrack` 还带有模糊器创建工具包（`Fuzzer Creation Kit`）。该工具包带有工具包括 `webfuzz`（用于模糊的小工具组合）和 `spike`（用于发送随机参数以寻找导致端口的 bug）。

## 伪装（Spoofing）

破解网络或系统的一种方法是运行程序，其中程序伪装成它不是的东西，例如合法的 `DNS` 服务器或 `DHCP` 服务器，以希望欺骗毫无防备的用户或为你提供关键信息。`BackTrack` 包含一整套伪装工具（`Menu → BackTrack → Spoofing`），你可以尝试使用它们来测试你系统的漏洞。

`arspoof` 程序（来自 `www.monkey.org/~duong/dsniff` 包的一部分）试图欺骗另一台计算机使其相信自己是网关机器。它通过不断向受害者机器发送其 `IP` 地址作为网关来实现这一点。当受害者机器最终将 `arspoof` 的 `MAC` 地址缓存为网关时，它开始将 `IP` 包发送到 `arspoof` 而不是真实的网关。

`dhcp` 程序（来自 `www.phenoelit.de/irpas`）是一个 `DHCP` 泛洪器。这种技术也被称为 `DHCP` 耗尽攻击。`dnsspoof` 命令试图通过对各种 `DNS` 地址和指针查询提供伪造回复，来说服局域网上的其他系统自己是 `DNS` 服务器。

使用 `fragroute` 命令，你可以更改和重写指向局域网外的流量。这种网络流量被称为出口流量（`egress traffic`）。虽然 `fragroute` 只对源本地机器的数据包有效，但 `fragrouter` 命令也可以用于其他机器。

检查伪装菜单查看你还可以进行的其他伪装类型。例如，某些命令尝试重定向 `ICMP` 流量，另一些则尝试通过重放 `TCP/IP` 包获取控制权。

## 网络嗅探器（Sniffers）

如其名，网络嗅探器监控网络，试图“嗅探”在该网络上传输的信息。这些信息可以用于坏事（当有人试图窃取数据或连接信息时），也可以用于善事（发现网络上的潜在问题）。在某些情况下，使用嗅探器可以确保员工没有在使用电脑时违反任何公司政策。

`BackTrack` 包含了十多个嗅探器，你可以使用它们来监控各种网络流量。检查嗅探器菜单查看 `BackTrack` 包含了哪些嗅探器（`Menu → BackTrack → Sniffers`）。

## 第 9 章 自定义安全 Linux 光盘

你可以使用 `AIM` 嗅探器（`aimsniffer` 命令）记录并捕获 `AOL Messenger` 会话的流量。`Driftnet` (`www.ex-portal.com/~chis/driftnet`) 是一种图形化实用，监听 `TCP` 流量中的图像并在 `Driftnet` 窗口中显示找到的内容。图 9-8 显示了从本地浏览器选择 `Wikipedia` 后在 `Driftnet` 窗口中出现的图像。

### 图 9-8

使用 `driftnet` 显示 `TCP` 流量中遇到的图像

![](img/6b7a4aaf8c4f76728e9b63b90222dd8e_297_0.png)

`dsniff` 命令（`http://monkey.com/~duong/dsniff`）是一个密码嗅探命令，可以监听各种服务的密码。这些服务包括 `FTP`、`TELNET`、`SMTP`、`HTTP`、`POP`、`X11`、`AIM`、`ICQ` 等等。当 `dsniff` 运行时，它会自动检测它正在嗅探的协议，提取出密码信息，并将这些信息以 `Berkeley DB` 格式保存到输出文件中。

要嗅探安全外壳（`SSH`）流量，可以将 `sshmit` 工具（`dsniff` 软件包的一部分）放置在 `ssh` 客户端和服务器之间。通过模拟真实的 `ssh` 服务器，`sshmit` 可以从毫无防备的客户端获取密码信息，然后代表与真实服务器完成交易，而客户端不会怀疑出了任何问题。`aftercap` 工具（`http://ettercap.sourceforge.net`）是一个图形化工具，同样可以执行中间人攻击，但 `aftercap` 还可以捕获整个会话以及密码信息。

正如其名所示，`URLsnarf`（`urlsnarf` 命令）可以获取指定接口上请求的 `Web` 信息（匹配你喜欢的任何模式）。`XSPy`（`xspy` 命令）可以跟踪输入到 `X` 显示的所有内容，并将这些信息回显到运行 `xspy` 的 `shell` 终端。

要保存使用 `NFS` 协议传输的文件，可以使用 `filesn` 命令。使用 `msgnarf` 命令，你可以保存来自许多不同 `IRC` 和消息协议的消息和聊天会。通过 `mailsnarf`，你可以嗅探 `SMTP` 和 `POP` 流量以保存电子邮件。`mailsnarf`、`filesn` 和 `msgnarf` 都是 `dsniff` 软件包的一部分。

### 无线网络工具

你可以使用处理无线网络的工具来尝试分析流量、破解密码、伪造数据包，并在网卡上切换不同的驱动配置。你可以在“`Wireless Tools`”菜单（`K menu -> BackTrack -> Wireless Tools`）查看 `BackTrack` 中用于无线局域网的工具。

`Kismet` 是一个用于无线接口的流行工具。通过 `Kismet`，你可以检测 `802.11` 无线网络（包括 `802.11b`、`802.11a` 和 `802.11g`）的入侵。`Kismet` 通过被动收集数据包来检测隐藏网络。它使用标准名称检测网络，并可以随着时间的推移伪装隐藏网络。你用 `Kismet` 记录的数据与 `Etter` 和 `tcpdump` 兼容。

要测试无线局域网节点密码强度，你可以使用如 `WepAttack`（`http://webpattack.sourceforge.net`）、`Wep_crack` 和 `Wep_decrypt`（`http://www.lava.net/~newsham/wlan`，属于 `wep_tools` 软件包）以及 `Weplab`（`http://weplab.sourceforge.net`）等工具。这些工具中的每一个都为测试无线网络密码的安全性提供了不同的选项。

“`Miscellaneous`”子菜单提供了一些杂项无线工具。`macchanger` 工具（`www.allobs.com/macchanger`）允许你查看并更改网络接口的 `MAC` 地址。如果你的系统连接了 `GPS` 设备，可以通过分别选择“`GPS Daemon`”或“`Stop GPS Daemon`”来启动和停止 `GPS` 跟踪守护进程。此外还有若干用于更改无线网卡驱动程序的实用。

要在无线网络上伪造数据包，“`Packet Forging`”菜单上提供了一些工具。`aircrack-ng` 软件包（`aircrack-ng.org/doc.php`）包含了审计无线网络可靠性的工具，包括 `airplay-ng`（用于注入帧以生成流量从而破解 `WEP` 和 `WPA-PSK` 密钥）。`Aircsnarf`（`www.shmo.com`）可用于设置伪造接入点。`WifiTap`（`wi tap` 命令）可用于在 `802.11` 网络上捕获流量并注入数据包（`http://sid.rack.org/index.php/wifitap_EN`）。

### 蓝牙设备工具

监控蓝牙设备（`www.bluetooth.org`）的工具位于“`Bluetooth`”菜单中（`K menu → BackTrack → Bluetooth`）。`Blue Snaper`（`bluesner` 命令）下载未受此类入侵保护的蓝牙设备电话录。`Carwhisperer`（`carwhisperer` 命令）测试蓝牙车载设备的漏洞，特别是那些使用标准密码密钥的设备（见 `http://trifinite.org/trifinite_stuff_carwhisperer.html`）。

你可以使用 `HelMoto` 工具（`helomoto` 命令）利用某些摩托罗拉手机和其他设备对受信任设备的处理漏洞。你可以从 `Trifinite` 网站（`http://trifinite.org/trifinite_stuff_helomoto.html`）了解 `HelMoto` 攻击。

### Cisco 路由器工具

查看“`Cisco Tools`”菜单（`K menu → BackTrack → Cisco Tools`）查找检查 `Cisco` 路由器漏洞的工具。`Global Exploiter`（`cge.pl` perl 脚本）可以测试一系列已知的 `Cisco` 设备漏洞。使用此工具通常需要目标和测试的漏洞名称。你可以从 `BlackAgents` 网站（`www.blackagents.it`）了解该脚本。

`Cisco Torch` 是一个 `Cisco` 漏洞扫描器（`cisco-torch.pl` perl 脚本）。通过它，你可以扫描 `Cisco` 设备上的多种服务，包括 `telnet`、`sshd`、`snmp` 和 `tftp`。你可以对网络时间协议（`NTP`）和 `TFTP` 服务进行指纹识别。

`Yersinia`（`yersinia` 命令）是一个用于分析网络协议的工具，包括 `Cisco` 发现协议（`CDP`）。你可以从其主页（`www.yersinia.net`）获取更多关于 `Yersinia` 的信息。`cisco-copy-config.pl` 和 `merge-copy-config.pl` perl 脚本分别是分别使用 `SNMP` 复制和合并 `Cisco` 配置的简单脚本。

### 数据库分析工具

`BackTrack` 将分析数据库漏洞的工具分为通用数据库工具、`MS-Sql`、`Mysql` 和 `Oracle`。存在许多工具用于检查数据库漏洞。

`Absinthe`（`www.ox90.org/releases/absinthe`）是一个用于分析数据库漏洞的图形化工具。

## 第 9 章 自定义安全 Linux CD

（注：提供的 OCR 文本在句子中间发生了跳转到第 9 章。我将按照提供的文本进行处理，保持逻辑流贯。）

## 向 BackTrack Live CD 中添加软件

通过第 6 章“构建自定义 Knoppix Live CD”到第 8 章“构建基础 Gentoo Live CD”中描述的定制化和重制技术，你可以为 `Knoppix`、`Fedora` 和 `Gentoo` live CD 添加本章描述的组件（以及你选择的任何组件）。在某些情况下，你所选择的 live CD 类型（类型）可能已经有了相应的软件包（`Deb`、`RPM` 或 `Emerge` 软件包）。在其他情况下，你可以从文中描述许多此类组件时提到的项目网站下载你需要的软件。

由于 `BackTrack` 是基于 `slackware`（特别是 `SLAX` live CD）发行版的，接下来的我将描述如何向 `BackTrack` live CD 添加基于 `SLAX` 的程序包。通过这种方式，你可以下载并运行 `SLAX` 仓库中提供的任何包（称为模块）。

向像 `BackTrack` 这样基于 `SLAX` 的 live CD 添加软件模块的技术比第 6 章中为 `Knoppix` 重制的技术（使用 `chroot` 环境）要简单得多。你可以通过两种方式向 `BackTrack` live CD 添加 `SLAX` 模块：

- **重制（Remaster）**——向 live CD 上的 `/modules` 目录添加 `SLAX` 模块。将你的 `BackTrack` live CD 内容复制到硬盘上的一个目录，将 `SLAX` 模块添加到该目录，并重新创建 `ISO` 镜像（使用 `makeiso`）；当启动该 live CD 时，添加的模块中的软件就会被安装。

- **现场（Live）**——你可以在 `BackTrack` 运行时，下载任何 `SLAX` 模块并使用 `livemod` 命令进行现场安装。该模块中的软件将立即可以可以使用。

要找到适用于 `BackTrack` 及其他基于 `SLAX` 的 live CD 的可用软件模块，请访问 `SLAX` 模块页面 (`www.slax.org/modules.php`)。你会发现 15 类可以添加到你的 live CD 或在重制时添加到 `/modules` 目录的软件。要立即安装模块，找到你需要的软件（选择类别或使用搜索框查找你想要的内容）。然后下载你选择的模块。

当要安装的模块位于当前目录时，你可以使用 `livemod` 命令安装该模块。例如，你可以输入以下命令来安装 `eMovix` 程序包：

```
# elivemod eMovix_0_9_0
```
