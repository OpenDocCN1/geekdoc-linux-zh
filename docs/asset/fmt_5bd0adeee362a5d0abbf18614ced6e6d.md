
`sudo dpkg -i *.deb`

`raspberrypi-bootloader-112613.deb`

```

## 设置 `PiTFT` 触摸屏

![](img/51c03797fb5c18679e30c47f609c6b83_58_0.png)

```text
文件 编辑 帮助 搜索 帮助

ECDSA 指纹是 `sha256:de61:83:f4:ba:32:2c:1d:19:32:c8`

树莓派正在连接 (ECDSA) 到

警告: 已将 `'172.25.2.10 (ECDSA)'` 永久添加到已知主机列表。

`172.25.2.10 (ECDSA) 'ECDSA'`

`linux raspberrypi 5.19.34#1 PREEMPT 周三3月28 20:10:54 2024`

Debian GNU Linux 系统包含的程序可以自由使用、分发和复制。

每个包的发行版本在...描述。

单独文件位于 `/usr/copyright`。

此软件在适用法律允许范围内是免费的。

`cast light-info http://www.raspberrypi.org/2.113`

`$ wget -O - - http://download.s3.amazonaws.com/raspberrypi-bitn-afrafruit-bit-deb`

`https://download.s3.amazonaws.com/raspberrypi-bit-afrafruit-bit-deb`

`$ ssh pi@172.25.2.10`

正在连接 `172.25.2.10` [`172.25.2.10`]:22 ...

HTTP 请求接收, 200 OK

HTTP/1.1 200 OK

`Content-Length: 1884`

`Content-Type: text/html; charset=UTF-8`

`Server: AmazonS3`

`Date: 周三，2024年3月27日 12:00:00`

`URL: https://download.s3.amazonaws.com/raspberrypi-bit-afrafruit-bit-deb`

保存至: `/raspberrypi-bit-afrafruit-deb`

`2014-07-27 14:41:14 [0s] -- 'raspberrypi-bit-afrafruit-deb' 已保存 [1884K] 0.5s`

```

## 02 连接屏幕

如果你使用的是 2013 年 9 月的树莓派镜像，请使用以下框架：

```bash
$ sudo cp /usr/share/x11/xorg.conf.d/99-fb.conf
```

完成后，将树莓派连接屏幕到 `GPIO` 引脚（如果你还没有这样做的话）。

## 03 安装驱动

我们可以执行此操作以确保屏幕工作。但屏幕没有工作：

```bash
$ sudo modprobe bcm2708
$ sudo modprobe touchft_device-name=adafruit rotate=90
$ export FRAMEBUFFER=/dev/fb1
$ startx
```

## 05 配置

我们需要创建一个配置文件以便屏幕正常打开。第一行打开，第二行需要添加到此处：

```bash
$ sudo nano /etc/modprobe.d/adafruit
options touchft_device-name=adafruit rotate=90
```

## 06 选项

你可能会注意到这些选项允许旋转 0、90、180 或 270 度。60hz 的频率可能会给你大约 20fps；如果屏幕还没有设置好，重启树莓派。

## 07 安装

一旦返回，我们需要创建一个新的配置文件：

```bash
$ sudo nano /etc/X11/xorg.conf.d/99-calibration.conf
Section "InputClass"
Identifier MatchProduct ""
Option "Calibration"
Option "SwapAxes"
```

## 04 添加模块

有两个需要在启动时自动加载的模块。打开模块文件并添加第二行：

```bash
$ sudo nano /etc/modules
spi-bcm2708 touchft_device
```

## 08 测试触摸

一旦完成，启动 `X`：你可以通过添加以下内容使其生效：

```bash
$ export FRAMEBUFFER=/dev/fb1
```

你也可以使用 `raspi-config` 为你的便携式播放器设置显示。

![](img/51c03797fb5c18679e30c47f609c6b83_58_1.png)
![](img/51c03797fb5c18679e30c47f609c6b83_58_2.png)

# 教程：设置触摸屏和界面

Rob Zwetsloot 是一位复杂系统专家，也是一名精通 `Python`、`Django` 和 `PHP` 的 Web 开发者。他热爱实验。使用一些 `Python` 代码校准你的新触摸屏并添加界面。

![](img/51c03797fb5c18679e30c47f609c6b83_59_0.png)

## 你需要

- 带有最新版本树莓派的 `SD` 卡
- 已完全组装的 `PiTFT`
- `bitly/nej`

## 01 新规则

为了方便起见，我们将创建一个规则，这样就不会在命令行中丢失触摸屏的名称。登录 `SSH`，运行下一个命令并将以下文本复制进去：

我们有了一个具有基本触摸功能的屏幕，但接下来该怎么办？我们的第一步是让触摸实际上变得可用；电阻式，这样你可以使用手指或电磁笔，这将影响我们获得的校准结果。不要担心——如果你用一种方法进行校准，始终可以回来用另一种方法重新校准。

```bash
$ sudo nano /etc/udev/rules.d/95-touch.rules
SUBSYSTEM="input", ATTRS(name)="touch-ts", ENV(name)="event", SYM="touchscreen"
```

## 02 重新安装触摸

我们需要撤销上一个教程末尾所做的操作，以确保触摸部分正常工作，通过重新安装来恢复对其支持：

```bash
$ sudo modprobe touch_ts; sudo modprobe touch_ts
```

## 03 主事件

通过以下方法查找触摸屏的名称：

```bash
ls -1 /dev/input/touchscreen
```

我们可以安装工具来校准和调试触摸屏。使用以下命令安装并测试：

```bash
sudo apt-get install tslib libts-bin
sudo eventtest /dev/input/touchscreen
```

## 06 安装 `X` 校准

现在我们需要 `X` 中校准触摸屏，这意味着安装正确的工具。使用以下两个命令下载并安装：

```bash
wget http://adafruit-download.s3.amazonaws.com/xinput-calibrator-0.7.1-armhf
sudo dpkg -i -B xinput-calibrator-0.7.1-armhf
```

通过以下操作删除相关的校准数据：

```bash
sudo rm /etc/X11/xorg.conf.d/99-calibration.conf
```

![](img/51c03797fb5c18679e30c47f609c6b83_60_0.png)

## 04 触摸校准

我们终于可以开始校准过程。输入以下让树莓派学习屏幕上的大致位置：

```bash
$ TSLIB_FBDEVICE=/dev/fb1 TSLIB_TSDEVICE=/dev/input/touchscreen_ts_calibrate
```

![](img/51c03797fb5c18679e30c47f609c6b83_60_1.png)

## 07 `X`-校准

从 `SSH` 运行 `startx` 让屏幕打开。从这里你可以尝试在终端输入 `xinput_calibrator`，或者在 `SSH` 会话中输入以下内容：

```bash
FRAMEBUFFER=/dev/fb1 startx & DISPLAY=0.0 xinput_calibrator
```

## 08 保存校准

完成后，你会得到一个以 `InputClass` 开头的输出。打开以下文件并将 `Section` 到 `EndSection` 之间的输出复制到：

```bash
$ TSLIB_FBDEVICE=/dev/fb1 TSLIB_TSDEVICE=/dev/input/touchscreen_ts_test
```
