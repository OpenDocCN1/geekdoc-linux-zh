
# 08 你的第一个脚本

如果可以自动生成桥梁或城堡的柱子，那该有多好呢？有了 `Minecraft Pi`，你可以做到！

接下来，我们将创建一个快速测试脚本，并确保我们能够从新位置成功使用 `Python Minecraft API`。使用你喜欢的文本编辑器，输入以下内容并将其保存为`boilerplate.py`：

```python
from mcpi.minecraft import Minecraft
from mcpi.minecraft import block

mc = Minecraft.create()
mc.postChat("Connected")
```

![](img/a17757b82ff78d9c8d36ac46319604f3_61_1.png)

如果 `Minecraft Pi` 没有在运行，请现在启动它。在进入游戏中，按下 `Tab` 键显示菜单，打开终端窗口并导航到你的 `Minecraft` 文件夹。

进入目录后，输入 `python boilerplate.py` 并按回车 - 你将看到 `Minecraft Pi` 的聊天框中出现“`Connected`”字样。我们建议所有的 `Minecraft Pi` 脚本都以这段模板代码开头。

# 09 没起作用！

如果你此时遇到错误，请重新检查你的模板代码以确保它是正确的 - 大多数情况下，是因为拼写错误。如果你遇到错误，可能是你在连接 `API` 文件夹到新位置时出现了问题。请从头重试步骤并再次尝试。

上面的 `Minecraft Pi` 没有羊，但喷泉没问题！

不过，最常用的 `API` 功能是那些围绕操作玩家位置和在固定位置设置方块的功能。

# 10 乐趣从这里开始...

现在我们已经成功测试了模板代码，可以开始享受 `Minecraft Pi` 和 `Python` 的乐趣了。有许多选项可以利用，例如设置方块、查找和设置玩家位置、更改设置以及...

# MINECRAFT 中的新技能

# 六个待击败等级

# 制作 MINECRAFT

![](img/a17757b82ff78d9c8d36ac46319604f3_62_0.png)

制作电脑

视频

吃蛇

乒乓

Minecraft

音乐

# 11 坐标

如果不熟悉坐标系，在 `Minecraft Pi` 中就无法进行任何操作。这是一个相当奇特的系统，它会切换 3D 空间中的 `Y` 和 `Z` 坐标 - 在 `Minecraft` 中，`Y` 是垂直移动。你始终可以通过查看左上角找到你当前的坐标。

# 12 原点

当你第一次抬头看时，你将从地图的中心开始，即 `(0, 0, 0)`。为什么要这样呢？因为这会让构建方块和方块集合变得简单得多。原点不需要你考虑周围方块的位置，它们简单就是 0 或负 0。

# 使用 setBlocks 函数同时设置多个方块

`KOS` 使用了一种视觉化的方式在 `Minecraft Pi` 中编程

`KOS` 还允许你尝试 `Python` 脚本，

吃蛇并使用 `Sonic Pi` 制作音乐

## 13 getPos

让我们从玩家在 `Minecraft` 世界中最是最简单的操作开始，这在 `Minecraft Pi` 中无疑是强大且实用的工具。你可以做任何事情，包括在玩家上方（下方）设置方块以及寻找位置（特定位置）。我们将轻松地找到玩家位置并存储在变量`my_pos`中，通过将其写入聊天窗口来证明这一点。

现在，当你激活正在运行的脚本时，你的角色每秒都会在你当前位置画一个石头块。通过使用`setBlocks`函数根据`x`和`y`坐标同时设置方块，我们就有了创建更大结构的方法。

## 14 setBlock

下一个常见动作是在某个地方设置一个方块。我们可以在`minecraft`文件夹中找到所有方块的完整列表。我们可以通过在世界中行走时丢下某种类型的方块来追加排序。我们第一个脚本中的`mc.post`行添加了`mc.setBlock(my_pos), block.STONE`

脚本的这个顶部部分现在是：

```python
mc.postChat("Connected")
while True:
  my_pos = mc.player.getPos()
  mc.setBlock(my_pos, block.STONE)
  time.sleep(1)
```

## 15 Teleport Steve

到为止，我们读取了玩家的位置，并利用它通过操作玩家位置来完成任务。通过编写这个脚本，我们将玩家移回原点，假设他们走远并迷失了方向。

```python
from mcpi.minecraft import Minecraft
from mcpi.minecraft import block
import time

mc = Minecraft.create()
mc.postChat("Minecraft API Connected")
while True:
  my_pos = mc.player.getPos()
  mc.setBlock(my_pos, block.STONE)
  time.sleep(1)
```

> 进入 `Minecraft`
>
> 如果你家里有一个玩家还没准备好尝试 `Python` 脚本，你还有另一条路供你选择。`KOS` 是一个为树莓派设计的新操作系统，通过将积木块组合成 `Minecraft` 世界（就像我们在这里演示的那样），向孩子们介绍视觉化编程。你可以在`www.kanmo.com/downloads`了解更多信息。

```python
from mcpi.minecraft import Minecraft
from mcpi.minecraft import block
import time
```
