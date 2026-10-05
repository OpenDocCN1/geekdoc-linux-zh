
retrace[1] 将存储你之前的 z 轴位置。这里是代码，其中包含一行用于显示金块在其新位置的代码：

```
else: # 当没有未访问的邻居时执行此操作
retrace = cellsVisitedList.pop()
xposition = retrace[0]
zposition = retrace[1]
showMaker(xposition, zposition)
```

注意，`else` 语句应该与其匹配的 `if` 语句对齐——在这种情况下，就是测试你是否找到了任何可以移动的方向的那个。

算法中的第 6 步已经实现；`while` 循环将不断重复下方的缩进代码，直到每个单元格都被访问。

## 添加天花板

从个人而言，我们认为让天花板开放更有趣，你可以自由地向上飞行欣赏你的迷宫，然后掉到任何一点。不过，如果你想围绕你的迷宫制作一个游戏并防止人们作弊，可以使用以下代码添加天花板。只需在程序开始时将变量 `CEILING` 改为 `True` 即可。我们用玻璃砖制作了天花板，所以它在黑暗中也不会完全消失：

```
if CEILING == True:
mc.setBlocks(MAZE_X, GROUND+HEIGHT+1, MAZE_Z, 
MAZE_X+(SIZE*2), GROUND+HEIGHT+1, MAZE_Z+(SIZE*2), 20)
```

## 玩家定位

最后，让我们玩家放置在开始生成迷宫的随机位置。你可以将玩家放在任何地方，但这里似乎是一个不错的选择，而且利用了你已经生成的随机数：

```
mc.player.setTilePos(realx(player), GROUND+1, 
real(player)
```

现在你准备好玩了！图 13-4 显示了迷宫的内部视图。

## 最终代码

列表 13-1 显示了最终且完整的代码：

![](img/df9a01bf057d58c2401b5edabd6e8829_290_0.png)

图 13-4：
在迷宫中寻找路线。

## 列表 13-1：Minecraft 迷宫制作器

```
import sys, random
from mcpi import minecraft
mc = minecraft.Minecraft.create()

mc.postToChat("Welcome to Minecraft Maze!")

def realx(x):
    return MAZE_X + (x*2) - 1

def realz(z):
    return MAZE_Z + (z*2) - 1

def showMaker(x, z):
    mc.setBlock(realx(x), GROUND+1, realz(z), 41) == 41-gold

def hideMaker(x, z):
    mc.setBlock(realx(x), GROUND+1, realz(z), 0)
```

（续）

## 列表 13-1：（续）

```
def demolish(realx, realz):
    mc.setBlocks(realx, GROUND+1, realz, realx,
HEIGHT+GROUND, realz, 0)
```

```
def testWalls(cellx, cellz):
    if mc.getBlock(realx(cellx)+1, GROUND+1,
realz(cellz))==MAZE_MATERIAL and mc.getBlock(
realx(cellx)-1, GROUND+1, realz(cellz))==MAZE_MATERIAL
and mc.getBlock(realx(cellx), GROUND+1, realz(cellz)+1)==
MAZE_MATERIAL and mc.getBlock(realx(cellx), GROUND+1,
realz(cellz)-1)==MAZE_MATERIAL:
        return True
else:
    return False
```

```
mc.setting("world_immutable", True)
```

```
# 在这里配置你的迷宫
SIZE = 10
HEIGHT_X = 2
MAZE_Y = 0
GROUND = 0
MAZE_Z = 0
MAZE_MATERIAL = 1 # 1=石头
GROUND_MATERIAL = 2 # 2=草
CEILING = False
```

```
# 清除区域
mc.setBlocks(MAZE_X-10, GROUND, MAZE_Z-10, MAZE_X+
(SIZE*2)+10, GROUND+150, MAZE_Z+(SIZE*2)+10, 0) = air
```

```
# 铺地
mc.setBlocks(MAZE_X-10, GROUND, MAZE_Z-10, MAZE_X+
(SIZE*2)+10, GROUND, MAZE_Z+(SIZE*2)+10, GROUND_MATERIAL)
```

```
# 起点标记
mc.setBlock(MAZE_X, GROUND+HEIGHT+1, MAZE_Z, MAZE_MATERIAL)
```

## 将玩家移动到迷宫中心正上方
mc.player.setTilePos(MAZE_X+SIZE, GROUND+25, MAZE_Z+SIZE)

mc.postToChat("Now building your maze...")

```
# 墙体网格
for line in range(0, (SIZE+1)*2, 2):
    mc.setBlocks(MAZE_X+line, GROUND+1, MAZE_Z, 
MAZE_X+line, GROUND_HEIGHT, MAZE_Z+(SIZE*2),
    mc.setBlocks(MAZE_X, GROUND+1, MAZE_Z, 
MAZE_X+(SIZE*2), GROUND+1, MAZE_Z+(SIZE*2), 20) # 注意：此处原文代码似乎有截断或重复，已按逻辑保留结构
```
*(注：原文最后一段 `mc.setBlocks` 处似乎存在逻辑上的重复或截断，翻译时严格遵循了原文格式。)*
