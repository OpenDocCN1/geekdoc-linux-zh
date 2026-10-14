
```python
def tag(position):
    print("Tag!")
    if position == "north":
        print("Shoulder")
        MoveArm(0,0,1) #Shoulder
```

## 30 肩部

要移动肩膀，使用与第 27 步相似的格式。在新的一行中，通过语句的缩进检查是否触碰了南侧位置（第 1 行）。添加 `if` 语句来显示动作（第 2 行），并添加移动肩膀动作的代码（第 3 行），然后运行你的程序。

```python
elif position == "south":
    print("Shoulder Down")
    MoveArm(0,-1,0) #shoulder
```

## 27 添加更多触碰动作

现在为程序添加更多动作。在 `if` 语句之后的新的一行，添加一个 `if` 语句检查是否触碰了南侧位置（第 1 行）。如果你在南、南、东或西等位置触碰板子，使用相应结果并移动肘部（第 2 行）。按 `F5` 保存你的程序，然后运行并测试。

```python
elif position == "south":
    MoveArm(1,3,2,0) #elbow down
```

## 整合一切

按照第 26 步所示的方法简单创建一个程序。现在按照第 6 到第 30 步操作。选择你想要使用的手势类型，然后设置一个函数来识别手势和板子上的位置。使用北、南、东、西等的代码，并使用 `if` 语句检查位置，使用文件中找到的代码通过机械臂动作做出响应。使用教程资源中的示例程序作为基础设置，以便你调整自己的想法并进行定制，以添加你自己的手势和动作。

166 Python 之书

![](img/516df994db593237169e2aff6d3e6840_166_0.png)

# 与树莓派一起使用 Python

# 使用树莓派改造玩具：第一部分

学习如何掌握四个简单的改造技巧，并将其嵌入玩具中

## 资源

- 一个旧/新玩具
- 电阻
- 小型圆盘电机
- LED
- 无电台
- 小型摄像头
- 母对母跳线

通过将旧玩具和树莓派相结合，你可以嵌入一些组件来创建你自己的增强玩具，它能对用户输入做出响应。例如，制作一个 3 英镑的 R2-D2 直播神器，让它亮起来、播放音乐并像你的手机一样直播。这个分部分教程涵盖了设置四个基本功能：用于眼睛的 LED、模拟电击的触感电机、来自隐藏摄像头的流以及广播到无线电台的星大战主题曲。你可以选择将这些与你自己的改造相结合，或将它们作为其他项目的独立功能使用。

不要局限于仅使用星大战玩具——我们使用 R2-D2 人偶是因为它便宜、易于获得且受欢迎，但你可以尝试的玩具没有限制。动作玩（前提是可以拆卸以放置元件）以及塑料和坚固的玩具都适合这种制作，特别是当它们伴随着有你可以广播的记忆点或音效的电影电视节目时。第二部分介绍了如何设置玩具以及设置触发器来启动功能。

![](img/516df994db593237169e2aff6d3e6840_167_0.png)

# 01 设置 LED

LED 的设置和控制非常简单。它们是你玩具的很好的补充，可以作为闪烁按钮，或者例如 R2-d2 的雷达眼。取并握住长的一脚；这是正极并连接到输入端。将线绕在脚上并固定。取负极并将其连接到另一个电机上。

# 02 连接 LED

取带有 `G17` 的正极线，它是物理引脚编号 11（看远端）。取负极并将其连接到另一个电机上。

# 03 点亮 LED

要开启 LED，请使用以下库。将引脚分配给变量。

```python
import time
from gpiozero import LED
led = LED(17)

while True:
    led.on()
    time.sleep(0.5)
    led.off()
    time.sleep(5)
```

# 04 添加振动

你可能希望玩具在移动时振动。R2-d2 以产生短振动而闻名，类似于触感。

```python
from gpiozero import Motor
vibration = Motor(9)
while True:
    vibration.on()
    time.sleep(0.5)
    vibration.off()
    time.sleep(5)
```

# 05 接线电机

将电机的正极（通常是红色）接线连接到 `GPIO 9`；这是物理引脚编号 21。黑线连接到地——最近的引脚是 25。

