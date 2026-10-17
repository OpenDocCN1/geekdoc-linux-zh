
![](img/f96eeeb05685565f9f67cf36c9ea3ae1_62_1.png)

# 结尾

`GPG` 的最新版本将密钥的默认寿命从两年进行了更改。在你的密钥过期后，你可以更改此设置并让它们复活，但提前掌握这个核心技巧是个好主意。为什么呢？

首先，响应日历提醒中关于保护密钥寿命的这一简单行为，会让你重新考虑加密、隐私和安全。你数字生活中没有哪个关键部分是长期无法持续的；如果出现问题且你丢失了私钥，你至少知道损害只会持续有限的时间。

# 撤销密钥

仅仅信任证书会对恶意攻击者自动过期是有风险的，你还需要一个撤销证书。`GPG` 在这方面可以帮助你，因为你可以用私钥生成它。一旦你撤销了密钥，世界就会知道不要信任它，而且它是无法被再次撤销的。

将你的撤销证书存放在安全的地方，例如保险箱或银行的保险箱。撤销证书非常重要：请妥善对待。

# 友好的前端

除了签名和加密密钥外，你还可以对特定文件的区域进行签名或加密。如果你正在编辑，可以选择或签名一个 `GPG`，`GNUS` 将使用你系统的 `GPG` 打开对话框来运行文件，而不是类似 `Emacs` 的 `demise` 视图。`Emacs` 也处理密钥的导入和导出。

# 功能

## 加密

### 详解加密技术

驱动你的加密和隐私的应用、库和协议。了解 `OpenSSL` 和 `OpenSSH` 的区别，并建立一个 `OpenVPN` 连接。

有时，感觉我们都淹没在缩写词的海洋中，甚至是极其相似的内容也无法区分。如果你不确定 `OpenSSL`、`OpenSSH` 甚至 `OpenVPN` 之间的区别，那么这正是你需要的。这三个标准或技术的共同点是，它们都用于在任何网络（包括互联网）上保护数据，这私钥以及加密流量（还有一个足够可怕的 Logo 和 `OpenVPN`）。

`Google` 分叉了代码以产生 `BoringSSL`，旨在避免此类问题，而 `OpenSSH` 是一个核心被称为 `SSL` 的操作系统。`OpenBSD` 的开发者正在修剪那些数千行的代码。

`OpenSSL` 实现了 `SSL`（安全套接层）和 `TLS`（传输层安全）协议，它们出现在浏览器的地址栏中，但也用于许多地方，包括电子邮件。在电子邮件的情况下，它们用于“握手”以交换密钥并验证连接——至少理论上是这样。

然而，`OpenSSL` 有一个严重问题，在于其代码的规模和复杂性。`Heartbleed` 只是项目中未被撤销的漏洞之一，它也暴露在安全隐患中。如果你没有使用在线 `VPN`，但想为你的家或办公室建立安全连接，设置 `OpenVPN` 实际上很容易的——这是 `BBC` 网站上最流行的教程之一，展示了如何在树莓派上进行设置。

如果你担心安全，`Softmaker` 提供了一种替代方案，尝试多种协议，包括通过 `HTTPS` 隧道来欺骗攻击者。

## 一小撮盐 (Salt)

## 通过 OpenVPN 连接隧道

`NaCl`（网络与加密库——'salt'）是来自多伦多大学研究人员的网络和加密库。开发者们专注于安全性，并且其安全性足够快速使用。易用性也是一个问题，提供了简单的上层接口——而不是复杂的 `C` 和 `Python` 选项。由于互联网是一个安全的地方，它拥有 `SSH`，用于在远程计算机上运行 `Shell`，可能是最著名的工具。

`OpenSSL` 实现了 `SSL`（安全套接层）和 `TLS`（传输层安全）协议，它们出现在浏览器的地址栏中，但也用于许多地方，包括电子邮件。在电子邮件的情况下，它们用于“握手”以交换密钥并验证连接——至少理论上是这样。

如果你没有使用在线 `VPN`，但想为你的家或办公室建立安全连接，设置 `OpenVPN` 实际上很容易的——这是 `BBC` 网站上最流行的教程之一，展示了如何在树莓派上进行设置。

如果你担心安全，`Softmaker` 提供了一种替代方案，尝试多种协议，包括通过 `HTTPS` 隧道来欺骗攻击者。

## 功能加密

## 隧道传输的新方式：WIREGUARD

