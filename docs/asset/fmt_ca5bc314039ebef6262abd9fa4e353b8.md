
```ruby
with_tempo 200

play_pattern [40,25,45,25,25,50,50]

2.times do
  with_synth "beep"
    play_pattern [40,25,45,25,25,50,50]
    play_pattern [40,25,45,25,25,50,50].reverse
  end

play_pad "saws", 3

in_thread do
  with_synth "fm"
    6.times do
      if rand < 0.5
        play 30
      else
        play 50
      end
      sleep 2
    end
  end

2.times do
  play_synth "pretty_bell"
  play_pattern [40,25,45,25,25,50,50]
  play_pattern [40,25,45,25,25,50,50].reverse
end
```

#### 你将学到...

1. **如何编码**
   Sonic Pi 的编码风格使用标准编程语言的概念——如 `if` 语句、循环、线程等。Scratch 教授这种逻辑，而 Sonic Pi 教授它们的结构。

2. **机器人语音**
   使用 Sonic Pi 创建上下文相关的芯片声、吱吱声和蜂鸣声，并让它在宣传世界时使用熟悉的语音。

3. **MIDI**
   乐器数字接口（MIDI）是数字音乐的标准，Sonic Pi 中使用的数字和音调利用了这一点。

### 树莓派语音合成器

**使用通用的 eSpeak Python 库为你的树莓派项目添加语音功能**

得益于 eSpeak，让你的树莓派说话比你想象的要容易

#### 所需材料

- 便携式 USB 扬声器
- `python-espeak` 模块
- eSpeak
- Raspbian（最新镜像）

我们在之前的期中展示了树莓派如何用于为机器人供电，作为一台微型计算机，它也可以成为你家中或办公室中物联网的中心。

基于这些原因以及其他原因，使用树莓派进行文本到语音的命令可能正是你在寻找的。由于 Raspbian 基于 Debian，功能强大的 eSpeak 库很容易获取，任何人都可以使用它。此外，还有一个模块允许你在 Python 中使用 eSpeak，超越了标准的命令行提示，因此你可以执行自动化任务。

![](img/a1548a579bd09ff29b2b92de3f565e63_11_1.png)

##### 01 你需要的一切

我们将一次性安装本教程计划使用的所有软件。这包括 eSpeak 库和我们需要展示其功能的 Python 模块。打开终端并使用以下命令安装：

```
$ sudo apt-get install espeak python-espeak python-tk
```

![](img/a1548a579bd09ff29b2b92de3f565e63_12_0.png)

##### 02 树莓派的第一句话

eSpeak 库使用起来相当简单——要让它只是说点什么，在终端中输入：

```
$ espeak "message"
```

这将使用该库的默认设置朗读消息中写的内容，清晰度适中。

##### 03 多说几句

你可以使用多个不同的选项改变 eSpeak 朗读文本的方式，例如性别、阅读速度甚至音节发音方式。例如，像这样编写命令：

```
$ espeak -ven+f3 -k5 -si50 "message"
```

...将使语音变为女性，强调大写字母并减慢阅读速度。

![](img/a1548a579bd09ff29b2b92de3f565e63_12_1.png)

##### 04 用 Python 执行命令

在 Python 中使用 eSpeak 最基本的方法是使用 `subprocess` 直接调用命令行函数。在 Python 脚本中导入 `subprocess`，然后使用：

```
subprocess.call(["espeak", "[Options 1]", "[Option 2]",..."[Option n]", "message"])
```

消息可以从变量中获取。

##### 05 母语功能

Python 的 eSpeak 模块相当简单，只需将文本转换为语音即可。试试这段示例代码：

```
from espeak import espeak 
espeak.synth("message")
```

然后你可以将其集成到 Python 中，就像使用任何其他模块一样，用于自动化。

![](img/a1548a579bd09ff29b2b92de3f565e63_12_2.png)

##### 06 语音合成器

使用代码列表，我们正在使用 `Tkinter` 创建一个简单的界面，包含一些预设的语音按钮和自定义输入方法。我们展示了如何操纵 eSpeak 模块来改变其输出。这可用于阅读推文或自动消息。祝你玩得愉快！

#### 完整代码列表

```python
from espeak import espeak 
from Tkinter import * 
from datetime import datetime
```

*导入必要的 eSpeak 和 GUI 模块，以及用于获取时间的模块*

```python
def hello_world(): 
    espeak.synth("Hello World")

def time_now(): 
    t = datetime.now().strftime("%k %M") 
    espeak.synth("The time is %s" % t)
```

*定义界面将使用的不同函数，包括一个简单的固定消息、报时和自定义消息*

```python
def read_text(): 
    text_to_read = input_text.get() 
    espeak.synth(text_to_read)
```

```python
root = Tk() 
root.title("Voice box") 
input_text = StringVar() 
box = Frame(root, height = 200, width = 500) 
box.pack_propagate(0) 
box.pack(padx = 5, pady = 5)
```

*使用 Tkinter 创建界面的基本窗口，同时创建用于文本输入的变量*

```python
Label(box, text="Enter text").pack() 
entry_text = Entry(box, exportselection = 0, 
textvariable = input_text) 
entry_ready = Button(box, text = "Read this", 
command = read_text) 
entry_ready.pack()

hello_button = Button(box, text = "Hello World", 
command = hello_world) 
hello_button.pack() 
time_button = Button(box, text = "What's the time", 
command = time_now) 
time_button.pack()
```

*文本输入将附加到我们创建的变量中，每个按钮调用我们在代码上方定义的特定函数*

```python
root.mainloop()
```

获取代码：bit.ly/14XbLOC

## 10 个实用的树莓派项目

### 用 Minecraft-Pi 编程

通过玩有史以来最伟大的游戏之一来学习编程！

#### 你需要的内容

- Raspbian（最新发布版）
- Minecraft-Pi tarball 压缩包
- 键盘和鼠标
- 互联网连接

**Minecraft 可能是目前地球上最大的游戏。** 它几乎存在于你能想象的任何平台上，从 PC、游戏主机到手机。因此，它也可以运行在树莓派上也不足为奇。乍一看，Minecraft-Pi 是口袋版（专为平板电脑和智能手机设计）的简化版，但树莓派版非常特别，因为它是唯一允许用户访问其 API（应用程序接口）的 Minecraft 版本。在本项目中，我们将向你展示如何安装和配置 Minecraft-Pi，以便你可以以前所未有的方式与 Minecraft 进行交互。这个小项目仅仅是冰山一角……

![](img/a1548a579bd09ff29b2b92de3f565e63_13_0.png)

#### 01 需求

Minecraft-Pi 要求你的树莓派运行 Raspbian 系统，因此如果你还没有运行该系统，请前往 raspberrypi.org 进行设置。它还需要你加载 X Window。假设你处于命令提示符下，只需输入 `startx` 即可进入桌面。

![](img/a1548a579bd09ff29b2b92de3f565e63_13_1.png)
