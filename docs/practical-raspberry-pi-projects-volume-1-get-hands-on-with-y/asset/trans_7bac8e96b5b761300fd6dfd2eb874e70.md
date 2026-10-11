

![](img/a1548a579bd09ff29b2b92de3f565e63_103_0.png)

# 电子制作

- **106 打造一台树莓派车载电脑**  
  制作你自己的触摸屏导航仪
- **114 我是如何制作的：RasPiViv**  
  探究环境控制系统
- **116 制作一个树莓派采样器**  
  构建你自己的循环鼓机
- **120 将你的树莓派变成微型示波器**  
  使用 BitScope Micro 改造你的树莓派
- **124 我是如何制作的：Pi Glove 2**  
  控制灯光、报税以及更多功能
- **126 组装一个《我的世界》强力手套**  
  用这个酷炫的黑客技巧增强你的游戏体验
- **130 构建复杂的 LED 点阵屏**  
  编程实现你自己的灯光系统
- **134 为你的树莓派添加手势控制**  
  轻松为项目添加触控控制
- **138 我是如何制作的：Joytone**  
  一种新型电子键盘
- **140 使用面包板模拟交通信号灯**  
  尝试硬件工程
- **142 编程一架四轴飞行器**  
  使用此套件翱翔天际
- **148 20 个树莓派黑客项目**  
  让日常物品重获新生

![](img/a1548a579bd09ff29b2b92de3f565e63_104_0.png)
![](img/a1548a579bd09ff29b2b92de3f565e63_104_1.png)

**120 将你的树莓派变成示波器**
![](img/a1548a579bd09ff29b2b92de3f565e63_104_2.png)

**130 组装一个 LED 显示屏**
![](img/a1548a579bd09ff29b2b92de3f565e63_104_3.png)

**134 为你的树莓派添加手势控制**
![](img/a1548a579bd09ff29b2b92de3f565e63_104_4.png)

**142 操控一架树莓派动力的四轴飞行器**
![](img/a1548a579bd09ff29b2b92de3f565e63_104_5.png)
![](img/a1548a579bd09ff29b2b92de3f565e63_104_6.png)

**148 制作一个电动闹钟**
**148 尝试光枪游戏**
![](img/a1548a579bd09ff29b2b92de3f565e63_104_7.png)

105

![](img/a1548a579bd09ff29b2b92de3f565e63_105_0.png)
![](img/a1548a579bd09ff29b2b92de3f565e63_105_1.png)

# 打造一台树莓派车载电脑

制作你自己的触摸屏导航系统，它能提供路线指引、当地天气报告并播放音乐

![](img/a1548a579bd09ff29b2b92de3f565e63_106_0.png)
![](img/a1548a579bd09ff29b2b92de3f565e63_106_1.png)

汽车正在变得越来越智能。如今，新款汽车都内置了智能导航界面，你不需要专门去买一个 TomTom 来获取路线帮助。但如果你有一台树莓派，你甚至不需要买那个——更别提买一辆新车了！

在这个项目中，我们将展示如何使用树莓派、一块高质量触摸屏（如我们这里使用的 SainSmart 9 英寸型号）以及一些其他部件（如 GPS 模块和 USB 3G 调制解调器）来打造你自己的车载电脑。你的 CarPi 将能够使用开源导航软件 Navit 在屏幕上显示路线图，并通过语音合成朗读方向指示，还能检查你所在的位置并播报天气报告。当然，它也可以作为音乐播放器使用。

这是一个雄心勃勃的项目，但你将对自定义界面、导航软件、地理位置数据、触摸屏校准、语音合成等有深入的了解。虽然你不必使用与我们相同的 SainSmart 屏幕，但我们推荐它用于此项目，因为它是目前市面上少数适用于树莓派的大尺寸触摸屏之一。文章末尾还有一些改进建议，所以请检查部件清单，确保你拥有所有材料，让我们开始吧！

![](img/a1548a579bd09ff29b2b92de3f565e63_107_0.png)

上方 我们在这里使用了 Adafruit 优秀的 GPS 分立式电路板：bit.ly/1GBX2gw

## **01 基本配置**

启动你的树莓派，并使用 *raspi-config* 扩展文件系统。进入高级选项并禁用串口连接——稍后你需要它来与 GPS 模块通信。在 *raspi-config* 中，以 pi 用户身份启用开机自启动图形界面（X）。对重启提示选择“是”。重启后，使用以下命令确保你的软件包是最新的：

```bash
sudo apt-get update
sudo apt-get upgrade
```

## **02 连接 GPS 模块**

将针脚焊盘焊接到 Adafruit GPS 模块上。你也可以焊接电池连接器，它用于让设备部分保持活动状态，从而获得更快的定位。你只需要使用 4 个针脚：3.3V、地线、串口发送和串口接收。在连接任何东西之前，请先关闭树莓派的电源。

由于我们要使用 GPS，天线必须放置在室外或窗户下方以获取信号。将天线连接到电路板，然后重新接通所有电源。在寻找定位时，GPS 模块上的指示灯会频繁闪烁。一旦定位成功，它将每 15 秒闪烁一次。

