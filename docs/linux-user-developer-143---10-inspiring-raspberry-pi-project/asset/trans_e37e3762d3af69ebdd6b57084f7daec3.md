

...这些测量值。数学残差函数将是...

```
residuals = y + A*sin(pi*k*x + theta)
```

...而可调参数为 'A'、'k' 和 'theta'。为了使用 'leastsq' Python 函数，你需要将这个残差方程写成一个执行相关计算的 Python 函数。然后，你可以将该函数、包含参数初始猜测值的数组以及残差函数所需的任何参数传递给函数 'optimize.leastsq()'。

我们将要看的最后一个例子是求解线性方程组。这是许多领域都会做的事情，例如物理和工程。你可以使用线性代数模块（linalg）来完成此操作。使用矩阵表示法，该系统由 'Ax=b' 定义，其中 'A' 是系数矩阵，'x' 是变量向量，'b' 是包含每个方程右边值的向量。如果已经定义了 'A' 和 'b'，你只需使用以下代码即可解决此问题：

```
import scipy.linalg as sla
x = sla.solve(A, b)
```

由于它使用了 numpy 提供的新数据类型，它简化了你需要编写的代码，使你以后更容易理解自己原本想要编写的内容。

希望本文涵盖的内容足以说服你在处理可能需要解决的任何问题时尝试使用 scipy 和 numpy。有数百个函数可用于执行相当复杂的计算 - 请查看第 62 页。而且，树莓派提供的每次浮点运算的能耗表现是无法比拟的。

## 完整代码列表

```
# 所有科学代码的开头都应该
# 导入 numpy 和 scipy
import numpy as np
import scipy as sp

# 旧的方法是通过使用
# for 循环将向量乘以缩放因子
a = [1, 2, 3, 4]
scale = 2
b = []
for curr_a in a:
    b.append(curr_a * scale)

# 更简洁、优化的方法是使用
# numpy 数组数据类型
a = np.array([1, 2, 3, 4])
scale = 2
b = scale * a

# 要对 0 到 1 之间的 sin(x) 进行积分，
# 我们需要导入 integrate
# 子模块并使用 quad 函数
import scipy.integrate as spi
import math as m
# 结果将同时包含答案
# 以及答案误差的估计值
result = spi.quad(lambda x: m.sin(x), 0.0, 1.0)

# 此 leastsq 示例来自
# scipy 文档
x = np.arange(0, 6e-2, 6e-2/30)
y_meas = y_true + 2*np.random.randn(len(x))
# 为了测试，我们将为真实的
# y 值添加噪声
A = 8
k = 1/2
theta = 3e-2
y_true = A * m.sin(m.pi * k * x + theta)
def residuals(p, y, x):
    A, k, theta = p
    err = y - A*np.sin(m.pi * k * x + theta)
    return err
p0 = [8, 1/2, 3e-2, m.pi/3]
from scipy.optimize import leastsq
plsq = leastsq(residuals, p0, args=(y_meas, x))

# 为了解方程组
# 我们需要导入 linalg 子模块
import scipy.linalg as spl
# A 将是系数矩阵
A = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 10]])
# b 将是右侧值向量
b = np.array([15, 6, 11])
# 我们可以使用
# 'solve()' 找到 x 的值
x = spl.solve(A, b)
```

## 绘制数据

与 scipy 和 numpy 一起使用的模块是 matplotlib。前两个模块处理所有数值计算任务，而 matplotlib 提供了一组图形例程，用于显示所有这些数据和结果。在我们的树莓派上，你可以使用以下命令安装它：

```
sudo apt-get install python-matplotlib
```

然后你可以使用以下代码导入该模块：

```
import pylab as pl
```

绘图函数分为两大类，低级和高级。你想使用的大部分函数都是高级的。你最基本的需求是绘制一些数据。如果你有一个存储数字向量的变量 y，你可以用以下方式绘制它们：

```
pl.plot(y)
pl.show()
```

假设该向量具有一组 y 值，其中 x 值被视为元素的索引。如果你有一组 x 和 y 点，你可以用以下方式绘制它们：

```
pl.plot(x, y)
```

这些高级函数会根据坐标轴、标签、颜色等项，对你的绘图细节做出一些合理的决策。使用低级函数时，你控制这些选项并显式设置它们。如果你使用过 R 的绘图功能，它与此系统非常相似。

![](img/daaca9116bc2b1db669c224de81abc7c_73_0.png)

![](img/daaca9116bc2b1db669c224de81abc7c_73_1.png)

# 构建更好的网络

www.webdesignermag.co.uk

在各大报摊和超市均有售

## 现已发售

SEO 的科学 | 移动完美化的十条规则 | 使用 QUnit 测试你的 jQuery

- 设计灵感
- 实用技巧
- 幕后揭秘
- 分步建议
- 行业观点

## 立即购买本期杂志

