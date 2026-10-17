
![](img/3b256f430f51c98f1315671f6e4eec19_167_0.png)

上图：我们使用的是 Adafruit 出色的 GPS 分线板套件，此处：`bit.ly/1GBX2gw`

## 01 基本配置

启动树莓派，使用 `raspi-config` 扩展文件系统。进入高级选项，禁用串行连接——稍后你需要用它来与 GPS 模块通信。在 `raspi-config` 中，启用 `pi` 用户开机启动 X。选择 Yes 确认重启。重启后，确保你的软件包是最新的，运行：

```
sudo apt-get update
sudo apt-get upgrade
```

![](img/3b256f430f51c98f1315671f6e4eec19_167_1.png)

## 02 连接 GPS 模块

将排针焊接到 Adafruit GPS 模块上。你还可以焊接电池连接器，它可以让设备保持部分激活，从而更快地定位。你只需要使用 4 个引脚：`3.3V`、`地线`、`串行发送`和`串行接收`。在连接任何东西之前，再次关闭树莓派的电源。

由于我们使用的是 GPS，天线必须放到室外或窗边才能获得信号。将天线连接到板子上，然后重新通电。GPS 模块上的灯在寻找定位时会频繁闪烁。一旦定位成功，它会每 15 秒闪烁一次。

## 03 安装导航软件

输入以下命令开始安装 Navit 导航软件：

```
sudo apt-get install navit gpsd gpsd-clients espeak
sudo nano /etc/default/gpsd
set START_DAEMON="true"
```

...然后设置：

```
DEVICES="/dev/ttyAMA0"
```

使用以下命令启动 GPS 守护进程：

```
sudo /etc/init.d/gpsd start
```

你可以通过以下命令查看 GPS 数据，检查它是否正常工作：

```
cgps -s
```

## 04 连接屏幕

SainSmart 屏幕没有附带书面说明。不过，他们的网站上有一个 YouTube 视频，详细介绍了如何装配：`bit.ly/1DF6eJJ`。重要的是，直流电源应为 12V。

## 05 设置屏幕分辨率

我们需要通过 `sudo` 编辑 `/boot/config.txt` 来强制设置屏幕的正确分辨率（1024x600）。为此，添加以下选项：

```
framebuffer_width=1024
framebuffer_height=600
hdmi_force_hotplug=1
hdmi_cvt=1024 600 60 3 0 0 0
hdmi_group=2
hdmi_mode=87
```

为使更改正确生效，你需要使用 `sudo reboot` 重启。

## 06 下载内核源代码

要启动触摸屏，你需要编译一个额外的内核模块来支持它。`rpi-source` 程序（`github.com/notro/rpi-source/wiki`）会找到你的内核源代码。使用以下命令安装 `rpi-source`：

```
sudo wget https://raw.githubusercontent.com/notro/rpi-source/master/rpi-source -O /usr/bin/rpi-source
&& sudo chmod +x /usr/bin/rpi-source && /usr/bin/rpi-source -q --tag-update
```

然后运行 `rpi-source` 获取当前运行的内核源代码。

## 07 更新 GCC

最新的树莓派内核是使用 GCC 4.8 编译的。树莓派自带的只有 4.6，因此你需要安装 4.8 才能继续后续步骤。输入以下命令来安装：

- `sudo apt-get install -y gcc-4.8 g++-4.8 ncurses-dev`

然后你需要将 GCC 4.8 设置为默认版本：

- `sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.6 20`

- `sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 60`

- `sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.6 20`

- `sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 50`

## 08 选择要编译的模块

`rpi-source` 会将内核源代码放在名为 `linux` 的文件夹中。要选择 USB 触摸屏驱动，请输入以下内容：

- `cd linux`

- `make menuconfig`

- 设备驱动 -> 输入设备支持 -> 通用输入层（键盘、鼠标等所需）-> 触摸屏（按空格键包含）-> USB 触摸屏驱动（按 M 键生成模块）

完成之后，你需要确保将更改保存为 `.config`，然后运行 `scripts/diffconfig` 查看差异。

## 09 编译并安装模块

现在你需要编译并安装模块。输入以下命令：

- `make prepare`

- `make SUBDIRS=drivers/input/touchscreen modules`

- `sudo make SUBDIRS=drivers/input/touchscreen modules_install`

- `sudo depmod`

如果你拔下并重新连接触摸屏，它应该可以正常工作，但很可能需要校准。

```python
#!/usr/bin/env python2

import os, sys, requests, pygame

from gps import *

from pygame.locals import *

class WeatherClient:

    apikey = "7232a1f6857090f33b9d1c7a74721"

    @staticmethod

    def latlon():

        gpsd = gps(mode=WATCH_ENABLE)

        # Needs better error handling

        try:

            while True:

                report = gpsd.next()

                if report['class'] == 'TPV':

                    gpsd.close()

                    return report['lat'], report['lon']

        except:

            return None, None

    @staticmethod

    def usefuldata(j):

        # Returns a string of useful weather data from a LOT of json

        d = j['data']['current_condition'][0]

        out = "Now - Temp: {0}C, Feels Like: {1}C, Description: {2}\n"\
            .format(d['temp_C'],

                    d['FeelsLikeC'],

                    d['weatherDesc'][0]['value'])

        hourly = j['data']['weather'][0]['hourly']

        hour_count = 1

        for h in hourly:

            out += ("+{0}hr - Temp: {1}C, Feels Like: {2}C, Chance of Rain: "
                    "{3}%, Description: {4}\n")\
                    .format(hour_count,

                            h['tempC'],

                            h['FeelsLikeC'],

                            h['chanceofrain'],

                            h['weatherDesc'][0]['value'])

            hour_count += 1

        # Rstrip removes trailing newline

        return out.rstrip()
```
