
# Linux 用户与开发者 188 - 系统虚拟化 188

![](img/47c577d3c443392bbdb486d8e17c4a70_1_0.png)

你知道吗？用于造纸和许多其他产品的欧洲森林在过去 10 年中增加了 44,000 平方公里？这相当于每天增加了超过 1,500 个足球场面积！†

`Two Sides`是一项促进负责任使用印刷和纸张的全球倡议。如果源自经过认证或可持续管理的森林，纸张是一种独特且强大的自然传播媒介。

有很多完美的理由让我们 `#热爱纸`。现在就发现：`twosides.info`

## 欢迎

阅读 `Linux User & Developer` 第 188 期

### 编辑部

`Chris Thorne`

`chris.thorne@linuxuser.com`

设计师 `Dean Webber`

制作编辑 `Ed Richards`

总编 `John Graham Barrow`

高级编辑 `Jo Gulliver`

**贡献者**

`Dan Ahmed`, `Michael Bedford`, `Jozy Maynard`, `Neil Backforth`, `David Elston`, `Steven Thomas`, `Tim Casillo Grona`, `John Mason`, `Martin Coleman`, `Rahman Mayash`, `Alexander Evans`

客户总监 `Andrew Trevor`

`steven@futuremedia.com`

客户总监 `Richard Colplin`

`richard.marketing@futuremedia.com`

![](img/47c577d3c443392bbdb486d8e17c4a70_2_0.png)

欢迎阅读这份英国和北美最喜爱的 Linux 开源（`FOSS`）杂志。

在 `Spectre` 和 `Meltdown` 的风暴中，我们必须向那些快速创建新功能以帮助用户免受这些漏洞侵害的人们致敬。这是一项值得庆祝的艰巨任务。在杂志的核心部分，我们需要这样的内容——专栏作家 `Jon Masters` 本月撰写了一篇深度专栏来应对这些漏洞。多么大的挑战！

在杂志的其他部分，我们希望让你的生活压力减轻，包括一份成为虚拟化高级用户的指南（第 18 页）——一篇关于档案保护的重要性以及如何防止小偷盗用科技设备的文章（第 58 页）。我们的主访对象是 `Nextcloud` 创始人 `Karl Fritzsch`，探讨 `Nextcloud 13` 中端到端加密的未来。

作为常设栏目，“`Practical`”重点介绍了 `Metasploit` 和 `Racket` 编程语言。在“`Practical`”中，我们有一些关于 `Rubber Duck` 破解的内容，并使用 `Numpy` 来保护你的 `Python` 代码。享受其中！`Chris Thorne`，编辑

发送邮件至：`contact@linuxuser.co.uk`

或电话订购：`0800 668 8888`

或短信订购：`87988 66888`

或在线订阅：`www.linuxuser.co.uk`

由 `Heatline Masters` 发行

由 `US & UK Craft` 

项目经理 `Scott Marshall`

设计总监 `James Edwards`

数字内容 `James House`

**管理**

执行董事 `Aaron Asadi`

执行董事 `Paul Newton`

艺术与设计总监 `Ian Jervis`

`Waterberbury, Station's Road`

`Cambridge, CB1AE`

`Market House, Canary Wharf, London E14`

`LinuxUser` 是一本免费杂志。本期杂志由 `International Licensing Limited` 的广告和赞助支持。未经 `Future PLC` 的书面许可，`Future PLC` 在英格兰和威尔士注册（公司号 `02791433`）。注册地址：`25 Canada Square, London, E14 8AD`。`Future PLC` 对本期的任何错误或不准确之处负责。文中观点不一定代表 `Future PLC` 的观点。我们对广告中包含的任何内容负责。保留所有权利。

- `lux@futuremedia.com`

- `facebook.com/LinuxUser`

- `Twitter @linuxusermag`

`futuremagazines.co.uk`

纸质版可节省高达 20%！详情见第 30 页。

![](img/47c577d3c443392bbdb486d8e17c4a70_2_1.png)

## 编辑

首席执行官 `Elizabeth Bryan-Smith`

