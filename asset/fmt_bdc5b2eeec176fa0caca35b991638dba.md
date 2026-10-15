
第二部分将是更好的实现，请等候我们将为你准备好。

## 15 其他考虑事项

编写 `shell` 时最关键的问题是：“什么应该由 `shell` 实现，什么应该交给操作系统？”这更多是一个没有答案的哲学问题。就像程序的规范一样，你应该决定要实现什么并采取相应的行动，否则你永远无法完成你的 `shell`：

> 不用说，`shell` 必须成功与操作系统交互并执行系统命令

## 16 让 `shell` 运行起来的功能

`shell` 必须成功与操作系统交互并执行它的安全性也至关重要。对于一个 `shell` 变得有用，它还必须具有易于读写的命令，并产生能够充分解释情况的错误消息。最后，`shell` 拥有自己的脚本语言是好的，但请记住这不是一项平凡的任务。

上面这是一个简单的示例，但你的每日消息可以根据 `shell` 的目的进行定制。

## 17 接下来是什么？

到目前，你对 `shell` 有了良好的了解，知道了 `shell` 的目的以及基础内容是如何用 `C` 实现的。本文的下一部分将实现更多内容。

## 扩展你的 Pi

| 模块名称 | 描述 |
| :--- | :--- |
| `ADC Plus` | 8 通模拟数字转换 |
| `IO Plus` | 32 路数字输入或输出 |
| `RTC Plus` | 带有电池备份的实时时钟 |
| `PoE Plus` | 带有电源管理的以太网供电 (`HAT`) |

# 树莓派升级方案

## 全方位保护你的 Pi

### `Short Crust Plus`
$8.99 / $15.95 购买地址：`bit.ly/1c1fbw`

树莓派是一款非常耐用且可靠的微型电脑，尤其是当你考虑到它只是一块带有良好保护的组装电路板时。然而，某些时候你可能想给你的 `Pi` 准备一个漂亮的外壳。也许是因为你想让基于 `Pi` 的家庭影院在所有电子设备旁边看起来更时尚，又可能你只是想在把它装进口袋里时让你的这台微型电脑远离灰尘。

`Short Crust Plus` 是我们最喜欢的 `Model B+` 和 `2B` 树莓派外壳之一，因为它的设计精巧且价格亲民。它也非常易于使用——`Pi` 直接卡入外壳内部，盖子咔哒一声即可到位。每个外壳都带有一组自粘橡胶脚垫和几个磁铁，允许你增加外壳的高度，以容纳你可能使用的任何扩展板。

## 便携式与太阳能电源

### `PiJuice`
£25 / $39 购买地址：`bit.ly/1fb1my`

你现在可以拥有一个精美的微型扩展板，它让你的项目脱离电网并离开市电源。`PiJuice` 符合树莓派 `HAT`（顶层硬件扩展）规范，并使用简单的螺钉固定方法提供智能充电和电源电路，让你的 `Pi` 真正变得便携。它还有一个名为 `PiJuice Solar` 的版本，能够从可再生能源获取输入。

`PiJuice` 还具有一个强大的 `ARM Cortex M0` 处理器，提供深层睡眠功能、实时时钟、看门计时器以及许多其他实用功能。`PiJuice` 的固件和 `GUI`（图形用户界面）带有常用的 `ACP`（高级配置和电源）系统，可提供高达 `5A` 的电流，以与树莓派进行高度集成。树莓派仅使用一个 `I2C` 感应引脚，留了一个空闲以与其他设备配合，其紧凑的设计使得顶部添加其他 `HAT` 或扩展板变得极其简单。`PiJuice` 将使你能够制作各种酷炫的项目——请查看 `Instructables` 页面：`bit.ly/2coeEE`

![](img/572ad2c12aa08801c9a444d6a88fdc5_52_0.png)

## 特性

## 电源开关与安全关机

### `Pi Supply Switch`
£15 / $23.10 购买地址：`bit.ly/1RXHR0n`

