
- ggplot2`ggplot2.org`
- 文档`docs.ggplot2.org/current`
- RSQLite`bit.ly/1Acvkio`

R 是一个 **基于 S 的 GNU 项目，S 是著名的 AT&T 贝尔实验室开发的一种统计专用语言和开发环境**。你可以将 R 视为 S 的免费版本。尽管名字简单，但 R 是一款功能强大的统计计算软件，具备多种能力，且是一种解释型编程语言。

R 包可以极大地扩展其功能。`Ggplot2` 是一个由 Hadley Wickham 编写的 R 包，用于生成统计和数据图形，支持通过图层处理图表。尽管这是一个功能强大的包，但它学习起来相当容易，并且能生成出版质量的复杂、美观的图表。它与其他大多数图形包的主要区别在于其深层的原则语法。学习其语法（基于 `The Grammar Of Graphics` 一书）有助于你设计更好的图表，但阅读本文并非必须。换句话说，语法表明图表是从数据到几何对象美学属性的映射。

本文充满了实用示例，演示了 `ggplot2` 用于绘制多种不同种类图表的使用，甚至包括 Chrome 历史记录文件的图表！

熟悉数学和统计学会有帮助，但对于理解本文并非至关重要。

![](img/30dc0459712b32ede1a3814d456b41b6_64_0.png)

### “实验你的数据和 R 与 ggplot 能生成的各种类型的图表”

#### 01 安装 ggplot2

首先运行 R。`ggplot2` R 包默认未安装，因此请通过运行以下命令检查你是否已安装：

```r
> require(ggplot2)
```

加载必需的包：`ggplot2`

如果未安装，请下载并选择：

```r
> install.packages("ggplot2")
```

如果你不带参数执行 `library()` 函数，将获得已安装包的列表。若要获取详细输出，请不带参数运行 `installed.packages()` 命令。

#### 02 关于 R 和数据可视化

R 是一个命令行应用程序，这适合纯文本输出，但不适合图形输出。RStudio 是 R 更优选的图形外壳。在可视化数据时，请记住并非每种图表都适合每个数据集。这种知识来自经验，而经验来自实验，所以不要忘记实验你的数据以及 R 和 `ggplot2` 能生成的各种类型的图表。

#### 03 使用 quickplot()

`ggplot2` 包提供两个主要函数：`quickplot()` 和 `ggplot()`。`quickplot()` 函数（即 `qplot()`）类似于 R 的 `plot()` 函数，适用于简单图表。

`quickplot()` 函数隐藏了内部发生的过程，而 `ggplot()` 较难使用但更灵活。以下命令使用数据变量中的 `V2` 和 `V3` 列绘制图表：

```r
> str(data)
'data.frame':  16180 obs. of  3 variables:
$ V1: num  0 0 0 0 0 0 9.8 1 1.86 1 ...
$ V2: num  0.01 0.01 0.01 0.01 0.03 0.01 0.58 0.85 1.01 1.01 ...
$ V3: num  0.05 0.05 0.05 0.05 0.05 0.05 0.27 0.48 0.55 0.75 ...
```

```r
> quickplot(data$V2, data$V3)
```

以下版本为输出添加了颜色：

```r
> quickplot(data$V2, data$V3, color=data$V1)
```

#### 04 使用 ggpairs()

`ggpairs()` 命令查找变量之间的关系，然后计算相关系数值。相关系数与统计相关性相关联，这是一种展示两个变量是否相关的技术。随着相关系数趋近于零，相关性减弱（无相关性），而相关系数越接近 -1 或 +1，相关性（正或负）越强。正相关表示如果一个变量变大，另一个变量也随之变大。相反，负相关表示如果一个变量变大，另一个变量则变小。

![](img/30dc0459712b32ede1a3814d456b41b6_64_1.png)

上面展示的图表是使用以下命令生成的：

```r
> data <- read.table("uptime.data",
+ header=TRUE)
> require(ggplot2)
> require(GGally)
> require(CCA)
> ggpairs(data)
```

#### 05 生成条形图

现在使用一个示例数据集进行绘图。LUD 数据集可从 FileSilo 获取，存储在一个名为 `LUD.data` 的纯文本文件中。列标题的命名与其值相对应。你可以使用以下命令将数据集加载到 R 中：

```r
> LUD <- read.table("lud.data",
+ header=TRUE)
```

条形图非常简单。以下命令生成它：

```r
> ggplot(LUD, aes(x=RAM, y=SSD)) + geom_bar(stat="identity")
```

如果你输入 `ggplot(LUD, aes(x=RAM, y=SSD))` 而不指定绘图层，命令将显示 'Error: No layers in plot' 消息。若要更改条形的颜色，请尝试以下变体：

```r
> ggplot(LUD, aes(x=RAM, y=SSD,
+ fill=Uptime)) + geom_bar(stat="identity")
```

![](img/30dc0459712b32ede1a3814d456b41b6_65_0.png)

![](img/30dc0459712b32ede1a3814d456b41b6_65_1.png)

#### 06 添加标题和标签

迟早，你可能会想给输出结果添加标题和标签。

添加主标题很简单 – 你只需要使用 `labs()` 函数即可。因此，之前绘制的条形图可以在末尾包含以下命令进行修改：

```r
ggplot(LUD, aes(x=RAM, y=SSD, fill=Uptime)) + geom_bar(stat="identity") + labs(title="This is a Title")
```

可以通过输入以下内容来添加 X 和 Y 轴标签：

```r
ggplot(LUD, aes(x=RAM, y=SSD, fill=Uptime)) + geom_bar(stat="identity") +
    labs(title="This is a Title") + xlab("X Label") + ylab("Y Label")
```

#### 07 更多关于标题和标签的内容

你可以添加或更改所有标题和标签的外观、颜色、字体和大小。

以下命令使用 `theme()` 函数将标题设置为蓝色并增大其大小：

```r
ggplot(LUD, aes(x=RAM, y=SSD, fill=Uptime)) + geom_bar(stat="identity") +
    labs(title="This is a Title") + xlab("X Label") + ylab("Y Label") + 
    theme(plot.title = element_text(size = rel(2), colour = "blue"))
```

要更改 X 轴和 Y 轴的属性，请使用 `axis.line` 函数：

```r
ggplot(LUD, aes(x=RAM, y=SSD, fill=Uptime)) + geom_bar(stat="identity") +
    labs(title="This is a Title") + xlab("X Label") + ylab("Y Label") + 
    theme(plot.title = element_text(size = rel(2), colour = "blue"), 
          axis.line = element_line(size = 3, colour = "red", linetype = "dotted"))
```

#### 08 创建直方图

使用 `geom_histogram()` 函数生成直方图，类似于 `geom_bar()` 函数，并使用 `binwidth` 参数更改条形图的数量。使用以下命令绘制一个简单的直方图：

```r
ggplot(LUD, aes(Year5)) + geom_histogram(binwidth=1, color="gray")
```

使用 `geom_density()` 函数进行密度图绘制：

```r
ggplot(LUD, aes(Year5)) + geom_density()
```

以下命令在同一个图中绘制直方图和密度图：