首席财务官 `Leslie-Duncan`

电话 `+44 20 734 6000`

3

![](img/47c577d3c443392bbdb486d8e17c4a70_3_0.png)

![](img/47c577d3c443392bbdb486d8e17c4a70_3_1.png)

![](img/47c577d3c443392bbdb486d8e17c4a70_3_2.png)

## `InspireOS`

第 188 期 2018

## `Practical` 树莓派

## 封底

- 68 树莓派项目：`Peter Monaco` 解释了他如何基于树莓派制作了自己的家庭自动化控制触摸屏，包括仅需少量脚本即可实现的“`Rubber Duck`” `USB` 黑客设备

- 96 顶级开源项目：今年范围内范围内全球的软件

- 81 分组测试：轻量级 Web 服务器：对于我们不需要全服务器的人来说，这四种中哪个表现最好 |

- 70 远程硬件设备：只需少量脚本即可将你的树莓派变成基于 `USB` 的“`Rubber Duck`”黑客设备

- 86 `Varideisk Pro Plus 36` 黑色：人体工程学立学桌承诺各种健康好处。我们需要对这款昂贵的设备进行测试

- 74 温度显示：结合 `LED`、触摸按钮和传感器读数

- 88 `ReactOS 4.7`：一种为 `Windows` 美学设计的操作系统……等等！这个非 Linux 系统有很多

- 78 Python 者的剃刀：想要提高 `Python` 代码的性能吗？使用 `Numpy` 加速——无论选择如何

- 90 新鲜 `FOSS`：`Flickr` 客户端 1.4、媒体播放器 `mpv 0.28` 以及图像编辑器 `Fotox 18.01`

![](img/47c577d3c443392bbdb486d8e17c4a70_4_0.png)

![](img/47c577d3c443392bbdb486d8e17c4a70_4_1.png)

![](img/47c577d3c443392bbdb486d8e17c4a70_4_2.png)

![](img/47c577d3c443392bbdb486d8e17c4a70_4_3.png)

![](img/47c577d3c443392bbdb486d8e17c4a70_4_4.png)

![](img/47c577d3c443392bbdb486d8e17c4a70_4_5.png)

![](img/47c577d3c443392bbdb486d8e17c4a70_4_6.png)

![](img/47c577d3c443392bbdb486d8e17c4a70_4_7.png)

![](img/47c577d3c443392bbdb486d8e17c4a70_4_8.png)

### Linux 受到 `Meltdown` 和 `Spectre` 安全漏洞的影响

无论是 `Intel` 还是 `AMD`，所有系统都面临风险，且补丁过程可能非常痛苦。

`Meltdown` 和 `Spectre` 因其是过去 20 年来发现的最严重漏洞而成为全球头条。如果你使用的是过去 20 年内制造的 `CPU` 的设备，那么你几乎肯定受到了影响。整个 12 月关于 `Intel CPU` 问题的传闻不断传出，其可能产生的影响规模是无法预测的。更波折的是，由于一个“兄弟级”漏洞，甚至 `AMD`（以及某些 `ARM`）`CPU` 也与 `Spectre` 一起面临风险，这很显然表明这是一个真实的威胁。`Spectre` 利用了 `CPU` 中乱序指令执行的一个漏洞。这在本质上是 `CPU` 在等待从 `RAM` 接收大量数据时，继续处理少量数据（乱序执行）的一种方法。如果有必要，必须丢弃已经处理的数据。

![](img/47c577d3c443392bbdb486d8e17c4a70_5_0.png)

`Meltdown` 最初由 `Google Project Zero` 在 2017 年年中发现，并被另外两组研究人员独立检测到。通过利用推测处理数据与检查之间的延迟，研究人员发现可以在没有密码或加密密钥的情况下读取内核，且虚拟化并不会产生影响。

`Intel` 和 `AMD` 芯片以及 `ARM` 处理器都受到了影响。对于攻击者来说很难实现，但防御也同样困难。`Spectre` 强制通过推测执行泄露数据；研究人员已通过原生代码和 `JavaScript` 实现这一点。
