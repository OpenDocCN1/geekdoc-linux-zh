
球击中了玩家屏幕的底部，现在我们来添加一些游戏结束代码来处理这些情况（图 08）。并将图 09 所示的代码添加到 `breakout.py` 中。这应该能完全处理失败或胜利的情况，弹出一个带有适当消息的弹出框，并提供一个重试的按钮。最后，我们必须处理当球击中方块时销毁球（图 10）。

这完全涵盖了所有最后的条件，通过 kivy 的 `build_collide_method` 比较它们的边界框（`pos` 和 `size`）来检查碰撞。反弹将取决于球穿透了多远距离，因为我们将告诉它已经击中了方块（`Block`）。

大功告成了，你可以运行代码来玩你简单的打砖块游戏。目前它非常简单，但希望你能看到为不同类型的方块和增强道具添加额外行为的不同方法——你可以添加生命值系统、更复杂的球拍/球交互，或者构建一个带有菜单和设置界面的完整游戏界面。

我们刚刚结束展示一个你可以做的酷炫功能——为你的游戏编译为 Android 版本！通而言之，可以将任何 Kivy 应用程序转换为可以在你的任何 Android 设备上运行的 Android APK。你甚至可以访问标准的 Android API 来访问硬件或 OS 特性，如振动、传感器或原生通知。

我们将使用 Buildtool 来构建 Android，它是 Kivy 的一个姐妹项目，封装了其他构建工具以创建不同的系统。该工具会处理下载和运行 Android 构建工具（SDK、NDK 和 Kivy 的 Python-for-android）以创建 APK。

```python
size_hint: None, None
proper_size: min(3*self.parent.height,3*self.parent.width)
size: self.proper_size,self.proper_size
# canvas part
```

图 06

```python
from kivy.clock import Clock
from kivy.core.window import Window
from kivy.utils import platform
```

```python
class Game(FloatLayout):
    def update(self, dt):
        self.ball.update(dt) # Not defined yet
        self.player.update(dt) # Not defined yet
```

图 04

```python
import random

class Ball(Widget):
    def __init__(self,**kwargs):
        super(Ball,self).__init__(**kwargs)
        self.colour = random.choice((0.78,0.63,0.28),(0.25,0))
    def start(self,*args):
        Clock.schedule_interval(self.update, 1./60.)
```

图 05

```kvivy
<Widget>:
    size_hint: 0.09, 0.05
    # canvas part
<Player>:
    size_hint: 0.1, 0.25
    position: {'x': self.position,'y': 0.1}
    # canvas part
<Ball>:
    size_hint: {'x': self.pos_hint_x,'y': self.pos_hint_y}
```

```python
def reset(self):
    for block in self.blocks:
        self.remove_widget(block)
    self.blocks = []
    self.setup_()
    self.ball.velocity = [random.random(),0.5]
    self.player.position = 0.5
```

```python
class BreakoutApp(App):
    def build(self):
```

![](img/c72194f2c3aec198936695a665a5167c_35_0.png)

# 使用 Python 构建 Android 应用程序

# 介绍 Python

图 09

```python
g = Game()
if platform() != 'android':
```

# 介绍 Python

## 50 个 Python 技巧

![](img/c72194f2c3aec198936695a665a5167c_39_0.png)

# 50 个 Python 技巧

Python 是一种让你工作更快速、更有效地整合系统的编程语言。今天，Python 是开源领域最流行的语言之一。环顾四周，你会发现它无处不在，从各种配置工具到 XML 解析。这里是 50 个精华集合，让你的 Python 体验变得有所价值……

## 基础

### 运行 Python 脚本

- 01 在大多数的 UNIX 系统上，你可以从命令行运行 Python 脚本。

```bash
$ python myprogram.py
```

### 从 Python 解释器运行 Python 程序

- 02 交互式解释器让你能够轻松尝试编程的第一步并使用所有的 Python 命令。你只需要逐一个输入每个命令，结果会立即显示。

可以使用以下命令启动 Python 解释器：

```bash
$ python
Kunal@ubuntu:~$ Python 2.6.2 (release-2$main, Apr 19 2009, 01:56:41) [GCC 4.3] on linux
Type "help", "copyright", "credits" or "license" 获取更多信息.
>>> commands here>>
```

在本文中，所有的 `>>>` 符号都表示在 Python 提示符处输入。

记住，Python 对此非常严谨——如果你接收到任何错误，请修正制表符间进。

## 动态类型

- 03 在 Java、C++ 和其他静态类型语言中，你必须为每个参数指定返回值的类型。相反，Python 是一种动态类型语言。在 Python 中，你永远不需要指定所使用的任何值的类型。基于此，Python 会自动跟踪数据类型。

## Python 语句

- 04 Python 使用换行符来分隔语句，使用冒号和缩进来分隔代码块。大多数编译语言（如 C 和 C++）使用分号来分隔语句，使用括号来表示代码块。

## == 和 = 运算符

- 05 Python 使用 `==` 进行比较，使用 `!=` 进行不等于赋值：Python 不支持内联赋值，因此在你实际上想要比较它时，没有意外赋值的可能。

## 字符串拼接

- 06 你可以使用 `+` 来拼接字符串。

```python
>>> print 'kunal'+'al'
kunal
```

## __init__ 方法

- 07 当类的实例创建时，会立即运行 `__init__` 方法。该方法用于对你的对象进行任何你想要的初始化：`__init__` 类似于 C++ 或 Java 中的构造函数。

示例：

```python
Class:
    def __init__(self, name):
        self.name = name
    def hi(self):
        print('Hello, my name is ' + self.name)
```

```python
p = Person('Kunal')
p.hi()
```

输出：

```
Hello, my name is Kunal
```

## 模块

- 08 为了让你的程序随着规模的扩大而保持可维护性，你可能想将它们分成几个文件。Python 允许你将多个函数定义放在一个文件中，然后将其作为模块导入使用。这些文件必须具有 `.py` 扩展名。

```python
>> print '\n'.join(mylist)
spam
ham
```

### 向 Python 脚本传递参数

示例：

```python
# file_function.py
def min_max(a,b):
    if a < b:
        max = a, b
    else:
        min = b, a
    return min
# 模块用法
import my_function
```

### Python 解释器中的 Tab 补全

- 11 Python 允许你在调用脚本时访问传递给脚本的内容。命令行内容存储在 `sys.argv` 中。

```python
import sys
print sys.argv
```

### 加载模块和启动

- 15 你可以通过解释你的 `.python_file`（或 Python 启动时读取的文件）的想法来实现自动补全：
