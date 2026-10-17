
`self.bullet_fx = pygame.mixer.Sound("location/of/file")`

```python
def make_player(self):
    self.player = Player
```

剩余代码位于 `github/russ78/pivaders`

> “精灵集使得绘制到屏幕变得简单，但也保持了资源数量和性能水平”

![](img/f16311c48f0c39ab87b1836be5339b9e_96_0.png)

# 使用 Python 创建

## 制作视觉小说

### 你需要...

- Python (`www.python.org/doc`)
- Pygame (`www.pygame.org/docs`)
- IDLE Python
- 游戏资源
- 来自 FileSilo 的代码（可选）

通过使用 Python 创建交互式小说来弥接书籍与游戏之间的差距。大多数人都在现代游戏中寻找引人入胜的故事，而没有故事的人较少。讲述纯故事的一种极佳方法是通过视觉小说类型，你可以用 Python 简单地创建一个。交互式小说在日本是非常受欢迎的娱乐形式，通常通过玩家点击故事并做出决定来体验不同的情节和结局。

在 Python 中，这是一个相对简单的项目，但通过添加 `pygame` 模块，我们可以使其变得更容易，并且在未来更有扩展性。`pygame` 为图像和文本定位提供了更好的支持，创建窗口以及使用鼠标和键盘输入，简化了编码过程。

我们将使用标准 Python 2 进行编码，因此在编写、测试和编码时，请确保运行 `IDLE 2` 而不是 `IDLE 3`。

![](img/f16311c48f0c39ab87b1836be5339b9e_97_0.png)

## 使用 Python 创建

![](img/f16311c48f0c39ab87b1836be5339b9e_98_0.png)

### Pygame 依赖

01 为你的系统安装 Pygame 的最佳方法是编译它。要做到这一点，你需要首先安装正确的依赖。打开终端并安装包，如下：

```python
python setup.py build
```

02 安装，我们需要从源码下载代码。在终端中，你可以这样做：

```bash
git clone https://github.com/russ78/pivaders
```

03 安装，我们需要分两步完成。首先我们使用以下命令准备代码：

```python
python setup.py install
```

04 如果上述方法不起（或有点复杂），你可以检查网站是否有适用于其他操作系统和 Linux 发行版的二进制文件。访问 `http://pygame.org/download.html` 获取你特定系统的文件。

05 我们已经将代码上传到 File0，我们将引导你如何让它运行。下载视觉小说的文件并解压。我们目前关注的文件是 `visual novel py` 和 `script` 文件——这是所有重要代码所在。

06 目前 `script` 文件很小，字面上只是视觉小说游戏的脚本。它是逐行组成的，通过将其拆分为场景。这包括每个场景的位置、角色本身以及游戏如何流动的信息。这些矩阵包含了信息，并且是完全自定义的。

![](img/f16311c48f0c39ab87b1836be5339b9e_98_1.png)

### 获取视觉小说文件

游戏需要角色、背景和对话文件。

Pygame 是一个使用 SDL2 更改 SDL1 支持构建的库。它已发布并兼容 python 版本 3.8。

其中一个依赖未找到。Pygame 将报错。修复依赖项并继续配置...

![](img/f16311c48f0c39ab87b1836be5339b9e_98_2.png)

### 获取 Pygame 代码

接下来我们需要从源码下载代码。在终端中，你可以这样做：

```bash
git clone https://github.com/russ78/pivaders
```

### 构建 Pygame 模块

安装，我们需要分两步完成。首先我们使用以下命令准备代码：

```python
python setup.py install
```

### 理解脚本文件

“`pygame` 为图像和文本定位提供了更好的支持”

## 工作原理

```python
screen = pygame.display.set_mode(size)
menu_screen()
screen.fill(gray)
text = pygame.font.render('SCHOOL', True, (330, 100, 100))
start_button = pygame.draw.rect(screen, (black), (418, 310, 180, 55))
pygame.blit(text, (418, 330))
pygame.display.flip()
```

**07** 在我们的游戏中，代码会在执行过程中从脚本中提取元素。这在之后会很有有用，但也允许我们在稍后实现改变游戏可能走向的决策。

```python
for event in pygame.event.get():
    if event.type == pygame.MOUSEDOWN:
        if start_button.collidepoint(event.pos):
            start_game()
```

```python
import pygame, time, script
pygame.init()
```

### 查看鼠标

### 第一屏

### 启动游戏

**11** 当我们创建了图像并显示在菜单上时，我们悬停在上方以判断按钮何时被点击。首先，我们必须使用 `event.get()` 查看鼠标整体状态，然后通过 `get_pos()` 查找位置。之后，我们将等待点击（使用矩形的坐标进行点击），并在之后做出决策。

**13** 第一屏与众不同，而且为了获取界面上的每一个元素——这使得代码处理时间稍微缩短。我们开始使用字符串/整数方法来显示我们在故事中的位置，并从脚本中调用相关函数。

**08** 在这里对于视觉小说的状态，我们不需要很多模块。我们实现了新的游戏逻辑、作为 `script` 的我们的模块以及出于美学考虑的主题资源——我们将分部分编写代码，而不是通过简单的 `pygame.init()` 切换到下一个场景。

### 添加变量和资源

我们随后使用迭代过程来成功添加屏幕，营造出正在构建第一屏的错觉。我们通过推进进度值来完成它。

**09** 我们使用了混合信息来获取新内容。我们定义了显示尺寸（宽 1000 像素，高 563 像素）以及代码中的 RGB 颜色。我们还使用 Pygame 字体，并在场景中使用大字体，同时为游戏添加图像。

> "我们的下一个 if 语句和迭代会检查下一行的不同之处"

### 启动游戏

**10** Pygame 通过不断更新菜单新信息来工作。菜单函数向显示器上添加元素（我们将其命名为 `screen`），例如填充颜色、更新和形状以添加图像，或者在本例中添加文本。通过场景更改的缓冲区，使用 `flip` 函数进行更新。

```python
turn = 0 and click_state = 1:
    line_start = 0
    for(4):
        line_start = 0 and line[0] = 1:
            screen.blit(location(line[0]), [0, 0])
            time.delay(10)
        line_start = 1 and line[1] = 1:
            screen.blit(character(line[1]), [377, 113])
            line_start = 0
        screen.blit(gray, pygame.draw.rect(line(2), 1, white), (135, 430))
    turn = 1
    for(3):
        game_script = line[2]
        game_script = line[3]
        game_state = line[4]
        line_start = 1
    pygame.display.flip()
```

![](img/f16311c48f0c39ab87b1836be5339b9e_99.png)

# 制作视觉小说游戏

## 使用 Python 创建

```python
def game():
    global game_running
    while game_running == True:
        menu_screen()
```