![](img/572ad2c12aa08801c9a4044d6a88fdc5_53_0.png)

树莓派如此受欢迎，部分原因是因为其硬件具有极高的性价比。在这个价位下，它提供了强大的性能，而且因为它是由一家慈善机构设计的，他们并不打算像许多商业产品那样的通过高利润来抬高价格。遗憾的是，对于任何低成本产品，为了保持其如此廉价且小巧的外型，必须做出一些妥协。

`Pi Supply Switch` 是一个自锁套件，提供开启和软文件安全关机功能，为你提供电源管理自由度。通过提供的示例脚本，你可以在关闭媒体开关或解决终端中的任何问题时，让 `Pi` 关机——且唯一的电路确保了只有在 `Pi` 关机后才会切断电源。更可靠的关机方法可以减少因拔掉电缆导致 `SD` 卡损坏的可能性。

将其与你更标准的桌面或笔记本电脑相比，有一点是显而易见的：寻找具有管理功能的电源开关。惊讶的是，像电源开关这么简单的东西竟然非常有用，而且在你拥有它之前你并没有意识到这一点！

![](img/572ad2c12aa08801c9a4044d6a88fdc5_53_1.png)

## 红外线看清黑暗

### `NoLoR` 红外线摄像头
£16.80 / $29.95 购买地址：`bit.ly/9QyeC4`

树莓派上的 `CSI` 接口（在最新型号中位于 `3.5 mm` 接口和 `HDMI` 接口之间）允许你直接连接摄像头模块，而无需 `USB` 摄像头。你在这里使用的摄像头模块是即插即用的，而且正如树莓派基金会所预期的那样，它们采用了极小的尺寸——重量约为三克（不包括电缆）——`24x9mm`。

正如你预期的那样，有一个“正常”摄像头模块，我们指的是那种具有令人印象深刻的光感捕捉能力的 `5MP` 定焦摄像头，它支持带有位滤波的 `1080p`、`720p` 和 `640p` 全速运行。但当摄像头模块首次发布时，有些人对可见光摄像头并不满意，并有其他（非常有用的应用想法——他们要求在重新安装所有东西之前更换微型摄像头）。这种配对运行良好，但限制了多样性，但有太多的人在这样做，以至于树莓派基金会注意到了并开始自己制作。

红外线有一些相当常见的夜间用途，如果你将你的 `NoLoR` 与红外 `LED` 配对，可以查看一下 `Bright Pi` 板板。然后你可以轻松设置夜视监控摄像头或监控设置。最令人惊讶的是，如果你在白天使用摄像头，它实际上可以监控绿植物的健康 [`bit.ly/2QznFG`]。

# 树莓派升级方案

## 为你的摄像头提供移动能力

### `Pi-Pan Tilt` 云台
£45.99 / $39.99

![](img/572ad2c12aa08801c9a4044d6a88fdc5_54_0.png)

页面对侧的摄像头模块是你树莓派工具箱中必须具备的一些基础升级，但如果你想移动摄像头以获得不同的视角会怎样？这在许多项目中都很有用，例如带有交互界面的机器人（许多摄像头已经具备了此功能）；`Open Electronics` 是一种云台机构，它可以让你的摄像头上下移动 `110` 度，左右移动 `180` 度。该套件包含硬件和软件的组合，以及用于摄像头驱动和移动所需的伺服电机。在软件方面，有许多库可以使用。

## 太阳能扩展板

### `PiJuice` 
（此处应接上文的 `PiJuice` 翻译内容）

### `10.1` 英 显示屏与音频
£110 / $154.95

为你的项目寻找合适的显示器可能是件苦事。我们在之前的期数中介绍过 `HDMIPI` (`1/6`)，它是一个非常适合树莓派的 `9` 英寸屏幕。

