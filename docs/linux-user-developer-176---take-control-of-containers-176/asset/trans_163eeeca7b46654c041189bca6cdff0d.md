
# 动手体验 Pimoroni Blinkt!

![](img/6866071e033820549b214c239744aaa0_73_0.png)

### 学习基础知识，并用你的 Blinkt! 创建闪亮的灯光

**丹·奥尔德雷德（Dan Aldred）** 是一位树莓派认证教育者，也是 CAS 的主要学校教师。他曾带领一支团队在 Astro Pi 中学竞赛中获胜，并出现在英国教育部（DfE）的“激励型教师”电视广告中。最近，他从 Skyacademy 毕业，成功将一个绑有树莓派的高空气球发射至平流层 31,000 米以上的空域。

Pimoroni 公司打造了一款出色的“超高亮 RGB LED 指示灯”，它是为树莓派添加视觉通知的理想之选，而且价格亲民！Blinkt! 提供了 8 个 APA102 像素点，采用最小（也是最便宜）的外形规格，可以直接插入树莓派 3/2/B+/A+/Zero。本教程将指导你安装 Blinkt! 以及所需的 Python 库和模块。接下来，创建并尝试一些简单的代码，以控制灯光，改变 LED 的颜色和亮度。最后，结合这些技能，编写一个 LED 颜色生成器代码，从八盏灯的范围中随机选择一个 LED 和一个随机 RGB 颜色值。这将创建一个迷幻的迪斯科灯光设置。

## 你需要什么

- Pimoroni Blinkt!

![](img/6866071e033820549b214c239744aaa0_73_1.png)

![](img/6866071e033820549b214c239744aaa0_73_2.png)

## 01 安装 Blinkt!

Pimoroni 公司的工程师们让安装 Blinkt! 软件变得非常容易（软件还包含一系列展示其功能的酷炫示例）。要开始操作，请确保电源已关闭，将 Blinkt! 连接到树莓派的 GPIO 引脚并用力向下按压。它的一侧是直的，另一侧是弯曲的。弯曲的边缘与你的树莓派的弯曲角对齐。这确保了你能正确方向安装它。现在连接你的电源并启动树莓派。打开终端并输入：

```bash
curl -sS get.pimoroni.com/blinkt | bash
```

这将安装所有必需的代码。

## 02 点亮一个 LED

要点亮一个 LED，打开你的 Python 编辑器并导入所需的 Python 模块，第 1 行。使用代码 `set_pixel()`，第 2 行，来设置哪些像素被点亮。括号中的第一个数字对应每个 LED。与通用的计算方法一样，第一个 LED 由数字零表示，第二个 LED 是数字一，依此类推，直到第八个 LED，即数字七。复制下面的代码并运行程序，以点亮第一个 LED。

```python
from blinkt import set_pixel, show
set_pixel(0,255,0,0)
show()
```

## 03 更改 LED 的颜色

括号中的下一个三个值 (x, 255, 210, 150)，用于使用标准的 RGB 调色板控制 LED 的颜色。你可以控制和设置红色、绿色和蓝色的量，数值在 0 到 255 之间；数字越大，LED 上显示的该颜色越多。组合这些值可获得超过 1600 万种可能的组合和颜色。更改代码中的数值，保存然后运行。

```python
set_pixel(0,255,255,0)
show()
```

## 04 调整 LED 的亮度

你可能会发现 LED 太亮，难以直视。不建议长时间直视它们，因为这可能会损伤你的眼睛。相反，降低亮度，以便安全观看。首先，导入亮度模块，第 1 行。你可以通过在同一行包含“模块名称”来导入多个模块——例如，`from blinkt import set_pixel, show, set_brightness`。现在将亮度设置到合适的级别，第 2 行。数值范围在零和一之间，其中一表示全亮度，零则使所有 LED 熄灭。

## 谁在使用互联网？

你居住在一个或多个人的家庭或办公室中，多人同时使用互联网吗？是否有许多设备始终连接到网络，从而耗尽带宽并降低其他所有用户的网速？将 Blinkt 与 Python 和 npm 结合使用，以识别用户，追踪他们在网络上的活动，并在每个用户加入和离开网络时为其创建一个色彩鲜艳的 LED 视觉指示。在此处观看视频：youtu.be/r_JDw65FTMA

![](img/6866071e033820549b214c239744aaa0_74_0.png)

```python
from blinkt import set_brightness
set_brightness(0.5)
```

## 05 点亮多个灯

使用 `set_pixel` 代码点亮多个 LED，然后设置 RGB 颜色值。请记住，对于 LED 编号，‘零’ 是第一个 LED，因为你是从零开始向上计数的。最后一个 LED 是数字七。尝试点亮两个或更多 LED：例如，将最后一个 LED 设置为红色，将第四个 LED 设置为蓝色。保存并运行程序。

```python
set_pixel(7,255,0,0)
show()
set_pixel(3,0,0,255)
show()
```

![](img/6866071e033820549b214c239744aaa0_74_1.png)

## 06 创建随机闪烁的灯

结合之前的代码步骤，创建一组随机的闪烁迪斯科灯！首先，选择一个新的空白 Python 文件并导入随机模块，第 1 行。这用于为颜色和 LED 位置编号选择随机值。接下来，导入时间模块，第 2 行。这增加了对变化频率的控制（较大的时间值会导致较慢的闪烁）。最后，导入在程序退出时清除 LED、设置特定像素为开启状态以及降低亮度的代码，第 3 行。第 4 行启用 LED 在退出时清除，第 5 行设置你所需的亮度值，在零和一之间。

```python
import random
import time
from blinkt import set_clear_on_exit, set_pixel, show, set_brightness
set_clear_on_exit()
set_brightness(0.1)
```

