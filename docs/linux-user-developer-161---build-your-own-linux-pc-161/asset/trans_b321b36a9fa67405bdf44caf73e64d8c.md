

## FUZE 基础

### 绘制激光（第 29-40 行）

虽然 `DEF drawers` 存在，但实际上很多重复工作并没有看起来有那么困难。第一个已经搞定了，无论我们是使用标准激光还是粒子激光，每个单独的[逻辑都是相同的]。我们使用相同的颜色来执行[这些这些操作]。请注意，在处理粒子时，有两个（左侧和右侧）需要处理。

随后，我们检查是否有敌人与这道激光接触。这是通过产生“BOOM！”的效果来实现的。激光会扩张和收缩以匹配每一个敌人——如果被击中，敌人数量减一，并添加声音，在激光层上播放音效。

### 绘制敌人（第 41-50 行）

现在例如 `DEF drawEnemies`。任何敌人都会使用 `FOR` 循环生成，该循环足够快到可以移动，然后进行绘制。接着我们检查它是否与激光接触，如果是，玩家的激光数量将减一，如果我们把它们移出屏幕外，我们的运气也不会太差。

### 绘制玩家（第 51-60 行）

目前，变量用于存储 `CUR ID`，并且可以在每次绘制计算期间通过 `x = x + player` 进行移动。单位是距离屏幕中心的距离。然后使用 `Plot` 绘制玩家。

```
DEF drawPlayer
COL = yellow
x = cos((playerAngle + 90) * playerRadius)
s = sin((playerAngle + 90) * playerRadius)
height = 0
Plotstart
Plot( (x + s * 5, y + s * 5), playerX, 5)
Plot( (x - s * 5, y + s * 5), playerX, 5)
Plot( (x - s * 5, y - s * 5), playerX, 5)
Plot( (x - s * 2, y - s * 2), playerX, 2)
Plot( (x + s * 2, y - s * 2), playerX, 2)
Plot( (x - s * 5, y - s * 5), playerX, 5)
Plot( (x + s * 5, y - s * 5), playerX, 5)
Plot( (x + s * 5, y + s * 5), playerX, 5)
Plot( (x - s * 7, y + s * 7), playerX, 7)
Plot( (x + s * 7, y + s * 7), playerX, 7)
Plotend
ENDPROC
```

### 20 检查进度（第 52-58 行）

现在我们检查 `checkProgress` 是如何实现的。每当我们杀死一个敌人时，`progress` 变量就会增加，如果我们杀死了 `advance` 变量，就会跳转到下一关。屏幕上会显示分数。

```
DEF checkProgress
if progress = advance
playSample(sfx, 7, 0)
score = score + ((10 * score))
rou = 1
level = level + 1
advance = advance + 1
enemy = enemy / targetFPS
ENDPROC
```

### 21 更新敌人（第 59-71 行）

敌人需要更新，因此我们有一个非常简单的 `updateEnemy`。每个敌人碎片都会更新其位置并赋予随机颜色。

### 22 更新分数（第 72-76 行）

`DEF updateScore` 负责绘制当前的分数和等级。会有帮助吗，又一个免费的！这次我们更新了分数时间和奖励。我们还展示了如果分数是数字递增而不仅仅是像简单示例那样增加计数器的情况。

### 23 开始游戏（第 77-81 行）

每当游戏开始时都会调用该循环。所有变量都已初始化。

随后，在 `WHILE` 循环开始后，FUZE 已经准备好。

### 24 我们进入下一关

这样我们就可以跳转到下一关。我们不期望你一直使用 BASIC，但如果你学会了它，就可以迁移到 C++。如果你会编写 BASIC，你会发现它非常容易，并能够适应任何其他语言。

### 19 显示剩余线条（第 82-90 行）

下一个过程，`DEF plotLayers` 帮助我们显示屏幕右上角的剩余层数。这个位置位于 `GHEIGHT` 下，并使用 `Plot` 命令从左到右绘制线条。

linuxuser.co.uk

## 竞赛

### 赢得了！FUZE 特别版

![a54b3b473771472dd2321ddda1014be1_77.png]

具有明显的复古根源，屡获殊名的 FUZE 是一台可编程计算机和电子工作站。源于对编程和电子的热，坚固的外壳带有键盘、特殊设计的 GPIO 引脚以及用于简单电子实验的面包板。FUZE 在键盘下方封装了 Raspberry Pi，并预装了 FUZE BASIC。

支持图像和缩放、角度和 Alpha 控制以及旋转，FUZE BASIC 已完全配置，可在所有 Raspberry Pi 型号上运行。FUZE 系统不仅仅是一个解释器

FUZE BASIC 是 BASIC 编程语言的高级版本，被广泛认为是最容易学习和教学的初学者语言。具有重新设计的界面和高级图形

FUZE 特别版向 BBC Micro 和 Comic 等家用电脑致敬，并附带了一个机械臂套件以集成到你的项目中。FUZE 特别版还通过 FUZE Lar 提供独家教程和在线资源，为你提供所需的一切。更多信息，请访问 **fuze.uk**。

![a54b3b473771472dd2321ddda1014be1_77_1.png]

参赛截止日期：2016年2月10日

### 参赛

参赛截止日期：2016年2月10日