印刷版可在 www.imagineshop.co.uk 购买
数字版可在 www.greatdigitalmags.com 购买

可在以下平台上获取

![](img/daaca9116bc2b1db669c224de81abc7c_73_2.png)

facebook.com/webdesignermag    twitter.com/webdesignermag

# 评测

75 组评 | 80 香蕉派 | 82 树莓派 B+

![](img/daaca9116bc2b1db669c224de81abc7c_74_0.png)

## 组评

### 网络管理器

基础实用工具和长期以来的热门工具同台竞技，我们将挑选出提供完整解决方案的网络管理器

**Ifconfig**
作为你的命令行工具集的一部分，ifconfig 可以从你的 CLI 或终端模拟器中使用，是网络管理的基石——许多其他网络管理工具将其打包作为一部分，而有些人更喜欢直接使用它。请查阅文档了解可用选项的说明。
文档：bit.ly/1pol4eX

**GNOME 网络**
这是一个在许多 Ubuntu 版本中都能找到的简单应用，并且已经存在了很长时间，GNOME 网络应用是一个简化的网络连接管理器，非常符合 GNOME 设计。它也是大多数人曾经使用过的一款。
下载：bit.ly/U2P65I

**Network Tools**
同样在许多 Ubuntu 版本中预装，Network Tools 是 GNOME 网络更高级的对应物。它提供多种功能，通常是那些希望进行更复杂的网络检测任务或识别问题的人的首选。
下载：bit.ly/1uiCPyl

**Wicd**
作为一颗冉冉升起的新星，Wicd 近年来越来越多地成为 Linux 发行版的默认网络管理器。它还拥有一些有趣的功能，包括依赖项少以及为每个网络连接设置独立的配置文件。
下载：bit.ly/1rC17CI

# 评测

![](img/daaca9116bc2b1db669c224de81abc7c_75_0.png)

## Ifconfig

你的标准 Linux 网络管理命令行工具，深受许多人喜爱

![](img/daaca9116bc2b1db669c224de81abc7c_75_1.png)

- 如果你知道如何阅读 ifconfig 的输出结果，它可以帮助你识别连接问题

### 易用性
作为一个命令行工具，易用性非常主观。从头开始学习它比弄清楚图形工具中各个元素的工作原理要困难得多。话虽如此，一旦你确切知道自己在做什么，它可以快速且非常有用。

### 功能
ifconfig 中隐藏着许多针对各种连接设置的功能，例如 MTU 和隧道，以及有线或无线网络设置所需的基本功能。但是，没有可以附加到设置中的代理控制，这意味着你需要一个外部程序来实现这一点。

### 自定义
作为一个命令行工具，它具有危险的自定义能力，因为任何功能都可以按你希望的方式字面意义上完成——它只会比你在本次测试中的图形工具更容易断开连接。这也意味着你更能够将外部数据引入输入到字段中，这是其他工具所不允许的。

### 隐私
就隐私而言，IP 隧道是你唯一能做的事情，而不引入外部代理或 Tor 工具。Tor 比 ifconfig 能获得的工具强大得多，但如果该工具将来得到更新，一些额外的隐私控制形式将是一个绝佳的补充。

### 总体评价
> Ifconfig 是一个简单的命令行工具，它出色地完成了其设计任务。如果你正在运行命令行界面，它仍然是一种配置网络的极佳方式。

5

![](img/daaca9116bc2b1db669c224de81abc7c_75_2.png)

## GNOME 网络

GNOME 的网络工具相当基础，但功能依然非常强大

![](img/daaca9116bc2b1db669c224de81abc7c_75_3.png)

- 在此简洁软件中，轻松访问代理设置是一个受欢迎的景象

### 易用性
作为一个 GNOME 应用，Network 易于导航，并且在单个窗口内布局非常简洁明了。所有主要选项都可以从这里访问，通过清晰标记的按钮可以访问更高级的设置。这是经典的 GNOME 设计，但它没有移除功能，只是让一切变得稍微更容易访问。

### 功能
Network 中有相当多的可用功能，并且可以为你设置的各种网络提供高级设置。此外，还有一个类似手机的飞行模式，这是 GNOME 如今更多地从便携式计算角度思考的另一个例子。

### 自定义
有线和无线都有很棒的自定义控制，允许你完全控制 IPv4 和 v6 的地址，以及各种安全控制，甚至可以将无线通信转换为热点。它类似于你能从 ifconfig 等工具中获得的，但呈现方式要好得多。

### 隐私
除了上述的飞行模式（这对于切断所有访问非常有用）外，还有简单的代理控制，可以系统范围应用，从而让你在互联网上拥有更多安全性。它们不如 Tor 那么强大，但比你的标准连接做得多得多。

### 总体评价
> Network 是我们真正喜欢的少数 GNOME 应用之一，因为简化过程使其更容易使用，且没有使整个应用变得低端化。如果你默认使用它，你就拥有了一个很棒的应用。

8

