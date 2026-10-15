
# UnCiv

https://github.com/yairm210/UnCiv

## 太空生存

### Space 14

Space 14 是一部设定在空间站上的独特俯视角多人玩家游戏。它是邪典经典《Space 13》的重制版，但这个版本完全开源并处于活跃开发中。开发者认为游戏处于 Alpha 阶段，在理解正在发生什么以及整体目标可能是什么方面感觉可能会有些欠缺。开发者还要求人们测试游戏并为社区做出贡献；因此你的努力是值得的。如果你加入了，你需要连接以与其他玩家共享，这取决于该特定游戏实例使用了什么资产。然后你可以选择一个角色来玩。有许多角色可以选择，包括调酒师、厨师、安全主管和船长。每个角色都有自己的装备和任务列表。你会发现自己坐在一艘由驾驶员操控的飞船上，承载着大量人员，关键是，还有许多其他人。刚开始，游戏感觉有点像《Among Us》（太空狼人杀）。你在空间站上，没有位置地图或你角色能力的说明。你可以在区域之间移动，并通过门与其他人互动。画面中存在类随机元素，迷雾遮挡了你的角色从当前位置无法看到的内容，但画面非常有效地营造了沉浸式的空间站氛围。

游戏边缘是用于操作的“热键栏”、站点的控制按钮以及你所持有的物品。它让人想起一个名为 Pandora 的老旧 Atari 和 ST 游戏；出现在空间站并需要解决任务。在 Space 14 中，核心思想是各种灾难会击败你，你的队友必须共同努力来维持一切运行。

# 项目网站

https://spacestation14.io

# LINUX VOICE 教程 – PRETTYMAPS

## 创建你自己的自定义地图

### 地图艺术

Prettymaps 结合了多个 Python 库，使其可以直接从 OpenStreetMap 数据库轻松绘制地图。

作者：MARCO FIORETTI

地图极其重要。没有地图，我们不仅不知道该去何处，在很多情况下，甚至不知道该做什么。准确的地图对于规划从快速的周末旅行到大规模的城市项目的任何计划都至关重要。地图本身也是美观且实用的。它们由所有者定制，可以变成小型的艺术品。在教程中，我将介绍一种使用 OpenStreetMap [1] 和免费开源软件生成此类艺术品的相对简单的方法。结果包括多种风格和形状的地图，适合你的墙贴海报、手册和其他文档中的插图、马克杯、枕头和其他家居用品的装饰，或者……仅仅在路上使用，就像老纸质地图一样。

根据我的经验，prettymaps 是一个能让许多爱好者感到快乐的小工具，尽管它有一些缺点。微小的缺点是 prettymaps 运行很慢。在配备 16GB 内存的 Ubuntu 桌面，绘制一张较小的地图可能需要几分钟。不过这时，这个软件只会偶尔运行（而且总是在后台“打盹”），所以并不是什么大问题。

一个更大的障碍（至少对于本文而言）是唯一的文档是 Jupyter Notebook 书籍 [4] 以及 prettymaps 作者和其他用户的 GitHub 页面 [5]。不要绝望！本教程解释了如何安装 prettymaps，以及即使你从未用过 Python，如何完全按照你想要的方式绘制这些任何地图。要解决这个问题，有必要从快速概述 prettymaps 的工作流和管理开始，以及一些数字制图的概念。

# OpenStreetMap

如果你在过去的 15 年里都使用过互联网，你可能知道 OpenStreetMap 是什么。但以防万一，这里有一个快速定义，专注于与本教程直接相关的方面！OpenStreetMap (OSM) 是用于创建数字地理的维基百科，一个开放的世界地图，由全球数千名志愿者构建并持续维护。很难解释 OSM 有多重要，它是数字地理数据的基石。

## 什么是数字地图？

# LINUX 教程 - PRETTYMAPS

列表 1 中的代码来自开发者提供的示例之一。我修改了初始坐标——并且删除了所有注释，因为我必须重新思考代码，偏移量，由于某种原因，你可能希望地图以任何角度旋转，或者不在图像中心。此外，还导入了“备份”选项，它允许你在下次进行美化时加载之前运行的结果。欲需更多详细信息，请查看 prettymaps 网站：

