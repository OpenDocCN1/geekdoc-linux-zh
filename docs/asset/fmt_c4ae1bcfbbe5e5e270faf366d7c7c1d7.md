
# FOSSLIFE

面向所有人

新闻 • 职业 • 科技生活

技能 • 资源

FOSSlife.org

# 创空间 (MakerSpace)

## 树莓派上的 RFID 读器

## 计数南瓜

用于 `SPI` 接口的廉价组件让你可以将树莓派 4 升级为用于非接触式 `RFID` 数据采集的显示系统。*作者：Martin Mohr*

无线频率识别 (`RFID`) 标签已成为工业、政府以及批发和零售空间不可或缺的。这些廉价的芯片可以在衣服标签、身份卡和信用卡上找到。通过树莓派和 `RFID` 套件，你可以从这些芯片中读取数据并在显示器上查看。

在这个项目中，我读取了贴在 3D 打印南瓜上的 `RFID` 标签序列号——这是一个略有不同的检测任务。为了实现这一点，我将 `RC522` [1] `RFID` 适配件和一个 1.8 英寸 `ST7735` 串行外接口 (`SPI`) 薄膜晶体管 (`TFT`) 显示器 [2] 连接到树莓派 4。这两个模块在在线商店的价格可能低于 15 美元（14 欧元）。南瓜包含简单的 `RFID` 标签 [3]，这些也可以免费获得。这个项目看起来清晰易懂，似乎可以立即运行，除非遇到那些“意外、不幸和故障”，以找出可能出现的问题。

图 1 所示电路显示了模块如何连接到树莓派，以及用于测试目的的两个南瓜和 `LED`。

## 意外、不幸和故障

在经过简短的研究后，我发现了一些打算用来控制模块的库。在经历了一天的思考和编程后，事实证明 `RFID` 读器库已经多年没有维护了。在 Python 3 中获取它的唯一方法是修改代码。在开源项目中，你应该始终查看最后一次提交的日期以及问题（issues），这些会告诉你该项目是否仍由社区开发。

我在网上偶然发现了许多遗弃的软件。初看之下，它们可能仍然活跃，但它们已经积灰多年。那个非常流行的树莓派工具已经很长时间没有支持了，关于 Python 的文章已从树莓派包源中删除。然而，互联网是有遗忘的，这意味着用户会被过时的手册和教程所困扰。

遗憾的是，底层的 Python 库似乎是草率接线的，没有经过广泛测试，这导致了不兼容性。例如，我必须替换此项目中的读器和显示程序。

## 基于 SPI 的 RFID 创空间

![](img/6816acb85ab93ecedbe75e6e9cb5d00d_60_0.png)

**图 1：** 项目的电路布局包含下载部分。你可以在右侧看到图表和 `RFID` 读器的连接。

使用 `KiCad` 设计电路。每个模块都连接到自己的 `SPI` 接口。图 2 显示了构建后的项目；`RFID` 标签隐藏在南瓜中。请注意，只有树莓派 4 具有多个板载 `SPI` 接口。

## 显示器和 RFID 读器

树莓派 4 拥有七个 `SPI` 接口中的四个，可以通过 40 脚 `GPIO` 引脚访问。

之前的模型只有三个 `SPI` 接口，其中只有两个路由到引脚。表 1 显示了默认情况下引脚上的哪些引脚对应于各个接口。

注意表 1 中的某些端口存在重叠，并且在默认配置下引脚上无法使用 `SPI` 接口。然而，可以使用 `dtoverlay` 命令调整 `SPI` 接口配置，它允许输出所有预定义 `SPI` 设备的列表（列表 1）。

各个接口有多种配置，每种配置都有定义的芯片选择 (`CS`) 线。因此，你可以非常精确地配置接口以适应你的项目。

### 列表 1：SPI 接口

```
$ dtoverlay -l | grep spi
sppi0-cs
sppi0-cs
sppi1-cs
sppi1-cs
sppi2-cs
sppi2-cs
sppi3-cs
sppi3-cs
sppi4-cs
sppi4-cs
sppi5-cs
sppi5-cs
sppi6-cs
sppi6-cs
```

![](img/6816acb85ab93ecedbe75e6e9cb5d00d_60_1.png)

**图 2：** 完整的测试设置，有一堆南瓜，读器在左左侧，显示器在后面。

### 创空间 RFID SPI

### 表 1：默认 SPI 引脚

