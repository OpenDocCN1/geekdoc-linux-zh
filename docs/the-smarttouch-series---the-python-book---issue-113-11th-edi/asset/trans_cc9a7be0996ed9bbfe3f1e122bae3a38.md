
## 手势控制

![](img/e016e192a91ffc1a9e474690a590742f_163_0.png)

## 17 Skywriter 动作

Pimoroni Skywriter HAT 是一款电气近场 3D 手势感应板，采用 4 层 PCB 设计以实现最佳的感应性能，有效距离可达 5 厘米！它能够采集完整的 3D 位置数据和手势信息（滑动、轻点、双击、快速滑动和旋转），并对你设定的动作做出响应。此外，它还以完整组装的形式提供。

## 18 安装软件

Pimoroni 让 Skywriter HAT 的软件安装变得极其简单。打开 LX 终端并输入以下命令：

```bash
sudo curl -sS get-pimoroni.com/skywriter | bash
```

请遵循屏幕上显示的说明；这些步骤包括授予安装软件的权限以及同意库所需的更改。这将下载所需的库以及一组 Skywriter 示例和程序供你尝试。安装完成后，重启你的 Raspberry Pi，然后即可开始流程的下一部分。

## 19 你的第一个 Skywriter 程序

新建一个 Python 文件（记得使用步骤 6 中介绍的 LX 终端方法，因为需要管理员权限），并添加以下代码。首先，导入与 Skywriter 通信的库，即第 1 行和第 2 行。接下来，创建一个名为 `move` 的函数，用于感应手指在 Skywriter 上的位置，这是第 3 行。然后读取 x、y 和 z 坐标，这是第 4 行，最后将这些坐标打印到 Python 窗口中。保存并运行程序。将手指移过 Skywriter 上方。请注意，由于其具有触摸电容特性，你无需实际接触电路板，只需悬停在其上方即可。

```python
import signal
import skywriter

@skywriter.move()
def move(x, y, z):
    print(x, y, z)
```

![](img/e016e192a91ffc1a9e474690a590742f_163_1.png)

### 在 Pi 上使用 Python

```text
login as: pi
pi@192.168.1.219's password:

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Sun Sep 18 07:27:00 2016 from dan-pc.default
pi@raspberrypi:~$ sudo curl -sS get-pimoroni.com/skywriter | bash

This script will install everything needed to use
the Pimoroni Skywriter

=== Warning ===

Always be careful when running scripts and commands
copied from the internet. Ensure they are from a
trusted source.

If you want to see what this script does before
running it, you should run:
curl -sS https://get-pimoroni.com/skywriter

Note: Skywriter requires I2C communication

Do you wish to continue? [y/N]
```

### 新型 Skywriter 板

Pimoroni 开发了一款更大的 Skywriter 手势板，它可以在三维空间中工作。它可以在最远 15 厘米的距离内感应你的手势，这意味着你可以将其嵌入非导电材料下方。这使其非常适合可穿戴设备以及需要隐藏电路板的项目。它能够识别所有常见手势，如轻点、快速滑动和双击，但可以在更远的距离完成这些动作。你甚至可以将其用作鼠标或键盘。点击此处了解更多详情：http://bit.ly/2dJF0sw

### 20 双击

在这个程序中，你可以双击 Skywriter 电路板的某一部分，它会告诉你双击的位置。这里使用了一个名为 `position` 的变量，第 3 行，它根据你的触摸位置将双击位置存储为北、东、南、西或中心。第 4 行打印出你双击的位置。例如，如果你在电路板顶部双击，它将打印：Double tap! North。在每次轻点后，所有信号都会被清除，以确保每次轻点都能被明确识别，这是第 5 行。保存并运行程序；轻点，轻点。

```python
import skywriter

@skywriter.tap()
def tap2(position):
    print('Tap!', position)
    if position == 'north':
        print('North')
    elif position == 'south':
        print("South")
```

### 21 单次轻点

当执行任何手势，如轻点、双击、触摸、快速滑动等时，你可以识别该手势在 Skywriter 电路板上的位置并做出特定的动作响应。例如，你可以触摸电路板的顶部；这是向北轻点（North tap）。右边是东（East），底部是南（South），左边是西（West）。可以使用条件语句来检查你触摸 Skywriter 的物理位置，然后返回五种响应之一。

```python
import signal
import skywriter

def doubletap(position):
    print('Double tap!', position)

signal.pause()
```

### 23 降低响应速度

双击是指在短时间内快速按下 Skywriter 两次，而轻点则是单次按下。但是，如果你先按一次然后再按一次，它会被解释为双击。你可能会想知道轻点和双击是如何区分的。为了解决这个问题，请在轻点代码中添加一个独立的速率（rate）。这意味着该动作，即轻点，仅重复一次。如果你仍然觉得这两种手势区分不够明显，请增加重复速率的值。

```python
@skywriter.tap(repeat_rate=1)
```

### 24 感应快速滑动