`WireGuard` 是一种安全的网络隧道，运行在第 3 层，并实现为 `Linux` 的内核网络接口。它旨在大多数用场景下取代 `IPsec`，以及像 `OpenVPN` 等流行的用户空间/`TLS` 解决方案，同时变得更安全、更高效且更易于使用。

`WireGuard` 在不到一年前发布了“0 版本”，因此在达到 `1.0` 之前，它还不是你个人应该使用的东西，但我们已经迅速看到 `WireGuard` 是安全且快速的。无论 `VPN` 是否如人所意，它都是一种针对当前隐私工具范式的不同方法。

`WireGuard` 摒弃了 `VPN` 构建在 `IPsec` 或路由网络上的假设，而是通过使用加密密钥（`CryptoKey`）构建小型且易理解的协议。

代码库非常小，第一个版本仅有 `3904` 行代码，而 `OpenVPN` 则超过 `100,000` 行。由于没有对 `OpenSSL` 的依赖，它的方法变得如梦似完美。这段代码实现在 `Linux` 内核中，较小的体积使其易于审计。

`WireGuard` 中的每一个部分都经过了重新思考，从提供清晰度并提供简单管理的“加密密钥路由表”，到它使用的方式：

![](img/f96eeeb05685565f9f67cf36c9ea3ae1_65_0.png)

## WIREGUARD 快速、现代、安全的 VPN 隧道

身份，并通过状态转换瞬时运行。

对于终端用户和系统应用程序，一个简单的原则就是直接使用它。`WireGuard` 是一个标准网络接口，因此你熟悉的 `iptables` 命令可以配合使用。`GUI` 应用程序使用相同的接口，它们允许

`WireGuard` 有一个私钥、一个 `UDP` 端口和一个对端列表。它没有允许 `IP` 列表。加密不包含协议框架，而是 `ChaCha20`、`Curve25519`、`Poly1305`、`BLAKE2s`、`SipHash24` 和 `HKDF`。同时，算法不会被锁定。

`OpenSSH` 可以带外处理密钥，这再次保持了代码库的简洁，并允许 `WireGuard` 连接到它职责范围内。参见 `James` 的 `FOSDM`，文章见：`https://fosdom.com/2017/schedule/event/wireguard/`

`WireGuard` 提供了一场非常有用的演示，如果你想了解更多关于 `WireGuard` 的信息，我们推荐他的 `https://wireguard.org/wireguard.pdf`；并阅读白皮书（`https://wireguard.org/wireguard.pdf`）。

代码尚未准备好发布 `1.0`，但我们建议尝试一下。像我们一样，这样的 `WireGuard` 项目可能成为加密领域的乐观未来 █

## 隐私与 GPG 生活方式

如果这看起来工作量很大，那么现状的退化为开源领域带来了改进。不要迷失，如果你把隐私视为理所当然，你可能已经不再拥有它，只有通过公民意志，我们才能看到周围公司和政府对数据侵蚀的回溯。设置虚拟专用网络（`VPN`）需要基础设施或至少一个商业 `VPN` 服务，但如果你经常使用咖啡店或安全 `WiFi` 网络，这可能更多是一种安全措施。

如果你出于某种原因处理事务，你可能想向你的客户展示加密保护。其他人加入了另一支 `GPG` 公民军队来保护他们的电子邮件。如果你真的在寻找帮助，请寻找当地的聚会。在英国，`Open Groups`（相当于美国的电子前沿基金会）举办加密派（`Crypto Parties`），许多非技术用户参加以了解更多隐私问题。

最重要的是，尽尽全力。

![](img/f96eeeb05685565f9f67cf36c9ea3ae1_65_1.png)

关于：志愿者们排队参加 `Together` 的对，在曼彻斯特中央图书馆的加密派上使用加密数据

## 针对北美读者的特别优惠

## 7 期完全免费

当你订阅时
每期都赠送免费资源下载

`7.04` 特刊 | `13` 页综合报告

面向专业人士和开发者的开源权威杂志

# LinuxUser & Developer

`GNU` 世代打造的必备杂志

`www.linuxuser.co.uk`

加密你的生活 下一代加密工具

信息安全特刊 | `DVD` 包含 `3` 个发行版

`LinuxUser & Developer`

构建完美网络

`LinuxUser & Developer`

锁定你的系统

深度 `MySQL 8` 释放新功能的威力

漏洞详解

你的免费 `DVD`

# UBUNTU 17.04 启动包

`Ubuntu 17.04` 附带 `Ubuntu Beagle (LTS)` & `Ubuntu 16.04 LTS` - 加密你的生活套装

服务器监控 监控工具

`Linux` 云端 `CMS` 工具

网络设备

