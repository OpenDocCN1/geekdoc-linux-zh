
Signer Full Distinguished Name: `gerald.holmannoppa.com-gerald.holmannoppa.com`

Sign Time: `21:57`

Signature Hash Algorithm: `SHA1`

Signature Type: `adobe pkcs.7 [40532-41819]`

Total document signed

Signature Validation: `Signature is Valid.`

Certificate Validation: `Certificate has Expired`

**图 2**: pdfsig 使用搜索字符串检测密码。

LINUX-MAXIMAGE.COM | LINUXPROMAGAZINE.COM

第255期 2022年2月

## poppler-utils

`poppler-utils` 工具 [3] 是几个常用 PDF 管理工具的集合。在检查隐私或安全时，你可以使用这些工具中的任何一个来列出或提取各种对象进行检查：`dempdf` 用于嵌入页面图像，`pdftext` 读取内容并搜索文本。然而，对于大多数用途，`poppler-utils` 工具是 `pdfsig`（图3），它用于验证数字签名。

**图 3**: pdfsig 使用搜索字符串检测密码。

LINUX-MAXIMAGE.COM | LINUXPROMAGAZINE.COM

第255期 2022年2月

# 用数字存档清空你的书架

通过我们的数字存档合集，完善你的《Linux Magazine》和《ADMIN Network & Security》收藏。

你将获得一整年的 PDF 格式期数，可以随时随地任何设备访问。

https://bit.ly/archive-bundle

## 深度专栏

Charly 的专栏 - getnews.tech

# 系统管理员的日常工作：getnews.tech

## 新闻快讯

与新闻推送相比，Charly 更倾向于使用 `getnews.tech` 以一种更有针对性的方式关注全球正在发生的事件。作者：Charly Kühnt

如果我想关注世界的动态，我可以在网上查看我喜爱的报纸，或者使用新闻快讯。如果我很赶，不想离开命令行去操作这些呢？我使用 `getnews.tech` 来填补这一空白。你可以用它轻松搜索网页。如果我想保存数据，可以在 GitHub 上找到代码和安装说明 [1]。你还需要来自 News API [2] 的 API 密钥，你需要进行注册。News API 作为实际数据源，而 `getnews.tech` 作为 CLI 包装器，负责操作和排序，并处理人类可读的输出。

### 列表 1：参数化调用

```bash
$ curl en.getnews.tech/ne2?category=science
```

那些对我毫无意义的系统——例如希伯来语（图 1），或日语汉字。我只认识“男”和“女”这两个汉字，这是我最近在我的地下室公寓过了一个糟糕的夜晚后背诵的。

幸运的是，`getnews.tech` 提供了各种组织混乱的方法。例如，可以通过 URL 只获取英文（或法语）的新闻，或者几十种其他语言的新闻。我可以选择任何感兴趣的话题。如果我想查看任何类别的最新新闻，`getnews.tech` 接受最佳、娱乐、综合、健康、科学和技术分类。

如果不使用参数，我将获得来自世界各地的新闻而无需进一步筛选。这意味着我必须处理我不懂语言的新闻。

最后，我可以指定 `getnews.tech` 在我任何时候向我显示的消息数量。这是通过“number”参数实现的。要查看英语新闻流的最后两条消息（图 2），我可以使用以下列表：

```bash
curl getnews.tech
```

热点新闻 - 巴基斯坦空军允许飞往斯斯林加尔的新航班
巴基斯坦拒绝利用其空军对印度发动攻击，这将首当——内部长阿米特·沙哈在上周访问克什米尔期间拒绝了这一点。

Calaisut.com.il | 以色列军迫使58%的巴勒斯坦人口离开西岸

发布于 2021 年 11 月 3 日 上午 11:04
作者：Israel Berstein

הצבא הישראלי מאריח 58% מהאוכלוס הפלסטיני לעזוב הגדה המערב
（希伯来语原文）

根据半岛电视台报道，以色列军已迫使58%的巴勒斯坦人口离开西岸。查看 URL：https://getnews.tech/Israel-Army-WestBank

热点新闻 - 我们赌定你会喜欢！Apple iPhone 背面的这个隐藏功能

发布于 2021 年 11 月 3 日 上午 11:04
作者：David Miller

Apple iPhone 的最新更新 iOS 14 引入了“背部”功能，让你通过敲击手机背面执行任务。

# 图 1：getnews.tech 以所有语言和字体提供最新新闻

```bash
$ curl en.getnews.tech/ne2?category=science
```

ScienceAlert - 跨越数英里沙漠的玻璃碎片，阿塔卡马沙漠

它们大约在十年前出现在科学家视野中：一片散落在阿塔卡马沙漠的神秘玻璃区域，宽度达75公里（至少50英里）。

SctchDaily - 古老彗星、广阔岩石区的失落之城

发布于 2021 年 11 月 3 日 上午 11:04
作者：Sarah Jenkins

考古学家大学研究团队一年前在智利阿塔卡马沙漠发现沙土中包含面积达75公里（至少50英里）的玻璃块。

getnews.tech/FFRR-Atacama-Desert