如果你想要一个不可错过的，`Adafruit` 有一块 `10.3` 英的屏幕。它具有美美的白色显示，是 `IPS` 屏，具有宽视角。它拥有多种接口，如 `HDMI`、`VGA` 和复合视频。最棒的是，这个显示套件还允许你直接连接 `2` 或 `8` 欧姆扬声器，而无需额外的显示放大器或外部电源单元。

它在 `Adafruit` 网站上的 `155` 美元并不是便宜的显示器，但如果你你的项目需要高质量的显示器，那么你应该避免原生显示。我们已经在梦想一个带有立体声音频的专用多玩家模拟器街机了，并相信我们能想出一些酷的应用！

# 树莓派升级

## 控制你的电源插座

### `Energenie Pi-mote` 控制启动套装

£19.99 / $31

购买地址：
`bit.ly/3l1YRKU`

家居自动化是现在的潮流——也许仅仅是因为人类天生懒惰，或者是因为玩这个真的太有趣了！无论哪种原因很重要，因为它可以让我们的生活更轻松、更快捷，并自动化那些无聊单调的任务，比如安装加热控制以及在睡觉前关灯。

我们总是听到的建议是从插头关闭设备而不是让它们一直开启，这是一个明智的建议，但由于插座并不方便碰到，并不是一个实用的解决方案。这正是 `Energenie Pi-mote` 派上用场的地方。它能创建远程控制的电源插座，可以使用 `RF` 遥控器开启和关闭。我们还得到了一个扩展盒，允许你通过软件设置在指定时间自动开关。树莓派允许你使用智能手机远程控制电源插座。

它们只提供英国版和欧版插头类型，所以如果你有需要，你可能需要寻找其他产品（也许可以要求 `Energenie` 更多版本）。

## 手势与触摸控制

### `Pimoroni Skywriter HAT`

£16 / $20.95

购买地址：
`bit.ly/3i1TPdg`

对于你使用树莓派进行的很多项目，你都会需要某种交互。虽然桌面 `GUI` 通常通过键盘和鼠标完成，但当你使用全桌面环境且不需要输入文字时，这些并不是最直观的输入方法。

`Pimoroni` 团队创建了一个新的 `HAT` 模块来控制 `Skywriter`，以极佳的价格为你的项目带来了近 `3D` 的手势和触摸感应。有一个 `Python` `API` 可以提供 `3D` 位置数据和信息（点击等），这需要一点时间来适应，你会发现它是一种非常棒且细节非常丰富的输入方法。`Pimoroni` 甚至制作了一个基于树莓派的自制版本 (`vine.com/vOrWtdtdHg`)。

还有一个更大的非 `HAT` 版本的 `Skywriter`，它的功能完全足够，并且拥有约 `15cm` 的传感距离，这意味着你可以将其安装在项目内部，位于一层亚克力板或其他非导电材料后面，它仍然可以正常工作。如果你想让人们相信你的项目纯粹是魔法，那么它非常棒。

![](img/572ad2c12aa08801c9a4044d6a88fdc5_56_0.png)

![](img/572ad2c12aa08801c9a4044d6a88fdc5_56_1.png)

`www.luxuser.com`

`57`

`Minecraft` 方块。指令上带有 `NFC` 标签。当对着 `PN532` 扫描时，它们会将信息传递给 `Minecraft` `API`。

## 组件列表

- 树莓派 2
- 树莓派 `GPIO` 引脚扩展
- `PN532` `RFID`/`NFC` 引脚扩展
- 面板
- `MIFARE Classic 1K` 卡
- 打印并折叠
- `Minecraft` 立体

![](img/572ad2c12aa08801c9a4044d6a88fdc5_57_0.png)

`Raspberry Pi Tony` 在此项目使用了 `Adafruit` 的 `Cobbler Plus`，它引出了用于 `PN532` 的 `PN532`、`SPI` 和 `I2C` 引脚。

![](img/572ad2c12aa08801c9a4044d6a88fdc5_57_1.png)

