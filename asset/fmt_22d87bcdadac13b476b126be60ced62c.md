
- 面包板
- LED
- 按钮
- 电阻器
- 跳线
- ScratchGPIO3

Scratch 是一种非常简单的可视化编程语言，通常用于向任何年龄的学习者教授基本的编程概念。在本项目中，我们将学习如何在 Scratch 中点亮 LED 当按钮被按下时，然后当物理按钮被按下时改变角色的颜色。通过这些技术，你可以制作各种有趣且引人入胜的项目，从音乐键盘到你 Scratch 游戏和动画的控制器。

### 01 安装所需的软件

使用用户名 `pi` 和密码 `raspberry` 登录 Raspbian 系统。使用命令 `startx` 启动 LXDE 桌面环境。然后打开 LXTerminal 并输入以下命令：

```bash
wget http://i1ianfraser.co.uk/lxd/install_scratchgpio3.sh
chmod +x install_scratchgpio3.sh
sudo bash install_scratchgpio3.sh
```

这将在你的桌面上创建一个名为 ScratchGPIO3 的特殊版本的 Scratch。这是正常版本的 Scratch，其中包含一个处理 Scratch 和 GPIO 之间通信的 Python 脚本。ScratchGPIO 由 simplesi 创建（cymplecy.wordpress.com）。

## 使用 Scratch 实现交互

![](img/a1548a579bd09ff29b2b92de3f565e63_16_0.png)

### 02 连接面包板

关闭树莓派电源并拔掉电源线。准备好面包板、一个 LED、一个 330 欧姆电阻和两根 GPIO 线。你需要将 3.3V 引脚（右上角引脚，靠近 SD 卡）连接到 330 欧姆电阻的一端，然后将 LED 的正极（较长的一脚，有一个小凸起）连接到电阻的另一端。

### 03 开关 LED

目前，LED 连接到一个持续提供 3.3V 的引脚。如果我们想要能够开关它，这就没太大用处，所以让我们将它连接到 GPIO 17，我们可以打开和关闭它。GPIO 17 是顶部引脚行从左数第六个引脚。重新给树莓派通电。我们可以通过导出 GPIO 引脚，将其设置为输出，然后将其值设置为 1 来打开 LED。将值设置为 0 则关闭 LED。

```bash
echo 1 > /sys/class/gpio/export
echo out > /sys/class/gpio/gpio17/direction
echo 1 > /sys/class/gpio/gpio17/value
echo 0 > /sys/class/gpio/gpio17/value
```

![](img/a1548a579bd09ff29b2b92de3f565e63_16_1.png)

### 04 从 Scratch 控制 LED

启动 LXDE 桌面环境并打开 ScratchGPIO3。转到控制部分并创建一个简单的脚本，当精灵 1 被点击时广播 `pinOn`。然后点击精灵。LED 应该会亮起来。然后在脚本中添加等待 1 秒，然后广播 `pinOff`。如果你再次点击精灵，LED 会亮一秒然后熄灭。ScratchGPIO3 使用引脚编号而不是 GPIO 编号来识别引脚。右上角的引脚（我们最初将 LED 连接到 3.3V 的引脚）是引脚编号 1；该引脚下方的引脚是引脚编号 2；依此类推。

![](img/a1548a579bd09ff29b2b92de3f565e63_16_2.png)

### 05 接线按钮

再次关闭树莓派电源。这个电路比我们之前创建的 LED 电路稍复杂一些。我们需要做的第一件事是将 3.3V（我们之前用来测试 LED 的右上角引脚）连接到面包板的正极轨。然后我们需要将一个 10/kohm 电阻连接到正极轨，并将另一端连接到面包板上的一个空轨。然后，在同一轨上，添加一根导线，其一端连接到 GPIO 4。这是 GPIO 12 右侧第二个引脚。然后，再次在同一轨上，连接按钮的一个引脚。最后，通过添加一根连接到接地负极轨的导线，将按钮的另一个引脚连接到地。

当按钮未被按下时，GPIO 4 将接收 3.3V。但是，当按钮被按下时，到地的电路将闭合，GPIO 4 将接收 0V（因为到地的路径上电阻小得多，所以值为 0）。

