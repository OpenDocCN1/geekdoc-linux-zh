

![](img/fb76008333fb7aef815b136f9f1afe5f_70_0.png)

![](img/fb76008333fb7aef815b136f9f1afe5f_70_1.png)

## 建模 Mac 电脑

为了获得准确的 Macintosh Classic 尺寸，Hermann 使用他孩子的乐高积木制作了一个原型，并在乐高的 Digital Designer 软件中建立了一个 3D 模型（[http://ldd.lego.com]）。

## 组件列表

- 乐高 Digital Designer 软件
- 乐高积木
- Embedded Artists 的电子纸显示屏
- Raspberry Pi Zero（但现在建议使用 Pi Zero W）
- 电源
- 微型复古 Macintosh 贴纸
- Dremel 旋转工具
- 线缆（公对母）

## 添加转接头

整个项目由 Raspberry Pi Zero 供电，该设备添加了一个低剖面的 Wi-Fi 转接头，以便远程更新系统。

## Docker 基础

由于这台迷你 Macintosh Classic 是送给朋友的礼物，Jannis 使用来自 resin.io 的 Docker 基础镜像来设置 Raspberry Pi，以便在需要时能够远程更新信息。该显示屏目前显示的信息包括他朋友女儿的年龄（以天计）、降雨概率和当前温度。

## 电子纸展示

Jannis 使用了来自 Embedded Artists 的 2.7 英寸电子纸显示屏，这带来了一些挑战，其中之一是显示板比显示屏本身大得多。

![](img/fb76008333fb7aef815b136f9f1afe5f_70_2.png)

![](img/fb76008333fb7aef815b136f9f1afe5f_70_3.png)

**最左侧** 当 Jannis 开始他的项目时，Raspberry Pi Zero W 尚未发布，这就是为什么照片中的 Pi Zero 板上连接了一个 USB Wi-Fi 转接头的原因。如果你现在尝试这个项目，他建议只使用 Pi Zero W。

**左侧** 这个项目并不是一帆风顺的：Jannis 意识到他制作的模型恰好宽了一块积木时，不得不拿出 Dremel 旋转工具进行修整。

## Minecraft

### 使用 Python 代码在 Minecraft 中创建像素艺术

继我们关于 Minecraft 编程的系列报道后，本期我们将向你展示如何创建自动化的像素艺术

![](img/fb76008333fb7aef815b136f9f1afe5f_71_0.png)

#### Calvin Robinson

Calvin 是一所公立全纳学校的计算系主任和网络管理员。Calvin 还与伦敦各地的学校进行咨询合作，帮助提供高质量的计算教学和课程。

![](img/fb76008333fb7aef815b136f9f1afe5f_71_1.png)

```python
woolBlockGreenType = 5
#Black wool is blockID 15
woolBlockBlackType = 15

pixelArt = []

pos = mc.player.getPosition()
x = pos.x
y = pos.y + 7
#8 blocks above ground
z = pos.z
```

在 Minecraft 中创建像素艺术可以是一种很放松的活动，但逐个放置方块也非常耗时。然而，通过使用 Python 和几个简单的“for”循环，我们可以编写脚本来自动将预制好的像素艺术直接构建到我们的 Minecraft 世界中。

如果你正在树莓派上运行 Minecraft Pi 版，则无需安装额外的软件。我们还准备了一些工具，以确保此脚本可以在使用零售版 Minecraft 的 Linux 上运行。因此，作为先决条件，我们假设你已经从我们前几期的文章中安装了 McPiFoMo。McPiFoMo 包含了来自 MCPiPy.com 的 'jlep' 和 'bluepillRabbit' 开发的 MCPiPy，以及由 Alexander Pruss 开发的 Raspberry Jam。

在本教程中，我们将使用 Python 创建一个数组，用于按行和列构建方块，从而生成一些像素艺术。你需要手边准备好方块 ID 列表，以便选择与你期望颜色相匹配的一系列方块。在这里我们将使用羊毛作为选择，但你也可以使用任何符合你目的的方块。

所有 Python 脚本都应保存在目录 `~/home/minecraft/mcppy/` 中，无论你是运行 Minecraft Pi 版还是 Linux 零售版 Minecraft。

## 01 设置代码

这是主要的代码列表...

```python
from mcpy import minecraft
mc = minecraft.Minecraft.create()

#Wool is blockID 35
#Green wool is blockID 35:5 (type 5)
woolBlock = 35
```

务必使用我们 McPiFoMo 包中附带的 Forge 1.8 配置文件来运行 Minecraft。

```python
for row in range(len(pixelArt)):
    for pixel in range(len(pixelArt[row])):
        if pixelArt[row][pixel] == 0:
            mc.setBlock(x, y - row, z + pixel, woolBlock, woolBlockBlackType)
        elif pixelArt[row][pixel] == 1:
            mc.setBlock(x, y - row, z + pixel, woolBlock, woolBlockGreenType)
```

## 02 解析代码 – 方块类型

上述代码中有几个有趣的点。首先，你会发现我们每个方块使用了两个变量。为了将方块 ID 设置为 35:5（即绿色羊毛），我们使用 `woolBlock 35` 和 `woolBlockGreenType 5`。我们将对所有添加到像素艺术中的方块都这样做。如果没有方块“类型”，请简单使用 `0`。

在我们的 for 循环中，我们调用 `woolBlock.woolBlockGreenType.`。如果你经常使用没有类型的方块（例如钻石：57），可以完全省略类型变量。

## 03 解析代码 – 定位

你还会注意到我们的方块在 y 轴上的位置是 +7。这是因为我们将创建像素艺术

![](img/fb76008333fb7aef815b136f9f1afe5f_71_2.png)

## 资源

- **Minecraft**
  www.mojang.com/games/
- **Wireshark**
  www.wireshark.org
- **Python**
  www.python.org
- **McPiFoMo**
  http://rpiethat.co.uk/McPiFoMo.rar
- **Block IDs**
  http://minecraft-ids.grahamedgecombe.com

高八个方块，我们希望确保它从地面水平向上出现。

```python
pos = mc.player.getTilePos()
x = pos.x
y = pos.y + 7
z = pos.z
```

我们的方块按行构建：

```python
for row in range(len(pixelArt)):
    for pixel in range(len(pixelArt[row])):
        if pixelArt[row][pixel] == 0:
            mc.setBlock(x, y - row, z +
                        pixel, woolBlock, woolBlockBlackType)
        elif pixelArt[row][pixel] == 1:
            mc.setBlock(x, y - row, z +
                        pixel, woolBlock, woolBlockGreenType)
```

```python
woolBlockOrangeType = 1
#Blue wool is type 11
woolBlockBlueType = 11
#Brown wool is type 12
woolBlockBrownType = 12
#White wool is type 0
woolBlockWhiteType = 0
#Pink wool is type 6, but double jungle wood slabs look good (125:3)
woolBlockPink = 125
woolBlockPinkType = 3
```

## 06 创建史蒂夫头像 – 扩展你的 for 循环

我们还需要将这些新变量添加到下面的 **for** 循环中，以便将它们添加到每一行。我们可以这样做无数次。

```python
for row in range(len(pixelArt)):
    for pixel in range(len(pixelArt[row])):
        if pixelArt[row][pixel] == 0:
            mc.setBlock(x, y - row, z +
                        pixel, woolBlock, woolBlockOrangeType)
        elif pixelArt[row][pixel] == 1:
            mc.setBlock(x, y - row, z +
                        pixel, woolBlock, woolBlockBlueType)
        elif pixelArt[row][pixel] == 2:
            mc.setBlock(x, y - row, z +
                        pixel, woolBlock, woolBlockBrownType)
        elif pixelArt[row][pixel] == 3:
            mc.setBlock(x, y - row, z +
                        pixel, woolBlock, woolBlockWhiteType)
        elif pixelArt[row][pixel] == 4:
            mc.setBlock(x, y - row, z +
                        pixel, woolBlock, woolBlockPinkType)
```

### 04 绘制 2D 爬行者

现在，为了创建你的第一件像素艺术作品，你需要在 **pixelArt** 列表中创建一个由 1 和 0 组成的列表：

```python
pixelArt = [
    [1, 1, 1, 1, 1, 1, 1, 1],
    [1, 0, 0, 1, 1, 0, 0, 1],
    [1, 0, 0, 1, 1, 0, 0, 1],
    [1, 1, 1, 0, 0, 1, 1, 1],
    [1, 1, 0, 0, 0, 0, 1, 1],
    [1, 1, 0, 0, 0, 0, 1, 1],
    [1, 1, 0, 1, 1, 0, 1, 1],
    [1, 1, 1, 1, 1, 1, 1, 1]
]
```

如果你眯起眼睛，你可以从 1 和 0 中辨认出一个爬行者的头。

### 05 创建史蒂夫头像 – 添加更多方块类型变量

显然，爬行者只有黑色和绿色，但如果你想创建更高级的东西，你需要通过添加更多带有方块 ID 和类型的变量来添加更多颜色的方块。以下是创建史蒂夫头像所需的颜色：

```python
#wool is blockID 35
#Orange wool is type 1
woolBlock = 35
```

## 07 运行你的代码

将你的 **pixelart.py** 文件保存在 ~/home/minecraft。使用 Forge 1.8 配置文件打开 Minecraft，创建/加载一个世界，并输入 **/python pixelart** 来生成你的创作。你可以这样做任意次来构建你预制像素艺术的新副本。■

> **寻找新的像素艺术**
>
> 如果你在为像素艺术创作寻找灵感时感到卡壳，或者你需要一点帮助，试着谷歌搜索像素艺术模板。有很多免费的模板可用，带有网格线和可计数的盒子。你可以通过计算行/列并调整你的 Python 列表来匹配这些模板。我们的爬行者和史蒂夫头像都是 8x8，但你可以通过增加四行代码并给每行追加四个数字，轻松地将其改编为 12x12。
>
> 我们很乐意看到你的 2D/3D Minecraft 像素艺术创作。给我们发推特，附上你最棒的游戏截图 @linuxusermag，并告诉我们你正在哪个发行版上运行 Minecraft。