监控设备

`ALEXA`

`5` 个轻量级发行版

购买 `4` 个发行版赠送免费 `DVD`

`LinuxUser & Developer`

访谈：在 `CA` 案之后 `Black Duck Linux`：意料之外的前景

内附：完整的 `UBUNTU 17.04` 报告 解释所有新功能 服务器端与开发者焦点

构建 `VR` 配置：使用 `Docker` 和 `Python` 创建虚拟环境

容器

免费越狱

`LinuxUser & Developer`

征服云端

最佳 `VPN`

`Web` 服务器

冷存储

`Manjaro 17`

重塑：新版本带来了新高度

内附：可信的 `Linux` 与 `64` 位

## 教程

# 使用 Python 在 Minecraft 中编写新创意

![](img/f96eeeb05685565f9f67cf36c9ea3ae1_71_0.png)

直接通过 `Python` 接入 `Minecraft`，并使用 `Forge` 模组制作出惊人的创意

![](img/f96eeeb05685565f9f67cf36c9ea3ae1_71_1.png)

`Calvin Robinson` 担任教育领域的计算顾问，教授 `GCSE` 和 `A-level` 课程的计算机科学，帮助伦敦各学校提供高标准的课程。

![](img/f96eeeb05685565f9f67cf36c9ea3ae1_71_2.png)

## 你需要准备

- `Minecraft`
- `http://www.mojang.com/games`
- `Python`
- `https://www.python.org`
- `MCpiFoMo`
- `http://rogerthaat.co.uk/MCpiFoMo.rar`

![](img/f96eeeb05685565f9f67cf36c9ea3ae1_71_3.png)

有时候，`Minecraft` 看起来不仅仅是一个游戏。它是一个不可思议的创意工具，通过使用红石和 `Minecraft` 方块，你可以创造出神奇的世界。我们更进一步，允许你使用 `Python` 代码控制 `Minecraft`。为什么要这么做？`MCP` 是由 `https://mcpy.python.com` 的 `'flap'` 和 `'bluepiRabbit'` 开发的，用于简单的 `API` 在树莓派上连接 `Minecraft` 和 `Python`。

通过使用 `Forge`，我们整合了一个包，允许在零售版 `Minecraft` 中使用 `Python`。我们使用了由 `Alexander Press` 开发的 `Raspberry Jam`，这是一个实现了大部分 `Raspberry/Pi` 功能的 `Minecraft` 模组。

从 `MCpiFoMo` 解压出新的 `minecraft` 目录进行覆盖，并从你的备份中复制 `Saves` 目录。如果你有备份，使用 `cp -r ~/minecraft-backup ~/minecraft` 将 `minecraft` 目录复制到新目录。

![](img/f96eeeb05685565f9f67cf36c9ea3ae1_71_4.png)

备份你的 `.minecraft` 目录。从 `MCpiFoMo` 复制已模组化的安装文件。

![](img/f96eeeb05685565f9f67cf36c9ea3ae1_71_5.png)

## 02 以模式启动 Minecraft

像往常一样启动 `Minecraft`，登录后，选择 `Forge` 模式。这将加载 `1.11` 版本的 `Minecraft`。如果你愿意，可以玩最新版本的 `Minecraft` 并安装更新后的 `Forge`，但我们已经了与 `Raspberry Jam` 兼容性最好的版本。

你需要运行带有预安装 `Forge` 配置的 `Minecraft 1.8` 版本。（此处原文可能有笔误）

当你看到窗口左下角出现数字时，说明你运行正常。在创造模式下创建一个新的平坦世界（`flat world`），并使用 `Python` 开始编写代码。我们在 `MCpiFoMo` 中预装了“平坦（`Flat`）”世界类型。

![](img/f96eeeb05685565f9f67cf36c9ea3ae1_71_6.png)

## 01 替换你的 minecraft 目录

替换主目录下的 `.minecraft`。如果你使用的是 `GUI` 界面，可能需要按 `CTRL+H` 来显示隐藏目录。在终端中使用 `mv ~/.minecraft ~/minecraft-backup` 封足够。

## 03 Hello World - 实现变化功能

使用你喜欢的文本编辑器，你需要创建一个新的 `helloworld.py` 文件并将其保存到 `~/minecraft/mcpipy`。

# # Minecraft

![](img/f96eeeb05685565f9f67cf36c9ea3ae1_72_0.png)

![](img/f96eeeb05685565f9f67cf36c9ea3ae1_72_1.png)

你可以通过一个简单的 `for` 循环创建一个满水的玻璃甜圈

```python