![](img/6866071e033820549b214c239744aaa0_74_2.png)

## 07 创建 while 循环并设置随机值

现在创建一个 `while` 循环，以确保程序不断重复并循环执行代码，第 1 行。在下一行（缩进），使用 `for` 循环对每个 LED 的代码进行迭代。这有效地将下一条指令应用于每个 LED，从第一个 LED 到最后一个，第 2 行。使用 `set_pixel` 代码点亮 LED，第 3 行；注意，这也进行了缩进。

```python
while True:
  for i in range(8):
    set_pixel(i,
```

![](img/6866071e033820549b214c239744aaa0_74_3.png)

## 08 选择随机颜色

在编码 LED 时，如第 3 步所述，说明 LED 的 RGB 颜色值；使用代码 `random.randint(0,255)`。这会随机选择 0 到 255 之间的一个颜色值。再添加两个该代码的实例，分别为绿色和蓝色选择值。在第 2 行，使用代码 `show()` 设置 LED 显示颜色；注意，这一行没有缩进。最后，添加一个短的时间延迟，以便你可以在状态改变前观察到灯光，第 3 行。

```python
set_pixel(i, random.randint(0,255), random.randint(0,255), random.randint(0,255))
show()
time.sleep(0.05)
```

## 09 运行程序

保存你的程序文件并按 F5 运行；给文件取一个合适的名称。按 **Enter** 键，程序将运行，在每个 LED 上显示随机颜色的变体。尝试不同的颜色值，创建你喜欢的变体，并调整变化的延迟速度，使其加快或减慢。

## 红、绿和蓝颜色

RGB 颜色模型是一种加色模型，其中红、绿和蓝光以不同比例混合，以产生广泛的颜色范围，超过 1600 万种不同的变体。颜色的最低值是零，通常表示黑色，因为黑色不是一种颜色，而是颜色的缺失！最高值是 255；例如，红色 255 意味着正在添加最大量的红色到色调中。

# 制作树莓派 VPN 接入点

### 将你的树莓派作为 24/7 连接到 VPN 的无线接入点

![](img/6866071e033820549b214c239744aaa0_75_0.png)

Nate Drake
(@natewriter)
是一位自由科技记者，专注于网络安全和末日装置。

![](img/6866071e033820549b214c239744aaa0_75_1.png)

任何出过国的人都知道，不得不处理已切换为当地语言的内容始终是一种困扰，更不用说某些国家还会审查部分互联网内容。

幸运的是，使用树莓派可以避免这些限制。只需几个简单的步骤，你就可以配置树莓派生成自己的无线接入点（AP），并使其永久连接到虚拟专用网络（VPN）服务。

旅行时你要做的只是带上你的树莓派并将其连接到可用的路由器，你就拥有了自己的专用无线网络和连接。

VPN 最初的设计目的是允许上班族在远离办公室时通过加密连接连接到企业内网。如今，它们更常用于保护你的连接，并让你的电脑看起来像是位于另一个国家。

为了继续这个项目，你需要一个有效的 VPN 订阅以及客户端配置文件（.conf）以便自动连接。

## 01 选择你的 VPN

为了完成这个项目，你需要一个 VPN 提供商的账户。寻找支持 OpenVPN 协议的提供商，因为这种连接通常被认为是最安全的。免费提供商不需要任何账单信息，但它们不如付费服务那么快速或可靠。如果你选择付费提供商，请尝试寻找接受比特币等匿名支付方式的提供商。网站 www.weusecoins.com 列出了这些提供商。

![](img/6866071e033820549b214c239744aaa0_75_2.png)

## 02 下载配置文件

将树莓派连接到你的路由器。打开终端或通过 SSH 连接。如果你的 VPN 提供商支持安全的 OpenVPN 标准，那么他们将提供一个扩展名为 .conf 或 .ovpn 的配置文件。本教程使用的是免费提供商 VPNBook 的 VPN 配置文件。通过点击链接或在终端中使用 wget 将文件下载到树莓派，例如：

```bash
wget http://www.vpnbook.com/free-openvpn-account/VPNBook.com-OpenVPN-Euro01.zip
```

![](img/6866071e033820549b214c239744aaa0_75_3.png)

## 你需要什么

- 支持 Wi-Fi 的树莓派
- 以太网线
- 支持 OpenVPN 的有效 VPN 订阅
- 笔记本电脑等次要设备，用于测试你的 AP 是否正常工作

## 03 安装 OpenVPN

Raspbian 软件源包含 OpenVPN 软件，因此请确保你拥有最新版本。使用命令 `sudo` 切换到 root 用户，然后运行这些命令：

```bash
sudo -i
wget -O - https://repo.swapdate.openvpn.net/repo/public.gpg | apt-key add -
echo "deb http://swapdate.openvpn.net/apt jessie main" > /etc/apt/sources.list.d/swapdate.openvpn.net.list
apt-get update
apt-get install openvpn
```

运行 `openvpn --version` 再次确认你拥有最新版本的软件。在撰写本文时，版本为 2.3.14。

![](img/6866071e033820549b214c239744aaa0_75_4.png)

## 04 配置并运行 OpenVPN

使用 `mv` 命令将配置文件移动到 openvpn 文件夹 `/etc/openvpn`，如有必要请修改扩展名，例如：

```bash
sudo mv vpn42e_vpn151111658.opengw.net_udp_1344.ovpn /etc/openvpn/vpn1.conf
```

接下来，使用命令 `sudo service openvpn start` 启动 OpenVPN 服务。使用 openvpn --config 命令结合你的 .conf 文件启动 OpenVPN，例如：

```bash
sudo openvpn --config /etc/openvpn/vpn1.conf
```

![](img/6866071e033820549b214c239744aaa0_75_5.png)