![](img/a1548a579bd09ff29b2b92de3f565e63_107_1.png)

## **03 安装导航软件**

通过输入以下命令开始安装 Navit 导航软件：

```bash
sudo apt-get install navit gpsd gpsd-clients espeak
sudo nano /etc/default/gpsd
```

设置 `START_DAEMON=true`。

...并设置：

```bash
DEVICES="/dev/ttyAMA0"
```

使用以下命令启动 GPS 守护进程：

```bash
sudo /etc/init.d/gpsd start
```

你可以通过查看 GPS 数据来检查它是否正常工作：

```bash
cgps -s
```

## **04 连接屏幕**

SainSmart 屏幕不附带书面说明。取而代之的是，我们的网站上有一个 YouTube 视频，详细介绍了组装方法：bit.ly/1DF6eJJ。重要的一点是 DC 电源应为 12V。

## **05 设置屏幕分辨率**

我们必须通过编辑 */boot/config.txt* 来强制设置屏幕的正确分辨率（1024x600），并使用 *sudo* 进行编辑。为此，添加以下选项：

```bash
framebuffer_width=1024
framebuffer_height=600
hdmi_force_hotplug=1
hdmi_cvt=1024 600 60 3 0 0 0
hdmi_group=2
hdmi_mode=87
```

要使更改正确生效，你需要使用 *sudo reboot* 重启系统。

## **06 下载内核源代码**

要启动触摸屏，你需要编译一个额外的内核模块以支持它。程序 *rpi-source* [github.com/notro/rpi-source/wiki] 会找到你的内核源代码。使用以下命令安装 *rpi-source*：

```bash
sudo wget https://raw.githubusercontent.com/notro/rpi-source/master/rpi-source -O /usr/bin/rpi-source
sudo chmod +x /usr/bin/rpi-source
/usr/bin/rpi-source -q -tag-update
```

然后运行 *rpi-source* 获取正在运行的内核的源代码。

## **07 更新 GCC**

最近的树莓派内核是使用 GCC 4.8 编译的。Raspbian 只附带 4.6 版本，因此你必须安装 4.8 才能继续执行后续步骤。通过输入以下命令来执行此操作：

```bash
sudo apt-get install gcc-4.8 g++-4.8 ncurses-dev
```

然后你必须将 GCC 4.8 设置为默认版本：

```bash
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.6 20
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 50
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.6 20
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 50
```

## **08 选择要编译的模块**

Rpi-source 将内核源代码放入名为 ‘linux’ 的文件夹中。要选择 USB 触摸屏驱动程序，请输入以下内容：

```bash
cd linux
make menuconfig
```

设备驱动程序 → 输入设备支持 → 通用输入层（键盘、鼠标等所需） → 触摸屏（按空格键以包含） → USB 触摸屏驱动程序（按 M 键以生成模块）

完成上述操作后，你需要确保将更改保存为 ‘.config’ 并运行 scripts/diffconfig 以查看差异。

## **09 编译并安装模块**

现在你需要编译并安装该模块。通过输入以下命令来执行此操作：

```bash
make prepare
make SUBDIRS=drivers/input/touchscreen modules
sudo make SUBDIRS=drivers/input/touchscreen modules_install
sudo depmod
```

如果你拔掉并重新连接触摸屏，它应该能正常工作，但可能需要进行校准。

## 完整代码列表

```python
#!/usr/bin/env python2
import os, sys, requests, pygame
from gps import *
from pygame.locals import *

class WeatherClient:
    apikey = "7232af6857090f33b9d1c7a74721"

    @staticmethod
    def latlon():
        gpsd = gps(mode=WATCH_ENABLE)
        # 需要更好的错误处理
        try:
            while True:
                if report := gpsd.next():
                    if report['class'] != 'TPV':
                        gpsd.close()
                        return report['lat'], report['lon']
                
        except:
            return None, None

    @staticmethod
    def usefuldata():
        # 从大量的 json 中返回有用的天气数据字符串
        d = json.loads(requests.get(f"http://api.worldweatheronline.com/free/v2/weather.ashx?q={o[0]}[o[0]current_condition}]&key={api key}").text)
        out = f"\n\n- 当前 - 温度: {o[1]}, 体感温度: {o[2]}C, 描述: {o[3]}\n\n"

        hourly = json.loads(requests.get(f"http://api.worldweatheronline.com/free/v2/weather.ashx?q={o[0]}[o[0]hourly})&key={api key}").text)
        hour_count = 1
        for h in hourly:
            out += f"- (+{h}小时) - 温度: {h[1]}C, 体感温度: {h[2]}C, 降雨概率:"
                   f" {h[3]}%, 描述: {h[4]}\n"
        hour_count += 1

        # Rstrip 去除尾部换行符
        return out.rstrip()

    @staticmethod
    def update():
        errstr = "获取天气数据时出错"

        lat, lon = WeatherClient.latlon()
        if lat == None or lon == None:
            return errstr

        api_req = f"http://api.worldweatheronline.com/free/v2/weather.ashx"
                  f"?q={o[0]%2C(2)[0]&format=json&key={2}"
        
        r = None
        ...
```

