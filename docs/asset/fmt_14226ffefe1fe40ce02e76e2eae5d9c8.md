
你能利用所学的知识在屏幕上画出一个图像，然后根据摇杆推动的任何方向进行旋转吗？你能让中间输入在多张图片之间切换吗？

![](img/0aff4cdab15427839fb48fd7c6f677d3_189_0.png)

### Scratch 项目：Sense HAT 烟花

现在你熟悉 Sense HAT 了，是时候运用所学的一切来制作一个烟花了。在 Scratch 中启动一个新项目并添加 Sense HAT 扩展。当点击绿色旗帜时，使用“重复”循环来创建效果。在循环内部，使用随机积木来确定摇杆的方向。然后，使用“旋转”积木按该角度旋转你的角色。你还可以使用“如果...否则...”积木块在按下中间按钮时切换不同的图片。

![](img/0aff4cdab15427839fb48fd7c6f677d3_189_1.png)

```python
def temperature():
    temp = sense.get_temperature()
    temp = round(temp, 1)
    sense.show_message("Temperature: %s degrees Celsius" % temp)
```

仔细观察产生 LED 输出结果的那行代码：`%s` 被称为占位符，会被变量 `temp` 的内容替换。通过这种方式，你可以使用标签“Temperature”（温度）和单位“degrees Celsius”（摄氏度）格式化输出，这会让你的程序更加友好。

为湿度传感器定义一个函数：

```python
def humidity():
    humidity = sense.get_humidity()
    humidity = round(humidity, 1)
    sense.show_message("Humidity: %s percent" % humidity)
```

然后读取传感器：

```python
def pressure():
    pressure = sense.get_pressure()
    pressure = round(pressure, 1)
    sense.show_message("Pressure: %s millibars" % pressure)
```

最后是读取来自磁力计的罗盘数据：

```python
def compass():
    for i in range(0, 10):
        north = sense.get_compass()
        north = round(north, 1)
        sense.show_message("North: %s degrees" % north)
```

该函数中的 `for` 循环从磁力计读取十次数据，以确保有足够的数据来提供准确的结果。如果你发现报告的值不断变化，可以将循环次数扩展到 20、30 甚至 100 以进一步提高精度。

你的程序有五个函数，每个函数都从 Sense HAT 的一个传感器读取数据并并在 LED 上滚动显示。不过，你需要一种方法来选择想要使用哪个传感器，而摇杆正是此功能的完美选择。

输入以下内容：

```python
sense.stick.direction_up = orientation
sense.stick.direction_right = temperature
sense.stick.direction_down = compass
sense.stick.direction_left = humidity
sense.stick.direction_middle = pressure
```

这些行将传感器分配到摇杆的五个可能方向上：向上读取方向传感器，向下读取磁力计；向左读取湿度传感器；向右读取温度传感器；按下摇杆中间则读取压力传感器。

最后，你需要一个主循环，这样程序就会持续监听摇杆的按下操作，而不是立即退出。在程序的最底部，输入以下内容：

```python
while True:
    pass
```

点击“运行”（Run），尝试移动摇杆以获取某个传感器的读取值（**图 7-29**）。当结果滚动完成后，按下另一个方向。恭喜你：你制作了一个足以让行星联邦感到自豪的手持式三功能探测仪！

![](img/0aff4cdab15427839fb48fd7c6f677d3_193_0.png)

▲ 图 7-29：每个读取值都在显示屏上滚动

欲了解更多 Sense HAT 项目，请参考**附录 D，进一步阅读**中的链接。

# 第 8 章

## 树莓派摄像头模块

将摄像头模块或高质量摄像头（HQ Camera）连接到树莓派，可以让你拍摄高分辨率照片和视频，并创建惊人的计算机视觉项目。

![](img/0aff4cdab15427839fb48fd7c6f677d3_195_0.png)

> 如果你曾想构建某种能“看”的东西——在机器人领域被称为计算机视觉——那么树莓派可选的摄像头模块或新的高质量摄像头是一个极佳的起点。这是一个带有薄排线的小型正方形电路板，摄像头模块/高质量摄像头连接到树莓派上的摄像头串行接口 (CSI) 端口（树莓派 400 不可用），并提供高分辨率静态图像和动态视频信号，这些信号可以直接使用或集成到你的程序中。

