
# Linux User & Developer 189 - 构建完美的网络

## 深度指南：内页精彩内容

![](img/301dc180ffb6e12d0783cd156737047_0.png)
![](img/301dc180ffb6e12d0783cd156737047_1.png)

电子边界基金会 (EFF) 是维护数字世界公民自由的领先非营利组织。成立于 1990 年，通过法律诉讼、政策分析、草根行动和技术开发捍卫隐私、言论自由和创新。随着技术使用的增长，我们确保权利和自由得到增强和保护。

## EFF.ORG 电子边界基金会

在电子边界保护并促进自由

# 欢迎阅读

Linux User 第189 期

**编辑**

Chloe Thorn `chloe.thorn@futureunet.com`

**设计**

Rosie Webber

**制片**

Ed Ricketts

**总编辑**

Graham Beckham

**资深艺术**

Jo Guiviller

**访谈**

Joy Beard, Neal Bothoth, Christopher Gayle, Alex Cole, Mark Hill, Tom Teagan, Simon Jones, Masters, Paul O'Brien, Calvin Robinson, Sheila Sutton

**广告**

按需提供媒体包。

广告请联系 Richard Hemming `richard.hemming@futureunet.com`

**客户总监**

Andrew Turnbull

**客户经理**

Richard Hemming

**客户总监**

Chris Crispson `cris@outlook.com` 01225 68735

LinuxUser 可授权。请联系许可部门获取更多合作机会。

国际总监 Martin Ellis `ellis@futureunet.com`

**订阅**

发送邮件至 `contact@futureunet.com`

在线订单或拨打 0800 666 8888

访问 `www.mylinuxuser.com`

**订阅负责人**

Steven Todd

**发行负责人**

Haytre Martins

**制作负责人 (US & UK)**

Chris Scarselle

**艺术总监**

David Green

**数字创意**

James Hudson

**制作助理**

Jan Jackman

**管理**

Aaron Sasaki

**编辑总监**

Paul Newman

**艺术与设计总监**

Richard Reading

**设计负责人**

Company

**印刷商**

Wyndhurst Publishing, Stoney's Road, Peterborough, Cambridge PE1SY

**营销**

Marketforce, City Place, Canary West, London E14HU

`www.marketforce.com`

# 本期内容

欢迎阅读英国和美国最喜爱的 LinuxUser 和开源（FOSS）杂志。我们在制作这篇关于用于灾难救援的开源网络（p34）时经历了一场地震。幸运的是，那只是里氏规模上的。但还有许多让我们兴奋的内容，比如我们设置了一个适用于高级家庭或小型业务的网络（p18）。

如果你关注安全和隐私，你将喜欢我们从零构建 Qubes OS 的指南（p60）。同时，在教程中，我们有关于 R 统计编程的独立入门；关于服务器固化的教程；而在 Pi 教程中，我们将邀请“ZeroPhone”本人，介绍如何按键监控你的 Pi 参数！！Chris Thorn, 编辑

**竞赛**

给我们写信即可赢一台 iTunes Dash Pro！

`linuxuser@futureunet.com`

Twitter: @linuxusermag

Facebook: facebook/LinuxUserUK

第11页查看更多详情

获取最佳订阅优惠：`myfuturelinuxuser.co.uk/subscribe`

本期订阅可节省高达 20%！见第30页

![](img/301dc180ffb6e12d0783cd156737047_2_0.png)
![](img/301dc180ffb6e12d0783cd156737047_2_1.png)

`www.futureunet.com`

首席执行官 Ethan Smyth

首席财务官 Patrick Leahy

电话：+44 2072633000

# 目录

![](img/301dc180ffb6e12d0783cd156737047_3_0.png)

# 开源专题

# 教程

# 开源

![](img/301dc180ffb6e12d0783cd1567376047_5_0.png)

## 由于稳定性和共享问题，Wayland 不再作为默认

由于对稳定性的抱怨，Xorg 更适合这项工作。

据报道，即将发布的 Ubuntu 18.04 LTS 'Bionic Beaver'（海羚海狸）将放弃 Wayland 显示服务器并恢复到 Xorg。桌面工程经理 Will Cook 在博客中解释说，系统将包含 Xorg 图形栈和基于 Wayland 的系统。然而，在一次巨大的反转中，他强调了 Xorg 将成为默认选项。

考虑到 LTS 版本拥有五年的支持寿命，因此它需要可靠地运行。Cook 列举了如 WebRTC、Google Hangouts 和 Skype 等屏幕共享服务；带有 RDP 和 VNC 的远程桌面；以及——

在探索前两者时，Cook 观察到 Wayland/GNOME 计划是使用 Pipewire 进行屏幕共享，这需要进一步开发。“在此之前，Xorg 可以独立于显示服务器重新启动。”

关于可恢复性，文中明确了 GNOME shell 在崩溃时可以“结束”其他进程的事实：“当使用 Xorg 时，shell 可能会崩溃，一旦 shell 重启，你就可以从离开的地方无缝接会话，你的应用程序仍在运行。”

虽然开源驱动程序运行良好，但涉及到游戏时，他们想要确保 Wayland 的稳定性是合情合理的。对于标准的桌面活动，专有驱动的可靠性较低，遗憾的是，它们在帧率、纹理等方面的性能要好得多。解决此办法是切换到 Xorg 并使用专有驱动。

Cook 补充道，这不仅仅是为了 Wayland。“在使用不会崩溃或导致架构崩溃的 shell 时也存在问题。对于这项进行中的工作有两个解决方案，我们将向即将推出的上游做出贡献。简而言之，我们仍然致力于 GNOME 和 shell，通过添加功能和修复漏洞来改进 Wayland。”

正如 Cook 所指出的：“Ubuntu 的体验需要是稳定的，并提供用户在日常生活中需要的功能……对于 18.04 LTS，我们将评估 Wayland 作为默认选项。”恢复到 Xorg 仅仅是 Wayland 最终被所有主流发行版接受道路上的一个小插曲。
