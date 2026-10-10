

![](img/5cfcf2f4448dccdd1c5c2a2851544557_90_0.png)

## 你能为下一代程序员带来灵感吗？

![](img/5cfcf2f4448dccdd1c5c2a2851544557_90_1.png)

**代码俱乐部**（Code Club）是一个全国性的志愿者主导的课后俱乐部网络，面向 9 至 11 岁的儿童。

我们一直在寻找具备编程技能的人，志愿每周花一小时在其当地的公立学校、图书馆或社区中心主持一个俱乐部。

你可以与同事组队；现场会有老师支持你，并且我们会提供所有需要的材料，帮助激发孩子们对数字创作的兴趣。

参与的方式有很多种！

因此，了解更多详情，请访问 **www.codeclub.org.uk**

## 编程学院

**MU**

版权：https://codewith.mu

第一部分！不要错过下一期，请在第 16 页订阅！

### 用 Python 编写你自己的文字冒险游戏

内特·德雷克（Nate Drake）将指导你利用 Python 的强大功能创建自己的交互式文字冒险游戏，从基础知识开始……

![](img/5cfcf2f4448dccdd1c5c2a2851544557_91_0.png)

- **我们的专家**
- 内特·德雷克希望将本系列献给他的父亲，父亲曾告诉他，从来没有人会付钱让他坐着玩电子游戏。

我们这些年纪足够大、记得 20 世纪 70 年代和 80 年代早期的人都知道，当时的游戏在图形上非常缺乏吸引力，更别提个人电脑当时价格高昂得令人望而却步。1975 年，麻省理工学院（MIT）学生威廉·克劳瑟（William Crowther）从繁忙的 ARPANET 开发工作中抽出时间，创作了一款可以和孩子一起玩的文字冒险游戏。尽管它并不是同类作品中的第一部（那个荣誉属于 1973 年的 *Hunt the Wumpus*），但《巨大的洞穴冒险》（Colossal Cave Adventure）在经历大量修改后，迅速在早期互联网上流传开来。其基本前提与任何文字冒险游戏一样，即你输入指令，例如罗盘的四个基本方位（北、南、东和西），以在不同区域间移动，并与物品、陷阱和怪物互动，试图以最高分通关。

年纪较小的读者可能难以相信，人们现在实际上仍在做这件事作为娱乐。事实上，交互式小说（IF）从未如此流行。年度 XYZZY 奖项甚至会为编写出最优秀文字冒险游戏的人提供奖品。在这为期四部分的系列中，我们计划带你走过使用 Python 3 编程语言创建自己的文字冒险游戏的基本步骤。好消息是，由于它是基于文本的，你不需要拥有Photoshop魔术般的学位。这也是一个极好的编程项目，既适合 Python 入门，也能帮助建立良好的编程习惯。如果你是 Linux 用户，还有更多好消息，因为你的发行版中几乎肯定已经内置了对 Python 3 的支持。你只需在终端输入 *python3* 即可开始。不过，这并不是编码和运行 Python 脚本的最简单方式，因此我们使用了 Mu Python 解释器。你可以在 Ubuntu 软件中心获取它，它提供了一种快速简便的方法来运行脚本。Mu 也可以用于树莓派。

![](img/5cfcf2f4448dccdd1c5c2a2851544557_91_1.png)

- **快速提示**
- 要下载本系列第一部分的代码示例，请打开终端并通过 *sudo apt-get install git* 安装 Git。接下来运行 *git clone https://github.com/aagreate/bpython-textadventure.git*。文件将下载到你主目录下的 'bpython adventure' 文件夹中。

从如何**不**做这件事开始……在本指南的第一部分，我们将重点关注设置和世界观构建。换句话说，你将学习如何创建地下洞穴、地牢或神秘世界中的房间，以及如何在它们之间导航。

很容易想象这比实际情况要简单得多。例如，尝试将以下脚本粘贴到你的 Python 解释器中并运行它：

