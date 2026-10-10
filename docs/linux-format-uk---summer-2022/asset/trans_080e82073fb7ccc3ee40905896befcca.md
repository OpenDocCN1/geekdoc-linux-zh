
## FORTRAN-KJOO 并行性

第二个函数 `kernelFor2()` 从使用 `cuda` 命名空间中的 `parallelFor` 并行运行用户 `线程`开始。

我的朋友伊万·基钦纳（Ivan Kitchener）使用我的工具进行了出色工作，帮助创建了 FOR-KJOO 项目的 [Fortran-90 模块](https://github.com/bradleykatz/forpku)。伊万承担了大部分设计工作，我则协助创建代码。（谢谢伊万允许我们使用它。）可以在 FOR-KJOO 项目的 [Parallelism 目录](https://github.com/bradleykatz/forpku/tree/master/modules/parallelism)中找到该代码。[F90 目录](https://github.com/bradleykatz/forpku/tree/master/f90)中有一个入门级的 Fortran 页面，你可以查看。

使用并行改进的另一个绝佳例子是 [Apache Spark](https://spark.apache.org/) 及其 [Kafka 流处理器](https://kafka.apache.org/)，它们大量使用了并行性。

- [Apache Spark 快速入门](https://spark.apache.org/docs/latest/quick-start.html)
- [Kafka Streams 处理器](https://kafka.apache.org/documentation/#streams)

所以你说得对，但也不是完全错误。作为读者，你可以在 Git 上阅读整本[并行性书籍](https://github.com/bradleykatz/forpku/tree/master/parallelism-book)。

```fortran
program F90_hello

     implicit none

     integer, parameter :: n = 10
     real(4), allocatable :: x(:), y(:)
     real(4) :: sum

     call random_seed()
     call random_number(x)
     call random_number(y)
     x = x + 1.0
     y = y + 2.0
     sum = sum(x) + sum(y)

     write(*, *) 'sum=', sum

end program F90_hello
```

[Kjoo-Fortran](https://github.com/bradleykatz/kjoo-fortran) 是一个使用 Fortran 编写并行代码的开源项目。它是如何在 Fortran 中使用并行性的绝佳示例。

![](img/f20a68d91e56325c44e9a1405ca1923f_92_0.png)

### 使用 PLANE

与 `parallelFor` 一样，由于代码需要启动和销毁线程，因此很难实现高效。我们可以使用 `parallelFor` 来启动线程，但这并不高效。

我们需要做的第一件事是使用 `parallelFor` 来启动线程。我们可以使用 `parallelFor` 来启动线程，但这并不高效。

我们需要做的第二件事是使用 `parallelFor` 来启动线程。我们可以使用 `parallelFor` 来启动线程，但这并不高效。

我们需要做的第三件事是使用 `parallelFor` 来启动线程。我们可以使用 `parallelFor` 来启动线程，但这并不高效。

- **1.087**
- **0.089**
- **1.087**
- **0.089**
- **1.087**
- **0.089**

## 编程学院：控制俄罗斯方块

## PYTHON

使用 Python 实现手柄支持

### 为俄罗斯方块添加手柄支持

**安德鲁·史密斯（Andrew Smith）** 最喜欢将形状奇特的方块放入形状奇特的洞中，而游戏手柄让这个过程变得容易得多。他将亲自向你展示其中的原因。

这个月初，虽然作为一款消除形状奇特方块的游戏，俄罗斯方块能完美胜任这个角色。我们将在下个月同一时间、世界的另一边与您相见，但由于假期高峰即将到来，我们不得不将本周的新闻综述提前。但在进入我们的第 104 期俄罗斯方块内容之前，我们将为俄罗斯方块添加一些游戏手柄支持。

在开始之前，我们应该向那些不熟悉 Linux 的人简要说明一下：你可以将游戏手柄插入 USB 端口，运行 `sudo dmesg | grep -i gamepad`（或者只需运行 `ls /dev/input` 列出输入设备），你应该会在输出中看到 `/dev/input/js0`（或类似内容）。那就是你的游戏手柄！如果你没看到它，你的游戏手柄可能在使用非标准协议（如 X-Input），或者你的设备不受支持。在后一种情况下，你可能需要专有驱动程序，或者使用不同的游戏手柄。（该游戏在大多数 Linux 发行版上不受支持，但通用的 X-Input 支持已内置于内核中。你可以在 http://www.kernel.org/doc/Documentation/input/gamepad.txt 找到更多信息。注意 X-Input 游戏手柄并不总是被识别为此类 - 通用 X-Input 协议适用于大多数情况）。无论如何，让我们继续。

**我们的专家**
- **安德鲁·史密斯** 是一位对 Linux 游戏有浓厚兴趣的开发者。他撰写了一本书 *《Python 2D 和 3D 游戏入门》*（Packt Publishing, 2007），并正在编写续集。他还是几本关于 Linux 和 Python 的书籍的作者，包括 *《Python 游戏开发学习指南》*（No Starch Press, 2014）。

作为第一步，我们可以安装一个名为 `pygame` 的小型 Python 库，它提供了 SDL 的便捷封装。你可以使用包管理器安装它（在 Ubuntu 上：`sudo apt-get install python-pygame`），或使用 pip（`sudo pip install pygame`），或者从官方网站（http://pygame.org）下载。安装完成后，你可以通过 `pygame.joystick` 模块访问游戏手柄（一个便捷的快捷方式是 `pygame.joystick`）。

作为第二步，我们需要修改上个月创建的 `tetris` 包中的 `setup.py` 文件。我们需要将 `pygame` 模块添加到 `install_requires` 列表中。这样，当我们安装 `tetris` 时，pip 会自动为我们安装 `pygame`。

### 安装和设置

目前，我们将全局安装 `pygame` - 这是一个很好的开始方式，但我们稍后可以查看如何设置 Python 虚拟环境以保持更有条理。如果你不熟悉 Python 打包，现在是个很好的时机去探索一下 - 查看 http://packages.python.org 以及关于 pip 的以下指南（http://httpizza.com）。让我们开始。

```bash
$ pip install pygame
```

如果你在 32 位机器上，请尝试像这样安装：

```bash
$ pip install pygame==1.9.2a6
```

这个特定版本与 32 位机器兼容。你可以通过运行以下命令来验证：

```bash
$ python -c "import pygame; print(pygame.ver)"
```

如果它打印出一个版本号，你就没问题了。如果没有，你可能需要手动安装 32 位库。

> **提示**
> 提示：要测试你的游戏手柄是否工作，请在插入时运行 `sudo dmesg | grep -i gamepad`。你应该看到类似 `input: 2axis 4button gamepad as /devices/...` 的行或类似内容。你还可以检查它是否出现在 `jstest-gtk`（一个图形化摇杆测试器）中。如果你在那里看不到它，你可能存在问题。

最后，一旦我们安装了 `pygame`，我们需要修改 `tetris` 源代码以实际使用它。我们需要在 `tetris.py` 文件的顶部添加一些导入语句：

```python
import pygame
from pygame.locals import *
```

我们还需要修改 `__init__` 函数以初始化摇杆模块：

```python
def __init__(self, display):
    pygame.init()
    self.display = display
    pygame.joystick.init()
    self.joystick = pygame.joystick.Joystick(0)
```

此代码初始化第一个可用的摇杆。如果你有多个游戏手柄，你可以使用 `pygame.joystick.get_count()` 找出有多少个，并在 `Joystick` 构造器中使用适当的索引。

## 控制俄罗斯方块

现在我们已经在工作区下载并克隆了项目，我们可以进入项目，发现我们有一个相当新的文件。在我们的 main.html 文件中，我们已经在使用名为 Pexel 的 JavaScript 库。

如前所述，有两个 Python 文件，一个是 READY，一个是 SKELETON。它们之间的主要区别在于 READY 文件预先编码了两个函数。我们可以**初始化**游戏并通过键盘控制棋盘移动。此外，我们将学习如何控制玩家方块使其在游戏中移动。这是一个更高级的代码文件，因为它将包含支持额外按键控制以初始化游戏以及完整可玩版本的支持。如果你想更多地了解游戏的工作原理，最好从 SKELETON 文件开始，逐步过渡到 READY 文件。

### 项目概述

- 本项目使用了一个不可战胜的概念，即地图和几种不同类型的对象。让我们看看不同类型以及我们如何使用它们来控制游戏的移动。
- 为了控制主板，我们必须首先理解两个主要对象：
  - TetrisBoard() 类 - 这是持有棋盘状态并处理棋盘渲染的对象。它负责移动和旋转方块。
  - TetrisPiece() 类 - 这是代表单个俄罗斯方块（棋子）并处理其移动和旋转的对象。
- 为了控制棋子，我们有三种不同类型的对象：
  - Board - 这是持有棋盘状态并处理棋盘渲染的对象。它负责移动和旋转方块。
  - PlayerPiece - 这是代表单个俄罗斯方块（棋子）并处理其移动和旋转的对象。
  - GamePiece - 这是代表单个俄罗斯方块（棋子）并处理其移动和旋转的对象。

现在我们可以创建游戏了。
正如你可以在 `tetris.js` 文件中的代码中看到的那样，主要的 `tetris()` 函数接受四个参数。让我们看看这些参数及其工作方式。

第一个参数是 `canvas` 元素。这是我们将用于渲染游戏的 HTML canvas 元素。我们可以使用 `getElementById` 方法传入 `canvas` 元素。例如，如果我们有一个 ID 为 `tetris-canvas` 的 `canvas` 元素，我们可以使用 `document.getElementById('tetris-canvas')` 传入它。

作为第二个参数，我们可以定义游戏中想要的**列数**。这可以是 1 到 100 之间的任何值，但典型值是 10。第三个参数是我们想要的**行数**。这也可以是 1 到 100 之间的任何值，但典型值是 20。第四个参数是游戏的**缩放比例**。这是游戏中方块的大小。典型值是 20，但你可以将其设置得更大或更小，如你所愿。

```html
<html>
<body>
<canvas id="tetris-canvas"></canvas>
<script src="tetris.js"></script>
<script>
// 创建新游戏
const game = new Tetris(document.getElementById('tetris-canvas'), 10, 20, 20);
</script>
</body>
</html>
```

在 main.html 文件中，我们将看到我们创建的 canvas 元素。我们还将看到用于加载 `tetris.js` 文件的 script 标签。此外，我们将看到一个用于创建新游戏的 script 块。这是我们将传入游戏参数的地方。

我们可以使用 `Tetris` 构造器创建新游戏。此构造器接受四个参数。第一个参数是 `canvas` 元素。这是我们将用于渲染游戏的 HTML canvas 元素。我们可以使用 `getElementById` 方法传入 `canvas` 元素。例如，如果我们有一个 ID 为 `tetris-canvas` 的 `canvas` 元素，我们可以使用 `document.getElementById('tetris-canvas')` 传入它。

第二个参数是我们想要的游戏中**列数**。这可以是 1 到 100 之间的任何值，但典型值是 10。第三个参数是我们想要的游戏中**行数**。这也可以是 1 到 100 之间的任何值，但典型值是 20。第四个参数是游戏的**缩放比例**。这是游戏中方块的大小。典型值是 20，但你可以将其设置得更大或更小，如你所愿。

> **快速提示**
> 我们在此项目中使用的主要对象是 `TetrisBoard` 类。它负责创建游戏棋盘并将其渲染到屏幕上。它还处理用户输入并相应地更新游戏状态。

### 项目文件

在下一节中，我们将首先查看项目文件。本项目中有多个文件，所以让我们来看看它们。

#### main.html
主要的 HTML 文件是项目的主入口点。它包含 canvas 元素以及用于加载 `tetris.js` 文件的 script 标签。

#### tetris.js
包含游戏逻辑的主要 JavaScript 文件。它定义了 `Tetris` 类和 `TetrisBoard` 类。

#### style.css
包含游戏样式的 CSS 文件。

#### index.html
项目的替代入口点。它与 `main.html` 文件类似，但使用不同的布局。

#### README.md
包含项目信息的 Markdown 文件。

### 编码练习

在本节中，我们将编写主游戏循环。这是我们将更新游戏状态并将游戏渲染到屏幕的地方。

游戏循环是任何游戏中都非常重要的一部分。它负责更新游戏状态并将游戏渲染到屏幕上。通常使用 `requestAnimationFrame` 来运行。

在我们的项目中，游戏循环使用 `TetrisBoard` 类来运行。该类负责创建游戏棋盘并将其渲染到屏幕上。它还处理用户输入并相应地更新游戏状态。

在下一节中，我们将编写主游戏循环。这是我们将更新游戏状态并将游戏渲染到屏幕的地方。