| SPI | 引脚 | 编号 | SPI | 引脚 | 编号 |
|---|---|---|---|---|---|
| SPI0 | MOSI | 19 | SPI4 | MOSI | 31 |
| | MISO | 21 | | MISO | 29 |
| | SCLK | 23 | | SCLK | 26 |
| | CE0 | 24 | | CE0 | 7 |
| | CE | 26 | | CE | 22 |
| SPI1 | MOSI | 38 | SPI5 | MOSI | 8 |
| | MISO | 35 | | MISO | 33 |
| | SCLK | 40 | | SCLK | 10 |
| | CE0 | 32 | | CE0 | 12 |
| | CE1 | 37 | | CE1 | 37 |
| SPI3 | MOSI | 38 | | | |
| | MISO | 35 | | | |
| | SCLK | 40 | | | |
| | CE0 | 27 | | | |
| | CE1 | 13 | | | |

### 列表 2：dtoverlay 输出

```bash
$ dtoverlay -h spi=on
```

启用带有三个芯片选择 (`CS`) 线和相关节点的 `spi`。`CS` 线的 `gpio` 引脚和设备节点是可以配置的。这只在带有接线引头的设备上有效；例如：作为计算模块的树莓派 Zero B。

```
Usage: dtoverlay-spi <val>
Parameters:
cs_pin = gpio for spi (default BCM_SPI0)
cs1_pin = gpio for spi (default BCM_SPI1)
cs2_pin = gpio for spi (default BCM_SPI2)
cs0 = 设置为 "disabled" 以停止创建用户态节点/dev/spidev.0 (默认为 'ok' 或 disabled)
cs1 = 设置为 "disabled" 以停止创建用户态节点/dev/spidev.1 (默认为 'ok')
cs2 = 设置为 "disabled" 以停止创建用户态节点/dev/spidev.2 (默认为 'ok')
```

```
$ dtoverlay -l | grep spi
```

输出所有预定义 `SPI` 设备的列表（列表 1）。

由于在默认配置下引脚上无法使用 `SPI` 接口，请注意。然而，互联网是有遗忘的，这意味着用户会被过时的手册和教程所困扰。

如果你想启用 `SPI` 支持，请在你喜欢的编辑器中编辑 `/boot/config.txt` 文件末尾添加以下行：

```
dtparam=spi=on
dtoverlay-spi
```

重启树莓派使更改生效。

## 设置驱动程序

列表 4 中的示例程序用于在显示器上显示文本。为了生成合适的图像，从命令行传递的参数获取背景颜色

### 列表 3：准备工作

#### 更新树莓派

```bash
sudo apt update
```

#### 安装安装包

```bash
sudo apt install python3-libspidev-dev
```

#### SPI 和图形库

```bash
python3 -m pip install RPi.GPIO Pillow
```

#### 显示库

```bash
python3 -m pip install st7735
```

#### RPi 库

```bash
python3 -m pip install-2
```

## 基于 SPI 的 RFID

`PIL` 是一个功能强大的库，我将只使用一部分。为了显示在显示器上，文档 [7] 将让你大致了解 `Pillow` 可以做什么。

### 配置 RFID 读器

列表 5 中的程序从 `RFID` 芯片中读取单个 `UID`（第 10 行）并将它们显示在屏幕上（第 13 行）。显示器通过 `ST7735` 库控制我们使用的硬件。

注意，读器并没有对芯片进行身份验证，这意味着它生成了一个适合显示器的图像并存储在图像对象中。最后一个命令将图像传输到显示器。

示例程序只能读取受保护的芯片。如果你想进一步研究 `RFID` 身份验证主题，可以参考 `RC522` 库 [8]。

我使用了几个 `App` 来为芯片编程。`NFC Tag Reader` [9] 是入门的好工具，它许多许多奇的功能，同时也带有大量的广告。

`NFC Taginfo` [10] 和 `NFC TagWriter` [11] 提供了大量信息，这对于初学者来说可能有些困惑；将功能分为两个 `App` 使得工具更加易用。

`MIFARE Classic Tool` [12] 针对 `RFID` 芯片的操作进行了优化，并支持身份验证。我使用的读取器自带的 `S50` 卡也是一个 `RFID` 标签，它也遵循这种方法。

读取标签以获得结果。用于屏幕输出的 `Pillow` 库也是一个更清晰的选择。它的功能远超简单的弹出文本显示。

## Info

- [1] RC522 RFID 套件: https://www.amazon.com/Sunflower-Mifare-Reader-Arduino-Raspberry-pi/dp/B07KBJV/