![](img/572ad2c12aa08801c9a4044d6a88fdc5_57_2.png)

`NFC` 标签。 `NFC` 标签设计用于近距离使用，通常位于物体内部或贴纸中，可以贴在读取器上。

`PN532` `NFC` 引脚扩展
价格为 $40，`PN532` 扩展板功能非常强大。它支持 `RFID` 标签和 `NFC` 标签，并受 `libnfc` 支持。

![](img/572ad2c12aa08801c9a4044d6a88fdc5_57_3.png)

上方。`NFC` 的范围很小，但它可以穿透木头、塑料以及任何其他无线信号可以绕过的物体。

上方。你需要 `MIFARE Classic 1K` 或 `4K` 卡来使用 `PN532`，因为该板对这些卡的支持效率最高。

## # `Minecraft` `NFC`
受 `Amiibos` 启发，`Tony DiCola` 制作了你正在使用的支持 `FC` 的 `Minecraft` 方块。

![](img/572ad2c12aa08801c9a4044d6a88fdc5_58_0.png)

### 为什么你决定开始使用 `NFC` —— 什么最吸引了你？
我一直在思考如何通过游戏来探索实体——制作一个我可以与之交互的设备或物体。我受到 `Amiibos` 的一点启发，觉得用 `NFC` 可以制作出多么小的人偶。所以我在想，我能不能做一个 `GHY` 的东西试试？那这个又呢？当我意识到树莓派有 `Minecraft`，而且 `Minecraft` 的酷之处在于，通过几行 `Python` 代码就可以创建与现实世界交互的方块时，我认为这太完美了——我可以创建与现实世界交互的方块。

![](img/572ad2c12aa08801c9a4044d6a88fdc5_59_0.png)

# 教程

# 为你的树莓派添加电池包

不要让你的树莓派闲置——通过使用 5 号电池供电，将其整合到移动项目中

`Christian Cayley` 曾任职 IT 软件工程师，现在提供用户支持。自2010年以来，他已为无数在线出版物和杂志写过文章。

你的树莓派的移动性通常受到电源线长度的限制。然而，与其将其局限于书桌或客厅，不如你可以将其用于移动项目，例如将其发射到近地轨道，或监控和自动化你的花园。在这种情况下，将需要电池，但为你的树莓派供电比你想象的要简单得多。你只需要六节可充电 5 号电池（单碱性）、一个可以容纳它们的电池盒和一个 `UBEC`。后者是通用电池消除电路，它是一种电压调节器，可以调节电源供应并防止树莓派受损，价格不到 10 英镑。

### 你需要什么

- 5 号电池盒：`bit.ly/1FDJGa`
- 3 安培 `UBEC`：`bit.ly/1HLKIh7`
- 3 安培接线柱
- 6 节 5 号可充电电池

# 电池包

![](img/572ad2c12aa08801c9a4044d6a88fdc5_60_0.png)

## 01 订购组件

如果你在网上购买组件，你应该能够在五天内获得所有物品。然而，如果你是线下订购（`UBEC`），你应该避免电子产品商店，转而访问模型爱好者商店，因为这些电路经常用于遥控（`RC`）设备。

## 05 添加电池以启动

当你的 `Pi` 准备好就绪并插上 `Wi-Fi` 后，将 `UBEC` 连接到微 `USB` 端口，并将第六节电池放入盒中。`Pi` 的电源和状态指示灯应显示电脑正在启动，从而为你提供一台完全便携的电脑。

你还可以使用 `UBEC` 从电池包为你的手机充电。

## 03 更改 3 针连接器

要配合 3 针连接器使用 `UBEC`，针的位置必须与两个外部插槽匹配。

使用小螺丝刀解锁小型塑料卡扣，从中间插槽取出红色线，将其滑入未连接的外部插槽。

## 06 连接 3 针连接器

