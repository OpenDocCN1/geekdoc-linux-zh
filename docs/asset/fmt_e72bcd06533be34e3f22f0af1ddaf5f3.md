
# 树莓派官方新手指南

点击运行，你将看到加速度的值打印到 Python 终端中（图 27）。与你之前的程序不同，这些将连续打印；要停止它们，点击红色停止按钮停止程序。

![](img/0aff4cdab15427839fb48fd7c6f677d3_183_0.png)

**图 27：** 舍入到最接近整数的加速度读数

你可能已经注意到加速度告诉你其中轴——如果你的树莓派平放在桌子上，则是 Z 轴——加速度值为 1.0 重力（1G），这意味着 Sense HAT 并没有移动。这是因为它正在检测地球的引力——这种将 Sense HAT 拉向地球中心的力量，也是当你从桌子上撞掉东西时会掉到地板上的原因。

在程序运行时，小心拿起并旋转 Sense HAT 和树莓派——但要确保不要弄掉它的任何电缆！当树莓派的网络端口和 USB 端口指向地板时，你会看到变化，此时 Z 轴显示为 0G，X 轴显示为 1G；再次旋转让 HDMI 和电源端口指向地板，现在 Y 轴显示为 1G。如果你反过来操作让 HDMI 端口指向天花板，你会在 Y 轴上看到 -1G。

利用地球引力约为 1G 的知识以及你对空间轴的知识，使用加速度读数判断哪个方向是向下——同样，哪个是向上。你还可以用它来检测运动：小心摇晃 Sense HAT 和树莓派，并在操作时观察数字：摇得越剧烈，加速度越大。

在使用 `sense.accelerometer_raw()` 时，你是在告诉 Sense HAT 关闭 IMU 中的其他传感器（陀螺仪和磁力计），并仅返回来自加速度的数据。自然，你也可以对其他传感器执行相同的操作。

找到 `acceleration = sense.get_accelerometer_raw()` 这一行，并改为：

```python
orientation = sense.get_gyroscope_raw()
```

你也可以对其他传感器做同样的事情。运行程序，你将看到 Sense HAT 在三个轴上的方向舍入到最接近的整数。通过点击红色停止按钮停止程序。要使用磁力计，删除程序中除第一行以外的所有内容，然后在 `while True` 下方输入：

```python
north = sense.get_compass()
print(north)
```

运行程序，你将在 Python 终端反复打印磁北。小心旋转 Sense HAT，你会看到相对于北极的变化：你制作了一个指南针！尝试移动它，看看会发生什么。

## 挑战：自动旋转

利用你学到的关于 LED 矩阵和惯性测量单元的知识，你可以编写一个根据 Sense HAT 位置旋转图像的程序。

![](img/0aff4cdab15427839fb48fd7c6f677d3 185_0.png)

## 摇杆控制

Sense HAT 的摇杆位于右下角，虽然很小但功能非常强大：除了提供四个方向（上、下、左、右）的输入外，还有一个第五个输入，可以通过像按钮开关一样按下它触发。

> 警告！只有在在本节开头描述安装了垫圈后才能使用摇杆。如果没有垫圈，按下摇杆会导致 Sense HAT 板板弯曲，并损坏 Sense HAT 和树莓派的 GPIO 引脚。

![](img/0aff4cdab15427839fb48fd7c6f677d3_185_1.png)

## Scratch 中的摇杆控制

在 Scratch 中启动一个新程序并加载 Raspberry Pi Sense HAT 扩展。像以前一样，将一个 `when clicked`（点击单击）模块拖到脚本区域，在下方拖入一个 `clear display`（清除显示）模块，接着拖入并编辑一个 `set background to black`（背景设置为黑色）和一个 `set colour to white`（颜色设置为白色）模块。

在 Scratch 中，Sense HAT 的摇杆映射到键盘上的方向键：向上推摇杆等于按下向上键，向下推等于向下键，向左推等于左箭头键，向右推等于右箭头键；同时，像按钮开关一样向按下摇杆等于按下回车键。

> 警告！摇杆控制仅适用于实体 Sense HAT。当使用 Sense HAT 模拟器时，请使用键盘上相应的键来模拟摇杆按下。