列表 1 非常冗长，但并没有你初看时那么复杂。前 20 行仅加载了 prettymaps 所需的所有库。定义要创建的第一个 Matplotlib 图形，设置其坐标轴和尺寸。

可能是脚本的核心指令，第 24 行描述了地图将代表地球的哪个区域。这是一个以 10km 为半径的案例，中心位于大致对应罗马中心的经纬度上。

在脚本的第一部分，你可以可选地设置几个选项，从图形的标题和旋转开始。

# 列表 1：罗马的圆形地图

```python
01 os from IPython import get_python

03 ipython = get_python()

04

05 if '__IPYTHON__' in globals():

06 ipython.magic('load_ext autoreload 2')

07 ipython.magic('autoreload 2')

08

09 import sys; sys.path.append('../../')

10 from prettymaps import *

11 import vsketch

12 import osmnx as ox

13 import matplotlib.pyplot as plt

14 import prettymaps.pyplot as plt

15 from descartes import Polygon

16 from shapely.geometry import *

17 from shapely.affinity import *

18 from shapely.ops import unary_union

19

20 fig, ax = plt.subplots(figsize=(12, 12), constrained_layout=True)
```

```python
23 layers = plot(

24 4.1894859685158, 12.4194859606428, radius=1000,

25 ax=ax,

26 layers =
```

```python
27 'perimeter':
28 'streets':
29 'custom_filter': {'highway':'motorway|primary|secondary|tertiary|residential|unclassified|pedestrian|footway'},
30 'width':
31 'motorway': 5,
32 'trunk': 5,
33 'primary': 4,
34 'secondary': 3,
35 'tertiary': 2,
36 'residential': 3,
37 'service': 2,
38 'unclassified': 2.
```

```python
39 'pedestrian': 2,
40 'footway': 1,
41,
42,
43 building={'tags': {'building': True, 'landuse': 'construction': 'union', 'face': 'False'}},
44 water={'tags': {'natural': 'water', 'bay': 'bay'}},
45 green={'tags': {'landuse': 'grass', 'natural': 'island', 'wood', 'leisure': 'park'}},
46 forest={'tags': ('landuse': 'forest'}},
47 parking={'tags': {'amenity': 'parking', 'highway': 'pedestrian', 'man_made': 'pier'}},
49 drawing_keys=
50 background={'#F2F2F2', 'ec': '#dadcol', 'hatch': '', 'zorder': -1},
51 perimeter={'#F2F2F8', 'ec': '#dadcol', 'label': '0': '', 'zorder': 0},
52 green={'#F7F7F7', 'ec': '#F7F7F7', 'zorder': 1, '0': 2},
53 forest={'#A6A6A6', 'ec': '#F7F7F7', 'zorder': 1, '0': 3},
55 parking={'#F7F7F7', 'ec': '#F7F7F7', 'zorder': 1, '0': 3},
56 streets={'#F7F7F7', 'ec': '#47A567', 'alpha': 1, '0': 0, 'zorder': 3},
57 building={'palette': ['#F7F7F7', '#E2E2E2', '#C8C8C8'], 'ec': '#F7F7F7', 'lw': 5, 'zorder': 4},
58,
59,
60,
61 osm_credit={'color': '#F7F7F7'}
62 )
63 plt.savefig('rome-circular.png')
64 plt.savefig('rome-circular.svg')
```

# 教程 — PRETTYMAPS LINUX VOICE

选项非常多，多到可以填满一本书。因此，我只强调了相应函数的最重要的特征和共同特性，并建议你在美化后的页面或相应的页面上查看更多细节。看到地图的位置、形状和扩展范围后，第 26 到 48 行描述了你从数据库中下载的层，以及在需要时如何选择它们的子组件。这种能力的示例是第 29 行的 `custom_filter` 以及建筑、停车位和绿地的选项。