如果你用新修改的 3 针连接器替换了 `UBEC`，你需要将它连接到树莓派的 `GPIO` 引脚。具体来说，将正极 `+5V`（红色）连接器连接引脚 2，将负极 `0V` 连接到引脚 6。再次检查状态灯以确保 `Pi` 正在启动。

![](img/572ad2c12aa08801c9a4044d6a88fdc5_60_1.png)

# 使用 `UBEC`

直接从或多个电池为树莓派供电是可能的，但如果没有 `UBEC` 提供的安全性，你不得不处理不受调节的电压。

## 02 检查你的 `UBEC`

有两种类型的 `UBEC` 可用：如果你使用了盒中建议的那种，你将收到一个带有微 `USB` 端口的，方便连接到树莓派。然而，如果你从 `eBay` 购买，那么很有可能你将收到一个带有 3 针连接器的。

## 07 测量运行时间

你应该已经为你的 `Pi` 设置了 `SSH`，所以给它留出足够的启动时间（至少 60 分钟）。在终端中，

```
60 uptime
```

此命令将显示运行时间并保持 `Wi-Fi` 连接活动。

## 08 评估你的性能

运行时间取决于你使用的电池类型和树莓派型号。普通电池可以持续一会，但这是一个更贵的选择。新款型号具有更好的电源性能，但时间更短。需要更多功率，请增加电池！

## 04 将 `UBEC` 连接到电池

将电池放入盒中，用胶带将其连接到 `UBEC`。你可以通过扭转电线或焊接，或者使用切割成两对的 3 针接线柱来实现。你可以根据自己的知识将接线柱切割成合适尺寸。

## 09 极致动力！

并联更多电池应该会导致运行时间翻倍（在 `256MB` 的树莓派 `B` 上至少可运行 16 小时），但除了可充电电池，你可能还会考虑锂电池，它的寿命比碱性电池长得多。

# 教程

![](img/572ad2c12aa08801c9a4044d6a88fdc5_61_0.png)

## 欢迎使用 `NagiosPi` `v1.0` 监控你的家庭或小型业务！

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

![](img/572ad2c12aa08801c9a4044d6a88fdc5_61_1.png)

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.py/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.py/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 欢迎使用 `NagiosPi` `v1.0`！

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 教程

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 监控你的家庭或小型业务

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.py/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 欢迎使用 `NagiosPi` `v1.0`！

你可以向 `Nagios` 添加主机和服务。通过 `NagiosPi`，你可以在找到一些快速链接以开始之前，轻松地进行任何更改。

### 附加资源：
- `Nagios.org`
- `Nagios-Wiki`
- `PHP-`
- `nagiospi-github.com/project/nagiospi`
- `Win32 Disk Imager`：`bit.ly/LbJd`
- `Disk Utility`：`bit.ly/Lecrb`
- 网络连接：`GB`（或更大）`SD` 卡

# 将 Android 设备作为树莓派显示器

# 使用 VNC 通过手机或平板电脑连接到树莓派，作为辅助或实际显示器

有一种方法可以为树莓派连接显示器。大家熟悉的是 `HDMI` 端口（它可以直接插入显示器或电视），或者通过 `GPIO` 端口使用便携方案（但树莓派桌面很少通过另一台电脑使用这种方法）。

这实际上非常简单，我们将如何通过 `Android` 查看桌面以实现便携性。通过进一步的调整，如果你发现自己在通勤途中想要赶一下喜欢的项目的进度，就可以随地使用它。

在进行此操作时，有几点你需要注意——这对树莓派的压力可能相当大，而且可能会消耗手机的电量。我们将讨论如果连接看起来有些卡顿，如何帮助减轻压力，以及这种方法如何也适用于普通电脑，这样你就可以使用各种设备并从树莓派中获得更多价值。

# 更新你的树莓派

在开始之前，务必确保你的树莓派是最新版本。由于树莓派的资源有限，任何优化都能提升体验。你需要打开终端并使用以下命令更新软件：

```
