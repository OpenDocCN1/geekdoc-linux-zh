

# 使用 Python 制作视觉小说游戏

通过 Python 和 Pygame 创建互动小说或选择你自己的冒险，来弥合书籍与电子游戏之间的差距

![](img/3b256f430f51c98f1315671f6e4eec19_127_0.png)

切换场景以增加故事的深度，并允许游戏拥有决策和路线

## 资源

- **Python 2:** www.python.org/
- **Pygame:** pygame.org/download.shtml
- **IDLE Python IDE**
- **游戏素材**
- **来自 FileSilo 的代码（可选）**

大多数人会在现代电子游戏中寻找引人入胜的故事，而那些没有故事的游戏正变得越来越少。讲述纯粹故事的一种很好的方式是通过视觉小说类型，你可以用 Python 相对简单地制作一个。这些互动小说在日本是一种极受欢迎的娱乐形式，通常通过让玩家点击浏览故事并在过程中做出决策来体验不同的情节点和结局。

在 Python 中，这是一个相对简单的项目来创建，但通过添加 Pygame 模块我们可以让它变得更容易，并且对未来更具可扩展性。Pygame 提供了更好的图像和文本定位支持，创建显示窗口以及使用鼠标和键盘输入，从而简化了编码过程。

我们将使用标准 Python 2 编写代码，因此在编写、测试和编码时请确保在 IDLE 2 而不是 IDLE 3 中运行它。

### 01 获取 Pygame 依赖项

为你的系统安装 Pygame 的最佳方式是编译它。为此你需要先安装正确的依赖项。打开终端并安装以下软件包，在 Ubuntu 中看起来像这样：

```
$ sudo apt-get install mercurial python-dev python-numpy libav-tools libsdl-image1.2-dev libsdl-mixer1.2-dev libsdl-ttf2.0-dev libsmpeg-dev libsdl1.2-dev libportmidi-dev libswscale-dev libavformat-dev libavcodec-dev
```

![](img/3b256f430f51c98f1315671f6e4eec19_128_0.png)

### 02 获取 Pygame 代码

接下来我们需要直接从源代码下载 Pygame 的代码。仍在终端中，你可以通过输入以下命令来完成：

```
$ hg clone https://bitbucket.org/pygame/pygame
```

这将下载到 'pygame' 文件夹。进入该文件夹使用终端中的 CD pygame，以便我们可以继续构建它。

![](img/3b256f430f51c98f1315671f6e4eec19_128_1.png)

### 03 构建 Pygame 模块

要安装它，我们需要分两步进行。首先我们需要使用终端准备代码以便安装：

```
$ python setup.py build
```

完成后你就可以真正安装它：

```
$ sudo python setup.py install
```

这不会花费太长时间。

![](img/3b256f430f51c98f1315671f6e4eec19_128_2.png)

### 04 以其他方式安装

如果以上方法不起作用（或有点令人望而生畏）你可以查看网站上的二进制和可执行文件，这些文件适用于其他操作系统和 Linux 发行版。前往 http://pygame.org/download.shtml 获取适用于你的特定系统的文件，包括 Windows 和 OS X。剩下的教程适用于任何操作系统。

### 05 获取视觉小说文件

我们已将代码上传到 FileSilo，在这里我们将带你了解我们为使其工作所做的工作。下载视觉小说的文件并解压。我们现在关心的两个文件是 visualnovel.py 和 script.py python 文件——所有重要代码都在这里。

![](img/3b256f430f51c98f1315671f6e4eec19_128_3.png)

### 06 理解脚本文件

目前脚本文件很小，字面意义上只是保存游戏脚本。它由视觉小说在逐行之间移动的事件组成，通过将其拆分为场景。包括每行的位置、角色、实际行本身以及游戏流程的信息。这些是包含信息的矩阵，并且完全可定制。

# 使用 Python 创建

### 07 脚本如何关联

在我们的游戏中，代码在进行过程中从脚本文件提取元素。我们稍后会解释其工作原理，但这也允许我们在以后实现决策以改变游戏可能带你去的方向。

```
import pygame, time, script
pygame.init()
```

### 08 启动主游戏

对于当前状态的视觉小说，我们不需要太多模块。在这里我们导入了新的 pygame 模块、作为模块的脚本以及出于美观原因的时间模块——我们将让代码在某些部分暂停而不是立即切换场景到下一行。我们还使用简单的 pygame.init() 初始化 Pygame

### 09 添加变量和素材

我们添加运行小说所需的一系列信息。我们定义要使用的显示屏幕大小（宽 1000 像素，高 563 像素），以及代码使用的一些 RGB 颜色。我们还告诉 Pygame 使用什么字体以及某些部分的字体大小，并为游戏加载图像。

### 10 开始游戏

为游戏创建显示。Pygame 通过不断更新显示新信息来工作。为了展示其工作原理，菜单函数向显示（我们称之为 screen）添加元素，例如用颜色填充它、添加形状并使用 blit 添加图像或在这种情况下的文本。一旦你创建了屏幕更改的缓冲区，就使用 flip() 函数更新它。

### 11 查看鼠标

由于我们已将按钮创建为矩形，现在菜单上有一个图像，我们需要识别鼠标何时悬停在其上以知道何时点击按钮。首先

### 12 开始故事

当鼠标点击正确位置时调用我们的 start_game 函数，我们准备游戏，获取角色、位置和通过游戏脚本的进展。此函数的其余部分使用此信息从脚本中提取数据以使游戏正常流动。

### 13 第一个屏幕

第一个屏幕的处理方式不同，并且在继续之前起作用以将每个元素都显示在界面上——它使代码的处理时间稍微少一些，因为我们

```
def start_game():
    get_button = pygame.Rect(location, character)
    turn = 0
    game_state = 1
```

> “代码在进行过程中从脚本文件提取元素，允许我们在以后实现决策”

```
elif turn > 0 and clicked_state[0] == 1:
    line_start = 0
    for i in range (4):
        if line_start == 0 and line[0] != '0':
            print line[0]
            screen.blit(character[location[line[0]]], [0, 0])
            time.sleep(1)
        elif line_start == 1 and line[1] != '0':
            screen.blit(character[line[1]], [377, 113])
            time.sleep(1)
        elif line_start == 2:
            pygame.draw.rect(screen, (grey), pygame.Rect(130, 423, 740, 120))
        elif line_start == 3:
            screen.blit(game_font.render(line[2], 1, white), (135, 430))
            turn += 1
            if line[3] != '0':
                game_script = line[3]
                time.sleep(0.5)
            game_state = line[4]
            clicked = 0
        line_start += 1
        pygame.display.flip()
```

