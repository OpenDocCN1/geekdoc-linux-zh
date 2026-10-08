

## 01 组装你的机械臂

机械臂以套件形式提供，并附带一套详细的说明书，涵盖如何组装各个部件以及如何将它们组合成最终的机械臂。这个过程大约需要三个小时左右，非常适合在下雨天打发时间。机械臂套件包含所需的所有部件，但电池除外。最难的部分在于确保接线方向正确。如果接反了，虽然不会损坏机械臂，但会导致机械臂的运动方向与编程设定的方向相反。

## 02 更新你的树莓派

组装好机械臂后，插入你的树莓派并开机。此时请勿连接机械臂。首先更新软件和操作系统。确保你的树莓派已连接到互联网，打开 LX 终端窗口并输入：

```
sudo apt-get update
sudo apt-get upgrade
```

等待软件下载并安装完成后，输入 `sudo reboot` 重启系统。

## 03 安装 USB 软件

要使用 Python 编程语言与你的机械臂进行交互，首先需安装 PyUSB 模块。它提供了 Python 与树莓派通用串行总线（USB）之间的连接，以便轻松访问机械臂插入的 USB 端口。

在终端窗口中，输入：

```
sudo git clone https://github.com/wallac/pyusb.git
```

安装完成后，进入 pyusb 文件夹，输入 `cd pyusb`，然后输入代码 `sudo python setup.py install`。这将安装所需的模块。最后，使用 `sudo reboot` 重启树莓派。

![](img/e016e192a91ffc1a9e474690a590742f_160_0.png)

## 04 将机械臂连接到树莓派

既然已经安装了编程机械臂所需的软件，现在可以将其插入。只需将机械臂上的 USB 线插入树莓派上任意一个可用的 USB 接口即可。使用机械臂底座上的电源开关打开机械臂电源。你可以通过打开 LX 终端并输入 `sudo lsusb` 来测试连接是否生效以及机械臂是否被识别。这将返回连接到 USB 端口的硬件列表。

![](img/e016e192a91ffc1a9e474690a590742f_160_1.png)

## 05 控制机械臂

通过 USB 向机械臂发送一行代码来控制机械臂。该代码包括每个动作的持续时间，以及用于识别需旋转哪些电机、开启或关闭以及旋转方向的坐标。实际用于移动机械臂的代码相当冗长，但 Python 将其简化为易于管理的单行代码。

![](img/e016e192a91ffc1a9e474690a590742f_160_2.png)

## 06 打开 Python

从任务栏菜单中选择并打开 LX 终端，双击该图标。通过 Python 访问机械臂需要管理员权限，因此请以 sudo 用户身份打开 Python。在 LX 终端中，输入 `sudo idle` 并按回车键。当 IDLE 加载完成后，打开一个新窗口，点击“文件”（File），然后选择“新窗口”（New Window）。

## 07 导入所需的库

在窗口顶部，创建你的程序。导入 time、核心 usb 和 usb 工具库，位于第 1 行。这些库使你能够向 USB 端口发送命令并控制机械臂。USB 是一种复杂的协议，但 PyUSB 为大多数常见配置提供了良好的默认值，从而减少了大量冗长代码的需求。time 库允许你在机械臂的每个动作之间添加短暂的延迟。添加如下代码行：

```
import usb.core, usb.util, time
```

![](img/e016e192a91ffc1a9e474690a590742f_160_3.png)

### 尝试不同的手势以找到适合你的

Skywriter 拥有许多你可以尝试并用于自己程序中的手势。例如，该板卡可用于检测你做出的圆形手势，这被称为空中滚轮（air wheel）。Skywriter 也非常适合控制其他项目，如调整音乐播放器的音量，或使用手势创作音乐或播放采样。请在 `https://github.com/pimoroni/skywriter-hat/tree/master/examples` 查看这些示例及其他更多示例的完整代码。

![](img/e016e192a91ffc1a9e474690a590742f_161_0.png)

### 机械臂动作

使用以下列表作为参考，查看机械臂的各种动作。每个 # 后的文本是注释，用于标识该命令。

- MoveArm(1,0,1,0,1) #逆时针旋转底座
- MoveArm(1,0,2,0,1) #顺时针旋转底座
- MoveArm(1,0,4,0,0) #肩部向上
- MoveArm(1,0,8,0,0) #肩部向下
- MoveArm(1,0,16,0,0) #肘部向上
- MoveArm(1,0,32,0,0) #肘部向下
- MoveArm(1,0,4,0,0) #手腕向上
- MoveArm(1,0,8,0,0) #手腕向下
- MoveArm(1,0,2,0,0) #夹爪打开
- MoveArm(1,0,1,0,0) #夹爪闭合
- MoveArm(1,0,0,1,1) #灯亮
- MoveArm(1,0,0,0,1) #灯灭

## 08 命名 USB 设备