另一种你可以检测的实用手势是快速滑动（flick）。只需设置 Skywriter 等待快速滑动，这是第 1 行。然后创建一个函数来识别快速滑动并记录其方向，例如从南到北或从东到西，这是第 2 行。然后打印确认信息，表明已检测到快速滑动，包括快速滑动方向的起始位置和结束位置，这是第 3 行。

```python
@skywriter.flick()
def flick(start, finish):
    print('Got a flick!', start, finish)
```

### 22 感应位置

创建一个新的函数，用于感应用户轻点电路板时，这是第 3 行，然后等待轻点并记录用户在电路板上触摸的位置。这存储在名为 `position` 的变量中，这是第 4 行。添加一个 if 语句，这是第 6 行，用于检查和比较位置。如果在电路板顶部（即北侧位置）被轻点，则打印 'north'。使用 elif 语句，这是第 8 行，来检查电路板底部（即南侧位置）的轻点。保存程序并运行它。

```python
import signal
```

## 25 编辑你的机器人代码

既然你已经尝试过一些 Skywriter 命令，你可以使用并改编这些命令来控制机械臂。打开步骤 16 中的前一个机械臂文件，并在程序窗口顶部导入额外的所需库。

```python
import skywriter
import signal
```

![](img/e016e192a91ffc1a9e474690a590742f_165_0.png)

## 26 添加 Skywriter 动作以抬起肘部

接下来，添加基于 Skywriter 感应到的手势来控制机器人的代码。在该函数下，设置 `touch` 命令以注册触摸，这是第 1 行，并创建一个变量来保存你按下电路板的位置，如北、南、东等，这是第 2 行。现在检查位置，并使用 `if` 语句检查是否触摸了北侧位置，这是第 3 行。如果已触摸，则使用机械臂代码移动机械臂，这是第 4 行。最后，打印一条简短消息，告知用户肘部现已抬起。

```python
@skywriter.touch(repeat_rate=1)  # Raise / lower the wrist
def touch(position2):
    if position2 == 'north':
        MoveArm1([16,0,0])  # elbow up
        print("Elbow Up")
```

![](img/e016e192a91ffc1a9e474690a590742f_165_1.png)

## 27 添加更多触摸动作

现在为程序添加更多动作。在下一行，并与其 `if` 语句位置对齐缩进，添加一个 `elif` 语句以检查是否触摸了南侧位置，这是第 1 行。如果你在电路板底部（即南侧位置）触摸，它将注册响应并向下移动肘部，这是第 2 行。按 F5 保存你的程序，然后运行并测试它。

```python
elif position2 == 'south':
    MoveArm1([32,0,0])  # elbow down
```

## 28 添加握力控制

继续构建并将机械臂动作分配给你做出的各种手势。在之前的代码行下方，添加另一个 `elif` 语句以检查西侧位置，这是第 1 行，然后使用机械臂命令代码打开握力，这是第 2 行。通过在 Skywriter 上触摸东侧位置来关闭握力，这是第 3 行，然后添加关闭握力的代码，这是第 4 行。

```python
elif position2 == 'west':
    MoveArm1([1,0,0])  # grip close
elif position2 == 'east':
    MoveArm1([2,0,0])  # grip open
```

## 29 使用轻点

Skywriter 的任何手势都可以用来控制机械臂。在新的一行中，创建一个新函数以识别轻点，这是第 1 行。请注意，重复速率设置为 1，以排除双击的可能性。接下来创建一个名为 `position1` 的新变量，这是第 2 行。这是为了防止手势覆盖之前的变量（例如，如果灯已打开，你可能希望移动机械臂但保持灯开启）。在第 4 行，检查轻点的位置，然后打印机械臂将执行的动作，这是第 5 行（这是可选的）。与前几步一样，分配机械臂的动作代码；例如，向上移动肩部，这是第 6 行。

```python
@skywriter.tap(repeat_rate=1)
def tap_tap(position1):
    print("Tap", position1)
    if position1 == 'north':
        print("Shoulder Up!")
        MoveArm1([64,0,0])  # shoulder up
```

## 30 肩部向下

要向下移动肩部，请使用与步骤 27 类似的格式。在下一行，与 `if` 语句的缩进级别对齐，添加一个 `elif` 语句以检查南侧位置的轻点，这是第 1 行。添加一个可选的 print 语句以显示已注册轻点，这是第 2 行，然后添加向下移动肩部的命令，这是第 3 行。保存并运行你的程序。

```python
elif position1 == 'south':
    print("Shoulder Down!")
    MoveArm1([128,0,0])  # shoulder down
```

## 31 将所有内容整合在一起

以类似于步骤 26 到 30 中展示的方式继续创建你的程序。首先选择你想要使用的手势/输入类型，然后设置一个函数来识别该手势及其在 Skywriter 上发生的位置，例如北、南、西等。接下来，使用条件语句，`if` 和 `elif`，来检查位置，然后使用完整列表中的代码以机械臂动作做出响应。使用教程资源中的示例程序作为你创意的基础设置，然后进行扩展和自定义，添加你自己的手势和动作。