![](img/0aff4cdab15427839fb48fd7c6f677d3_185_2.png)

将一个 `当 摇杆被按下时` 模块拖到你的代码区域。然后，为了让它执行动作，在其下方拖入一个 `说 Hello! 2秒` 模块。

![](img/0aff4cdab15427839fb48fd7c6f677d3_186_0.png)

向上推动摇杆，你会看到 Scratch 小猫说一句开心的“Hello！”。接下来，将 `说 Hello! 2秒` 模块修改为 `说 Joystick Up! 2秒` 模块，并继续添加“事件”（Events）和“外观”（Looks）积木块，直到你为摇杆的五种按下方式都准备好了相应的代码。

![](img/0aff4cdab15427839fb48fd7c6f677d3_186_1.png)

![](img/0aff4cdab15427839fb48fd7c6f677d3_186_2.png)

![](img/0aff4cdab15427839fb48fd7c6f677d3_186_3.png)

![](img/0aff4cdab15427839fb48fd7c6f677d3_186_4.png)

![](img/0aff4cdab15427839fb48fd7c6f677d3_186_5.png)

尝试向各个方向推动摇杆，看看你的消息出现！

![](img/0aff4cdab15427839fb48fd7c6f677d3_187_0.png)

# 终极挑战

你能使用 Sense HAT 的摇杆来控制舞台区域上的 Scratch 角色吗？你能实现当角色收集到另一个代表物体的角色时，让 Sense HAT 的 LED 显示显示一条开心的消息吗？

## Python 中的摇杆控制

在 Thonny 中启动一个新程序并将其保存为 `Sense HAT Joystick`。从设置 Sense HAT 并清空 LED 矩阵的常用代码开始：

```
from sense_hat import SenseHat
sense = SenseHat()
sense.clear()
```

接下来，设置一个无限循环：

```
while True:
```

然后使用以下代码告诉 Python 监听来自 Sense HAT 摇杆的输入，Thonny 会自动对其进行缩进：

```
for event in sense.stick.get_events():
```

最后，添加以下代码——Thonny 同样会为你缩进——以便在检测到摇杆按下时执行操作：

```
print(event.direction, event.action)
```

点击“运行”（Run），并尝试向各个方向推动摇杆。你会看到 Python 控制台区域打印出你所选择的方向：上、下、左、右，以及当你像按下按钮一样向下推摇杆时的情况。

每当你推动一次摇杆，你都会收到两个事件：一个 `pressed`（按下）事件，用于在你第一次按下某个方向时触发；另一个 `released`（松开）事件，用于摇杆返回中心时触发。你可以在程序中使用这些：想象游戏中的一个角色，可以被设置为在摇杆按下某个方向时开始移动，在松开时停止。

你还可以使用摇杆来触发函数，而不是局限于使用 `for` 循环。删除 `sense.clear()` 下的所有内容并并以下内容：

```python
def red():
    sense.clear(255, 0, 0)

def blue():
    sense.clear(0, 0, 255)

def green():
    sense.clear(0, 255, 0)

def yellow():
    sense.clear(255, 255, 0)
```

这些函数会将整个 Sense HAT 矩阵更改为单色：红、蓝、绿或黄——这将让你极易观察到程序是否运行正常！要实际触发它们，你需要告诉 Python 哪个函数对应哪个摇杆输入。输入以下行：

```python
sense.stick.direction_up = red
sense.stick.direction_down = blue
sense.stick.direction_left = green
sense.stick.direction_right = yellow
sense.stick.direction_middle = sense.clear
```

最后，程序需要一个无限循环（被称为主循环）以便保持运行，从而持续监测摇杆输入，而不是在运行完你写的代码后就退出。输入以下两行：

```python
while True:
    pass
```

点击“运行”（Run），并尝试摇杆：你会看到 LED 亮起绚丽的颜色！要关闭 LED，像按下按钮一样推动摇杆：中间方向被设置为使用 `sense.clear()` 函数来关闭所有。恭喜你：你可以捕捉来自摇杆的输入了！

# 终极挑战