现在使用 Python 查找 USB 机械臂。在下一行代码中，创建一个名为 RoboArm 的变量来存储机械臂位置的信息——这基本上就是它插入的是哪个 USB 端口。现在为插入树莓派 USB 端口的设备命名。为此，请输入 ID Vendor 号和产品 ID 详细信息以搜索机械臂。如果你使用的是不同的机械臂或型号，你需要找到这两个详细信息并替换代码行中的相应数值。

```
RoboArm=usb.core.find(idVendor=0x1267,idProduct=0x0000)
```

## 09 查找机械臂

下一步是搜索机械臂，以确保它已插入 USB 端口并且已通电。这使用了一个简单的条件语句（if 语句）来进行此检查。如果未找到机械臂，则向 Python 窗口返回一条错误消息，以提示你插入它、打开电源，或者两者都要做！注意，代码的第二行是缩进的。

```
if RoboArm is None:
    raise ValueError("Arm not found")
```

![](img/e016e192a91ffc1a9e474690a590742f_161_1.png)

## 10 创建函数，第 1 部分

你需要在机械臂的每个动作之间有一小段延迟。创建一个名为 Duration 的新变量，并赋予值 1。在下一行代码中，创建一个函数，其中包含你刚创建的持续时间值，以及停止机械臂运动的代码。在第 3 行，添加将运动命令传输到 USB 端口并中继给机械臂的代码。再次注意，该行是缩进的。

```
Duration = 1
def MoveArm(Duration, ArmCmd):
    #start the movement
    RoboArm.ctrl_transfer(0x40,6,0x100,0,ArmCmd,1000)
```

## 11 创建函数，第 2 部分

在下一行代码中，添加一个小的持续时间来设置动作时长的限制。在本例中，持续时间设置为 1，意味着每个动作或行为将发生一次。你可以通过更改步骤 10 中设置的值来实验持续时间。在每个动作发生后，它们需要停止。使用代码 ArmCmd=(0,0,0)（第两行）来准备停止电机旋转并结束动作的代码。

```
#stop the movement after specified duration
time.sleep(Duration)
ArmCmd=(0,0,0)
```

![](img/e016e192a91ffc1a9e474690a590742f_161_2.png)

### 使用 Python 配合树莓派

```
#!/usr/bin/env python

#import the USB and time libraries
import usb.core, usb.util, time

#allocate the name 'RoboArm' to the USB device
RoboArm=usb.core.find(idVendor=0x1267, idProduct=0x0000)

#Check to see if arm is detected
if RoboArm is None:
    raise ValueError("Arm not found")

#Create a variable for duration
Duration=1

#Define a procedure to execute each movement
def MoveArm(Duration, ArmCmd):
    #start the movement
    RoboArm.ctrl_transfer(0x40, 6, 0x100, 0, ArmCmd, 1000)
    #stop the movement after specified duration
    time.sleep(Duration)
    ArmCmd=(0,0,0)
    RoboArm.ctrl_transfer(0x40, 6, 0x100, 0, ArmCmd, 1000)
```

## 12 创建函数，第 3 部分

该函数的最后一部分是将停止命令发送给机械臂，第 1 行。这连接到机械臂，然后传输到你上一步设置的 ArmCmd=(0,0,0) 代码。请注意，它存储在一个名为 ArmCmd 的变量中，这意味着你可以更改传输给机械臂的命令。这一行也是缩进的。

```
RoboArm.ctrl_transfer(0x40, 6, 0x100, 0, ArmCmd, 1000)
```

## 13 运动和动作代码

完成函数后，你就可以使用它来控制机械臂。每个运动或动作都有一组独特的数字，用于标识运动的持续时间、需要开启或关闭哪些电机以及它们需要旋转的方向。每个命令都以 MoveArm 开头，然后第一个数字是运动的持续时间。例如，“1”基本上意味着执行此指令或动作一秒。随后是所需的信息以旋转电机：

```
MoveArm(1, [0,1,0]) #rotate base anti-clockwise
```

## 14 打开灯

在函数下方的下一行，添加打开灯的代码。输入命令 `MoveArm(1, [0,0,1]) #light on.`。#light on 是一个注释，控制机械臂时不需要它。它用于让用户识别该代码的作用：打开灯。当程序中有多条命令时，这很有用。

## 15 运行程序

现在你拥有了一个完整的程序，该程序将连接到 USB 端口，搜索机械臂，准备一个函数，然后传输控制机械臂的指令，即打开灯。将程序保存到主文件夹。一个简单的做法是按键盘上的 F5，命名并保存文件，按回车，然后它将运行。查看机械臂上的灯，它应该会亮起！

## 16 关闭灯

除非你编写代码使其关闭，否则灯将保持亮起。如果你直接在“打开”命令后添加这一行，灯将快速开闭，以至于你看不到。在下一行，添加一个两秒的短延迟（第 1 行），然后关闭灯（第 2 行）。使用 F5 按钮保存并运行你的程序。查看完整的代码列表，了解所有可用动作的代码。你可以使用这些代码行来构建动作并实验机械臂的功能。