```python
print("Which way will you go?")
action_input = input('Action: ')
if action_input == 'n':
    print('To the North, you see the skeleton of a dwarf holding an axe.')
elif action_input == 's':
    print('To the South, you see an antique wooden chest. It’s locked.')
elif action_input == 'e':
    print('You see entrance to the cave where you arrived earlier. The gate is locked.')
elif action_input == 'w':
    print("To the west you see an iron grille set into the wall.")
else:
    print("You cannot go that way.")
```

![](img/5cfcf2f4448dccdd1c5c2a2851544557_92_0.png)

如果你使用的是 **Mu**，请记住在运行脚本之前，你需要使用有效的文件名（例如 `test1.py`）保存代码。

为了分解这段代码，`print` 命令在这里被很好地利用。设置变量 `action_input`，然后匹配小写字母 `n, s, e` 或 `w`，使脚本输出对新房间的描述。

`elif` 命令是 Python 中 `ELSE IF` 的缩写，意思简单就是如果输入不匹配，就执行另一个查询。如果你没有输入有效的方向，这个脚本会告诉你，“你不能走那条路。”

虽然你可以这样编码冒险游戏，但这会在以后带来头痛。首先，你很可能想要拥有超过五个房间。这意味着你必须包含更多的 `print` 和 `elif` 命令行来描述每一个房间。大多数文字冒险游戏还允许你以某种方式与房间互动。如果你想拿起斧头或尝试打开大门怎么办？

既然你以后可能除了在不同房间之间漂移外还想要做其他事情，最好将移动定义为特定的函数。你可以在 Python 中使用 `def` 命令创建函数。语法相当简单，例如：

```python
def hello_world():
    print("Hello World")
```

然后你只需将 `hello_world()` 插入到你的脚本任何位置即可调用这个函数。

目前，这个脚本一旦你移动到一个房间就会正常退出。幸运的是，Python 允许你使用 `while` 命令来循环代码，你可以将其插入到你的新 `move` 函数中：

![](img/5cfcf2f4448dccdd1c5c2a2851544557_92_1.png)

```python
def move():
    print("Which way will you go?")
    while True:
        action_input = get_player_command()
        if action_input in ['n', 'N']:
            print("To the North, you see the skeleton of a dwarf holding an axe.")
        elif action_input in ['s', 'S']:
            print("To the South, you see an antique wooden chest. It's locked.")
        elif action_input in ['e', 'E']:
            print("To the East, you see entrance to the cave.")
        elif action_input in ['w', 'W']:
            print("To the west you see an iron grille set into the wall.")
        else:
            print("You cannot go that way.")

def get_player_command():
    return input('Action: ')

move()
```

这个版本的代码略有改进。现在有一个定义的移动函数。玩家可以

> **Mu** 是一个优秀的 Python 编辑器。你可以在程序内部编写和运行代码。请确保先保存。

### 绘制你的世界地图

在那个年代，新兴的游戏设计师会使用方格纸和大量的耐心来创建他们文字冒险游戏的地图。如果你对此感兴趣，可以试试，但还有更现代的选择。

其中一个是 **IFMapper**（https://tinyurl.com/ifmapper）。这个实用工具允许你绘制单个房间、绘制它们之间的路线，甚至可以列出房间描述和物品。

现在这样做会给你提供更清晰的想法，关于后来如何编码游戏。IFMapper 是用 Ruby 编写的，因此要开始，请在终端中运行 `sudo apt-get install ruby`。

运行 `sudo apt-get install build-essential libfox-1.6-dev ruby-dev libxrandr-dev` 安装依赖项，然后使用 `sudo gem install ifmapper` 安装 IFMapper 本身。你随时可以通过在终端中键入 IFMapper 来运行该程序。

程序启动后，转到 `File > Save` 并为你的地图取一个容易记住的名字。

点击网格中的任意框来创建新位置。双击它来更改名称，例如 Main Cavern。你可以使用其他选项卡来添加房间中的物品列表（如果有），以及描述。点击房间之间的虚线来代表它们之间的路线。你只需点击路线或房间然后按 Del 键即可删除它。

如果你需要灵感，请转到 `File > Open` 并查看 maps 目录中的一些示例。

![](img/5cfcf2f4448dccdd1c5c2a2851544557_92_2.png)

像 IFMapper 这样的工具可以让你轻松绘制游戏中区域和房间。