```python
import RPi.GPIO as GPIO
GPIO.setmode(GPIO.BCM)
import time
```

# 06 启动电机

要启动电机，设置输出引脚 9。这告诉程序 `GPIO 9` 是一个输出。接下来，将 `GPIO` 设置为高；这就像开启它。在将输出设置为低 之前添加暂停，这会让电机旋转。

```python
sudo apt-get install python3
GPIO.output(9, GPIO.HIGH)
time.sleep(0.5)
GPIO.output(9, GPIO.LOW)
```

# 07 挂摄像头

小型摄像头可以隐藏在玩具内部，拍摄照片或直播传输到笔记本电脑或移动设备。使用你的摄像头并小心剥离塑料外壳，留下电路板和镜头。根据你玩具的大小，调整外壳使其容纳

![](img/516df994db593237169e2aff6d3e6840_168_0.png)

# R2-d2 演示

查看 R2-d2 玩具的视频并查看功能的运行情况。这为你自己的玩具项目提供了很好的灵感。

![](img/516df994db593237169e2aff6d3e6840_168_1.png)

![](img/516df994db593237169e2aff6d3e6840_168_2.png)

The Python Book 169

# 在 Pi 上使用 Python

## 08 设置 IP 地址

每次你连接到互联网时，你的 Pi 都会赋予一个新的 IP 地址。这被称为动态 IP 地址。这可能会导致问题，当地址变化时，其他设备将无法定位你的 Pi。要创建一个静态的（IP 地址），请加载 LX 终端，输入 `ifconfig` 并记录 `inet addr` 和子掩码（Mask）数字，输入 `route -n` 并记录网关（Gateway）。输入 `sudo nano /etc/network/interfaces`，找到第一行 (`eth0`) 并将其更改为：

```
interface eth0 static
address 192.168.1.5
netmask 255.255.255.0
gateway 192.168.1.1
network 192.168.1.0
broadcast 192.168.1.255
```

将数字替换为你自己的（即你记录的那些）。按 `CTRL+X` 保存并退出编辑器。当你重启 Pi 时，它现在将拥有一个静态 IP 地址，在重启或重新连接时不会改变。

![](img/516df994db593237169e2aff6d3e6840_169_0.png)

## 11 配置软件 – 部分 2

接下来，找到设置为 8080 的流端口（`streamport`）。这是用于视频的，如果你查看流时遇到问题，可以更改它：8081 提供静态流。然后，找到 `Localhost` 行并设置为 `localhost`，以便通过 `control_port` 访问视频，如果你遇到流问题，也可以更改它。帧率是摄像头每秒捕捉的帧数。帧率越高，质量越好，但性能消耗越大且容易产生卡顿。设置 `post_capture` 并指定检测到运动后的帧数。

![](img/516df994db593237169e2aff6d3e6840_169_1.png)

## 09 安装 Web 服务器

要设置 Web 服务器，请使用 LX 终端并通过输入 `apt-get update` 和 `sudo apt-get upgrade` 更新你的 Raspberry Pi。接下来，安装控制摄像头的 Motion 服务器；输入 `sudo apt-get install motion`。完成后，重启 USB 摄像头并重启系统，你将看到摄像头已被识别。

## 12 运行 守护进程

守护进程（`daemon`）是在后台运行并提供服务的程序；在这个项目中，你不希望每次使用 Pi 时都手动启动 Motion。最好让它启动时自动运行。在 LX 终端中，输入 `nano /etc/motion/motion` 来编辑文件。要从启动时作为服务运行 motion，你需要将 `start_motion_daemon` 改为 `yes`

![](img/516df994db593237169e2aff6d3e6840_169_2.png)

### start_motion_daemon=yes

使用 `CTRL+X` 保存并退出文件，重启你的 Pi。

## 10 配置软件 – 部分 1

现在有几个配置可以从摄像头中获得最大的收益。你可以尝试这些配置以产生最佳结果。在 LX 终端中，

```
sudo nano /etc/motion/motion.conf
```