由 News API (https://newsapi.org/) 驱动
免费贡献者：Twitter 和 GitHub

https://github.com/orgimanander/getnews-tech

# 图 2：新闻可以根据语言和数量30进行限制

信息

(getnews.tech)

https://github.com/orgimanander/getnews.tech

(News API: https://newsapi.org

# 作者

Charly Kühnt

德国南部地区数据中心内的单位系统。他的职责包括确保功能和 DMZ 安全与可用性。

![](img/dda1c68e5613db309d70a0ab080ae51a_29_0.png)

# 针对真实网络的真实解决方案

ADMIN 是你获取解决现实问题技术解决方案的来源。

通过关于以下实用文章提升你的管理技能：

- 安全性
- 云计算
- DevOps
- HPC（高性能计算）
- 存储及更多！

![](img/dda1c68e5613db309d70a0ab080ae51a_29_0.png)

立即订阅！
shop.linuxmedia.com

![](img/dda1c68e5613db309d70a0ab080ae51a_29_0.png)

![](img/dda1c68e5613db309d70a0ab080ae51a_29_0.png)

![](img/dda1c68e5613db309d70a0ab080ae51a_29_0.png)

![](img/dda1c68e5613db309d70a0ab080ae51a_29_0.png)

![](img/dda1c68e5613db309d70a0ab080ae51a_29_0.png)

![](img/dda1c68e5613db309d70a0ab080ae51a_29_0.png)

# 深度
编程开发

# 使用 Go 进行游戏开发

# 芯片球击

我们都知道 Go 的 E 框架可以用于创建桌面 GUI，但你也可以用它编写游戏。

# 编程快照 - 游戏开发

$$\vec{r}(t) = \begin{pmatrix} x(t) \\ y(t) \end{pmatrix} = \begin{pmatrix} v_{0t} \cos \beta \\ v_{0t} \sin \beta - \frac{1}{2}at^2 \end{pmatrix}$$

度，正如我们期望数学包中的正弦和余弦函数一样。因为 180 度对应 pi 的值，函数必须将度转换为弧度。坦率地说，这使得 45 度变成了 pi 的分之一，而 30 度变成了 pi 的六分之一。

**图 2：** 计算随时间变化的轨迹 X/Y 坐标的方程。

将这四个数据集绘制到与你相同的坐标系图表中，带有图例，并保存（第 24 行将图形保存为 8x8 的 PNG 文件）。

文件 3 显示了球以每秒 10 米的速度和 45 度的角度发射后的轨迹。如果踢球者稍微偏左一点，球将以相同的角度以 15 m/s 的速度起飞，在回到地球之前会飞得更远。发射角度由列表 2 中的第 16 到 19 行定义，使用的是弧度而不是……

## 游戏化

本章的剩余内容将弹道轨迹物理学引入桌面游戏引擎。第 4 章，游戏正进行得如如荼，球的顶部速度为 55 m/s，底部角度为 45 度。目标动态由中心和目标之间的彩色矩形表示，目标位于更右侧。

### 列表 1：physics go

```go
01 package main
02 import (
03 "math"
04)
05 func shoot(v float64, a float64, t float64) (x float64, y float64) {
07 const g float64 = 9.8
08 x = v * t * math.Cos(a)
09 y = v * t * math.Sin(a) - g/2*t*t
10 if y < 0 {
11 y = 0
12 }
13 return x, y
```

通过这些设置的参数，用户点击左上角的射击按钮。通过鼠标，球飞过守门员，用最后的能量进入球门。这行不通。例如，图 5 显示了一次尝试，球飞过了守门员但在通球门的途中停止了，因为它有足够的动能，并在落地后因摩擦力而停止。最后，在图 6 中，球落在了那里，守门员接住了。

![](img/dda1c68e5613db309d70a0ab080ae51a_32_0.png)

这类简单的视频游戏最早出现在 20 世纪 80 年代的街机中。推出时内置了事实上的传感器。

**图 3：** 由列表 2 代码生成的球的轨迹。

### 列表 2：plot go

```go
01 package main
02 import (
03 "gonum.org/v1/plot"
04 "gonum.org/v1/plot/plotter"
05 "gonum.org/v1/plot/plotutil"
06 "gonum.org/v1/plot/vg"
07 "math"
08)
09
10 func main() {
11 p := plot.New()
12 p.Title = "Trajectory Motion"
13 p.X.Label = "X"
14 p.Y.Label = "Y"
15 err := plotutil.AddLinePoints(p,
16 	"/v=45", shoot(45, 45, math.Pi/4),
17 	"/v=55", shoot(55, 45, math.Pi/4),
18 	"/v=60", shoot(60, 45, math.Pi/4),
19 	"/v=65", shoot(65, 45, math.Pi/4))
21 if err != nil {
22 panic(err)
23 }
24
25 err := p.Save("shoot.png", 8.inch, "curve.png")
26 if err != nil {
27 panic(err)
28 }
29
30 func shoot(v float64, a float64) plotter.XY {
31 n := 20
32 pts := make(plotter.XY, n)
33 t := 0.0
34 for i := 0; i < n; i++ {
35 pts[i].X, pts[i].Y = shoot(v, a, t)
36 t += 0.25
37 }
38 return pts
```

## 深度解析编程快照 – 游戏开发

每秒流畅显示几次。视频游戏通常运行在提供显示功能的现有引擎上。它们通过为每一帧触发回调函数来获取游戏事件的访问，然后游戏推动角色或检查它们是否与任何障碍物碰撞。人类跟踪复杂的情况，以便我们立即在游戏场中移动球以射门。另一方面，程序会重复每次游戏，无论球是否真的击中了其中一个物体。程序可以快速做到这一点，并表现出类似于人类的模式识别能力——但当然，这个过程是基于幻觉。用户觉得玩几分钟内置游戏很有趣，使用快速射击按钮让他们难以置信，并且认为如果这些人家里没有 PlayStation 主机就会产生疑问！街机游戏背后的策略以及创建驱动它们的软件的信息在 Franz Lanzinger 编写的《经典设计》中有详细介绍，他是该领域的先驱。根据 Lanzinger 的说法，他在圣克鲁斯发现了一种当时流行的带有“水晶球”的街机游戏。通过他所知的两个按钮的秘密组合，他发现游乐园的游客在机器行业中投入了超过 10 万枚硬币。推测到此时生产的 5,000 台机器，产生了 1 亿美元的收入。

## 伟大的网球

视频游戏由纯代码组成；图形在最近的专栏中用图片覆盖。图 4 到 6 显示了游戏动作。用户使用两个滑块将球的发射速度设置在 0 到 30 之间，并将角度设置在 0 到 90 之间。如果然后点击顶部帧，球开始在其抛物线路径上飞行。

## 从帧到帧

所有这些视频游戏的共同点是计算机在或多程度上进行计算和播放。球一落地，它就会滚动一会儿——运气好的话，进入游戏，让顶部的计数器加 1。然而，如果球落在守门员面前，它会被接住，守门员可能会对这次尝试大笑/欢快地笑。射击者射击。此值重复 100 次，以确保动画流畅无卡顿。第 26 行和第 27 行设置每次击中球的位置；然而在飞行阶段捕捉时移动球。

从第 97 行开始的函数在启动时使用球门和守门员的位置，并为新轮创建一个不同参数的状态以确保随机性，使守门员站在球后面。当球结束轨迹并回到地球时，物理函数 `physics()` 返回零，或者作为一个简化的近似——绕球门滚动的 X 和 Y 坐标。如果玩家得分，分数增加，游戏通过重新生成守门员和目标创建一个新局面。如果攻击者失败且球没有进门，玩家可以尝试模拟。

**图 5：力量不够：球在球途中停止了。**

## 动作！

图 6：太短：守门员接住了球。现在，第 42 行的 `animate()` 函数定义了用户点击“射击”时球的动作。使用球的初始值 (vel) 和角度 (la)，它将轨迹画入游戏，并根据当前位置处理球与球门或守门员的碰撞。

## 程序化随机

图形控件定义在第 48 行和 50 行，但球定义在第 41 行（使用 `vel()` 和 `angle()`）以确保每次的随机性。直到在后的第 51 行（函数根据需要导致刷新它们的文本序列）。

列表 3 设置了游戏。为了防止程序重启后总是出现相同的位置，第 34 行使用了 Go 内部数字生成器的 `rand()`，当使用当前时间的纳秒作为种子时，

球在第 57 行被显示为圆形，并创建并填充为红色。目标位于位置 8，即球场的左边缘。

# 深度解析

## 编程摘要 - 游戏开发

### 列表 3: chipshot.go

```go
package main

import (
	"fmt"
	"golang.org/x/image/colornames"
	"image/color"
	"math/rand"
	"os"
	"time"
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/data/binding"
	"fyne.io/fyne/v2/widget"
)

type UI struct {
	ball, goal, goalText, goalie
	goalieText canvas.CanvasObject
}

var (
	width      = float32(1200)
	height     = float32(800)
	goalWidth  = float32(30)
	goalHeight = float32(40)
	mindist    = 30
	textHover  = float32(50)
)

func main() {
	app := app.New()
	ui := &UI{}
	rand.Seed(time.Now().UnixNano())
	tw := app.NewWindow("Chipshot")
	tw.Resize(fyne.NewSize(width, height))
	tw.SetContent(ui.goalList)
	goalist, goalDist := itemsXPos()
	goalie.Canvas = canvas.NewCanvas(color.LightGray)
	goalie.Move.Move(fyne.NewPos(goalDist, height-goalHeight))
	goalie.Resize(fyne.NewSize(goalWidth, goalHeight))
	goalie.Canvas = canvas.NewCanvas(color.LightGreen)
	goalie.Move.Move(fyne.NewPos(goalDist, height))
	goalie.Resize(fyne.NewSize(goalWidth, goalHeight))
	ball.Move.Move(fyne.NewPos(0, height-30))
	ball.Resize(fyne.NewSize(30, 30))
	ui.goalText = canvas.NewText("Goal!", color.Red)
	placeTextHover(ui.goalText, ui.goalie)
```