# 官方树莓派初学者指南

![](img/0aff4cdab15427839fb48fd7c6f677d3_196_0.png)

## 摄像头类型！

树莓派摄像头有三种：标准摄像头模块、NoIR（无红外）版本和高质量摄像头（HQ Camera）。标准摄像头模块是一款通用的摄像头。NoIR（无红外）版本缺少红外滤镜，配合红外 LED 使用时非常适合夜视项目。高质量摄像头（HQ）提供了更高的图像质量和可更换镜头，适用于专业级摄影和视频拍摄。

### 测试摄像头

为了确认你的摄像头模块（Camera Module）或高清摄像头（HQ Camera）已正确安装，并且你已经在 Raspberry Pi 配置工具中启用了接口，你可以使用 `raspistill` 工具。该工具连同用于视频的 `raspvid`，旨在通过树莓的命令行界面 (CLI) 从相机拍摄图像。

与你之前使用的程序不同，你不会在菜单中找到 `raspistill`。相反，点击树莓图标加载菜单，选择“附件”（Accessories）类别，然后点击“终端”（Terminal）。将出现一个带有绿色和蓝色文字的黑色窗口（图 8-4）：这就是终端，允许你访问命令行界面。

![](img/0aff4cdab15427839fb48fd7c6f677d3_199_0.png)

![](img/0aff4cdab15427839fb48fd7c6f677d3_199_1.png)

- ▲ 图 8-3：你需要在 Raspberry Pi 配置中启用摄像头
- ▲ 图 8-4：打开终端窗口以输入命令

要测试摄像头，在终端中输入以下内容：

```
raspistill -o test.jpg
```

一旦你按下 **ENTER** 键，你就会看到屏幕上出现一张摄像头看到的内容的大图（**图 8-5**）。这被称为*实时预览*（live preview），除非你对 `raspistill` 做出其他指令，否则它将持续 5 秒。在这 5 秒结束后，摄像头将拍摄一张静态照片并将其保存到你的主文件夹中，命名为 **test.jpg**。如果你想再次拍摄一张，请再次输入相同的命令——但务必更改 **-o** 之后的输出文件名，否则你将覆盖掉第一张照片！

![](img/0aff4cdab15427839fb48fd7c6f677d3_200_0.png)

**图 8-5**：摄像头的实时预览

如果实时预览是倒着的，你需要告诉 `raspistill` 摄像头已旋转。摄像头模块的设计是为了处理从底部边缘伸出的排排线；如果它通过某些第三方摄像头支架配件从侧面或顶部伸出，你可以使用 **-rot** 开关将图像旋转 90、180 或 270 度。对于电缆从顶部伸出的摄像头，只需使用以下命令：

```
raspistill -rot 180 -o test.jpg
```

如果排排线从右侧边缘伸出，请使用 90 度的旋转值；如果它从左侧边缘伸出，请使用 270 度。如果你原始的拍摄角度不对，尝试使用 **-rot** 开关使用另一个来纠正它。

要查看你的照片，请从树莓菜单的“附件”类别打开文件管理器：你拍摄的名为 test.jpg 的图像将位于你的 `home/pi` 文件夹中。在文件列表中找到它，然后双击在图像查看器中加载它（图 8-6）。你还可以将图像附加到电子邮件、通过浏览器上传到网站或将其将其到外部存储设备。

![](img/0aff4cdab15427839fb48fd7c6f677d3_201_0.png)

图 8-6：打开拍摄的图像

### 介绍 picamera

控制摄像头模块或高清摄像头最灵活的方法是使用 Python，通过方便的 `picamera` 库。这让你对摄像头的预览、拍照和视频拍摄能力具有完全控制权，并允许你将它们集成到自己的程序中——甚至可以将它们与通过 GPIO Zero 库使用 GPIO 模块的程序相结合！

> PYTHON 编程