我们可以通过观察引脚值然后按下按钮使其改变来看到这种效果：

```bash
echo 4 > /sys/class/gpio/export
echo in > /sys/class/gpio/gpio4/direction
watch -n 0.5 cat /sys/class/gpio/gpio4/value
```

![](img/a1548a579bd09ff29b2b92de3f565e63_16_3.png)

### 06 点亮灯光！

启动树莓派并像以前一样启动 ScratchGPIO3。转到控制部分并添加“当绿旗被点击时”。然后附加一个永远循环，并在其中添加一个 if-else 语句。转到运算符部分并添加“如果 [] 等于 []”运算符到 if 语句。然后转到感应部分并在等式左侧添加一个值传感器，将值设置为 `pin7`。在等式右侧，输入 0。如果传感器值为 0，则广播 `pinOn`，否则广播 `pinOff`。点击绿旗。如果你按下按钮，LED 将会亮起！

#### 你将学到...

- **简单电路**

  虽然这些是非常简单的电路，但你会很好地理解树莓派如何与基本原型套件接口。如果你需要购买部件，我们建议你查看：shop.pimoroni.com

- **编码原则**

  如果你是编程新手，Scratch 是学习所有编程语言采用的相同编程原则的完美场所。

- **物理计算**

  没有什么比将代码从电脑屏幕转化为现实效果更神奇的了。你的第一个项目可能只是一个灯的开关，但一旦点亮，天空才是极限。

## 10 实用树莓派项目

![](img/a1548a579bd09ff29b2b92de3f565e63_17_0.png)

Google Coder 是让你入门网页开发的好方法。

### 构建树莓派 Web 服务器

使用 Google Coder 将你的树莓派变成一个小型、低功耗的 Web 服务器和 Web 托管平台

- **你需要什么**

  - 互联网连接
  - Web 浏览器
  - Google Coder

我们在树莓派上用多种不同的方式教你编程，所以看看网络也是合情合理的。

在树莓派上使用网络还有一种新方法：互联网巨头谷歌最近专门为这款小型计算机发布了 Coder。这是一个基于 Raspbian 的镜像，将你的树莓派变成一个 Web 服务器和 Web 开发套件。它可以轻松通过局域网访问，并且开箱即支持 jQuery，它是进一步提升你的网页开发技能的一种简单且很棒的方式。

#### 01 获取 Google Coder

前往 Google Coder 网站，下载压缩版的镜像。将其解压到任何你希望的位置，并使用 `dd` 安装它，就像其他树莓派镜像一样：

```bash
$ dd if=[path to]/raspi_img of=/dev/[path to SD card] bs=1M
```

![](img/a1548a579bd09ff29b2b92de3f565e63_17_1.png)

#### 02 插入你的树莓派

对于这个教程，你只需要将一根网线插入树莓派。插入新写入的 SD 卡，插上电源并等待片刻。如果你已经连接了显示器，你会注意到一个 Raspbian 启动序列，最终进入命令行登录屏幕。

#### 03 连接到 Coder

在主系统上打开浏览器，访问 `http://coder.local`。你可能需要手动接受许可协议。它会要求你设置密码，然后你就可以进入并开始编码了。

![](img/a1548a579bd09ff29b2b92de3f565e63_18_1.png)

#### 04 Web 语言

现在是时候创建你自己的应用程序或网站了。点击示例旁边的“+”框，给你的应用程序起个名字，然后点击创建。你将被带到应用程序的 HTML 部分。

将 Hello/World 行更改为：

```html
<h1>这是一个 HTML 标题</h1>
<p>这是一个新的默认文本块</p>
```

![](img/a1548a579bd09ff29b2b92de3f565e63_18_2.png)

#### 05 令人印象深刻的样式

点击 CSS 选项卡。这更改了网页的外观和样式，而不必每次都在主代码中进行更改。你可以使用以下代码更改背景颜色和字体：

```css
body {
    background-color: #000000;
    color: #ffffff;
}
```

#### 完整代码列表

#### HTML

一些简单的 HTML 代码，可以引导我们访问一些重要的网站。

`h2` 标签用于显示时间，得益于 Java
