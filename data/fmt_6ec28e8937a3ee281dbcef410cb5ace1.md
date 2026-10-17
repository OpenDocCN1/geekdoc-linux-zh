
# [1] "ggplot"

要渲染图表，我们只需打印该对象：

```r
print(p)
```

### 8.3 几何形状 (Geometries)

在 `ggplot2` 中，我们通过添加层（layers）来创建图表。层可以定义几何形状、计算统计数据、定义刻度，甚至更改样式。添加层我们使用 `+` 符号。通常，一行代码看起来如下：

```r
DATA %>% ggplot() + LAYER 1 + LAYER 2 + ... + LAYER N
```

通常，添加的层定义几何形状。示例包括 `geom_point`、`geom_bar` 和 `geom_histogram`。

为了让 `geom_point` 正常运行，我们需要数据和映射。我们已经将对象 `p` 与 `murders` 数据连接，如果添加层，它默认使用该数据。要找出哪些映射，我们阅读帮助文件的 Aesthetics 部分：

> Aesthetics:
> x
> y
> alpha

### 8.4 审美映射 (Aesthetic mappings)

审美映射描述了属性如何连接到图表的特征，例如沿轴的距离、大小或颜色。`aes` 函数通过定义映射将数据与我们在图中看到的内容连接起来，并将是你绘图时最常用的函数之一。审美映射的结果通常作为几何函数的参数。这个示例生成了以百万为单位的谋杀总数散点图：

```r
murders <- ggplot() +
  geom_point(aes(x = population/10^6, y = total))
```

如果我们愿意，可以省略 `x` 和 `y`，因为它们是预期的前两个参数，见帮助页面。

不是从零开始，我们也可以向定义为 `p <- ggplot(data = murders)` 的对象 `p` 添加层：

```r
p + geom_point(aes(population/10^6, total))
```

![](img/276727cd0f1f6fea60002e6d839d370a_112_0.png)

添加此层时，刻度和标签默认定义的。像 `dplyr` 函数一样，`aes` 也使用对象组件中的变量名：我们可以直接使用 `population` 和 `total`，无需调用 `murders$population` 和 `murders$total`。识别数据组件变量的行为是 `aes` 特有的。

### 8.5 图层

我们想要制作的图的第二层涉及为每个点添加标签以识别状态。`geom_label` 和 `geom_text` 函数允许我们向图中添加文本，且分别不会在文本之间添加矩形。

由于每个点（在这种情况下为状态）都有标签，因此我们需要一个美学映射（aesthetic mapping）来建立点和标签之间的联系。通过阅读帮助文件，我们获知通过 `aes` 参数提供点与标签之间的映射。因此，代码如下：

```
p + geom_point(aes(population/10^6, total)) +
geom_text(aes(population/10^6, total, label = abb))
```

![](img/276727cd0f1f6fea60002e6d839d370a_113_0.png)

我们成功地为图表添加了第二层。

作为上述 `aes` 独特行为的示例，请注意以下调用：

```
p_test <- p + geom_text(aes(population/10^6, total, label = abb))
```

是没问题的，而此代码：

```
p_test <- p + geom_text(aes(population/10^6, total), label = abb)
```

将会导致错误 `aes abb is not found`，因为它位于 `aes` 函数之外。图层 `geom_text` 不知道去哪里寻找 `abb`，因为它是一个列名而不是全局变量。

#### 8.5.1 调整参数

每个几何对象都有许多 `aes` 和 `data` 之外的参数。这些参数通常特定于该函数。在我们想要制作的图中，点比帮助文件中看到的默认尺寸大，我们看到 `size` 是一个美学属性，我们可以这样更改它：

```
p + geom_point(aes(population/10^6, total), size = 3) +
geom_text(aes(population/10^6, total, label = abb))
```

![](img/276727cd0f1f6fea60002e6d839d370a_114_0.png)

`size` 不是 映射：映射使用来自特定观测的数据并需要包含在 `aes()` 中，而我们想要相同地影响所有点的操作不需要包含在 `aes` 内部。

现在因为点变大了，标签很难看清。如果我们阅读 `geom_text` 的帮助文件，我们会看到 `nudge` 参数，它可以将文本稍微向右或向左移动：

```
p + geom_point(aes(population/10^6, total), size = 3) +
geom_text(aes(population/10^6, total, label = abb), nudge_x = 1)
```

![](img/276727cd0f1f6fea60002e6d839d370a_114_1.png)

这种方法更好，因为它更容易阅读文本。在第 `8.11` 节中，我们将学习一种更好的方法来确保我们能看到点和标签。

### 8.6 全局与局部美学映射

在上一行代码中，我们两次定义了映射 `aes(population/10^6, total)`，分别定义在每个几何对象中。我们可以通过使用*全局*美学映射来避免这种情况。我们可以在定义空白画布 `ggplot` 对象时这样做。记住，`ggplot` 函数包含一个允许我们定义美学映射的参数：

```
args(ggplot)
#> function(data = NULL, mapping = aes(), ..., environment = parent.frame())
# NULL
```

如果在 `ggplot` 中定义了映射，所有作为图层添加的几何对象将默认使用该映射。
我们定义 `p`：

```
p <- murders %>% ggplot(aes(population/10^6, total, label = abb))
```

然后我们可以简单地写这段代码：

```
p + geom_point(size = 3) +
geom_text(nudge_x = 1.5)
```

![](img/276727cd0f1f6fea60002e6d839d370a_115_0.png)

我们分别在 `geom_point` 和 `geom_text` 中保留了 `size` 和 `nudge_x` 参数，因为我们只想增加点的大小并只移动标签。如果我们将这些参数放在 `aes` 中，它们将应用于两个图。此外注意，`geom_point` 函数不需要 `label` 参数，因此忽略了美学属性。

如有必要，我们可以通过在每个图层中定义新映射来覆盖全局映射。这些局部定义会覆盖全局定义。这里有一个示例：

```
p + geom_point(size = 3) +
geom_text(aes(x = 10, y = 800, label = "Hello there!"))
```

![](img/276727cd0f1f6fea60002e6d839d370a_116_0.png)

显然，第二次调用 `geom_text` 没有使用 `population` 和 `total`。

### 8.7 刻度

首先，我们需要的刻度是对数刻度。这不是默认值，此更改需要通过刻度层（scales layer）添加。快速查看速表发现 `scale_x_continuous` 函数允许我们控制刻度的行为。我们这样使用 `geom`：

```
p + geom_point(size = 3) +
geom_text(nudge_x = 0.05) +
scale_x_continuous(trans = "log10") +
scale_y_continuous(trans = "log10")
```

![](img/276727cd0f1f6fea60002e6d839161.png)

由于我们处于对数刻度下，`nudge` 必须更小。这种特定的转换非常常见，`ggplot2` 提供了专门的函数 `scale_x_log10` 和 `scale_y_log10`，可以使用它们来还原代码：

```
p + geom_point(size = 3) +
geom_text(nudge_x = 0.05) +
scale_x_log10() +
scale_y_log10()
```

### 8.8 标签与标题

同样，速表显示更改标签和添加标题使用以下函数：

```
p + geom_point(size = 3) +
  geom_text(nudge_x = 0.05) +
  scale_x_log10() +
  scale_y_log10() +
  xlab("Population in millions (log scale)") +
  ylab("Total number of murders (log scale)") +
  ggtitle("US Murders in 2010")
```

![](img/276727cd0f1f6fea60002e6d839d370a_117_0.png)

我们快完成了！只需添加颜色、图例和可选的样式。

### 8.9 类别作为颜色

我们可以使用 `geom_point` 函数中的 `col` 参数来更改点的颜色。为了演示新功能，我们将重新定义 `p` 为点图层：

```
p <- murders %>% ggplot(aes(population/10^6, total, label = abb)) +
  geom_text(nudge_x = 0.05) +
  scale_x_log10() +
  scale_y_log10() +
  xlab("Population in millions (log scale)") +
  ylab("Total number of murders (log scale)") +
  ggtitle("US Murders in 2010")
```

并通过给 `geom_point` 添加不同颜色来测试。我们可以通过添加 `color` 参数将所有点变为蓝色：

```
p <- geom_point(size = 3, color = "blue")
```

### 8.10 注释、形状与调整

## 2010年美国杀人案

![](img/276727cd0f1f6fea60002e6d839d370a_118_0.png)

当然，这不是我们想要的。我们想根据区域分配颜色。`ggplot2` 一个很好的默认行为是如果我们把分类变量赋予颜色，它会自动为每个类别分配不同的颜色并添加图例。

由于颜色的选择是由每个观测特征决定的，这是一种映射。要将每个点映射到颜色，我们需要使用 `aes`。我们使用以下代码：

```
p + geom_point(aes(col=region), size = 3)
```

## 2010年美国杀人案

![](img/276727cd0f1f6fea60002e6d839d370a_118_1.png)

- 东北
- 南部
- 中北部
- 西部

`x` 和 `y` 的映射继承自 `p` 中已定义，因此我们不需要重新定义它们。我们在函数调用中预期映射的第一个参数也使用了 `aes`。

在这里我们看到了另一个有用的默认行为：`ggplot2`会自动添加将颜色映射到区域的图例。为了避免添加此图例，我们使用 `geom_point` 参数 `legend = FALSE`。

我们想不对直接来自 `aes` 映射的图形添加形状或注释；示例包括标签、框、阴影区域和线。我们想添加一条代表整个国家平均杀人率的线。一旦每百万人的率为 `r`，这条线由公式定义：$y = rx$，其中 `y` 和 `x` 分别是我们的轴：总杀人人数和百万人口。在对数刻度下，这条线变为：$log(y) = log(r) + log(x)$。因此在我们的图中，它是一条斜率为 1 截距为 $log(r)$ 的线。为了计算这一点，我们使用 `dplyr` 技能：

```
summarize(rate = sum(total) / sum(population) * 10^6) %>%
pull(rate)
```

使用 `geom_abline` 函数添加线，`ggplot2` 使用名称中的 `ab` 来表示我们提供的截距 (`a`) 和斜率 (`b`)。默认线的斜率为 1 截距为 0，所以我们只需要定义截距：

```
p + geom_point(aes(col=region), size = 3) +
geom_abline(intercept = log10(r))
```

![](img/276727cd0f1f6fea60002e6d839d370a_119_0.png)

`geom_abline` 不使用来自数据对象的任何信息。我们可以使用参数更改线的类型和颜色。此外，我们先在点上方绘制它。

```
p <- geom_abline(intercept = log10(r), lty = 2, color = "darkgrey") +
geom_point(aes(col=region), size = 3)
```

`ggplot2` 创建的默认图已经非常好用了。然而，我们经常需要对默认行为进行微调。虽然从速表看起来并不如何进行这些操作，但 `ggplot2` 非常灵活。例如，我们可以使用 `scale_color_discrete` 函数更改图例。在我们的图中，`region` 一词的首字母是大写的，我们可以这样更改它：

```
p <- scale_color_discrete(name = "Region")
```

### 8.11 扩展包

扩展包的存在增强了 `ggplot` 的功能。完成图表最后所需的剩余更改需要 `ggthemes` 和 `ggrepel` 包。

## 8.12. 整合在一起

`ggplot2` 图图的样式可以使用主题函数（theme functions）进行更改。`ggplot2` 包中包含了几个主题。对于书中的大多数图表，我们使用了 `dslabs` 包中的一个函数来自动设置默认主题：
`s_theme_set()`

`ggthemes` 包还添加了许多其他主题。其中就包括我们使用的 `theme_economist` 主题。在安装该包后，你可以通过添加如下图层来更改样式：
```r
library(ggthemes)
p + theme_economist()
```

你只需更改函数，就可以查看其他一些主题的外观。例如，你可能会发现 `theme_fiveirtyeight()` 主题。

最后的区别在于标签的位置。在我们的图表中，某些标签重叠在了一起。扩展包 `ggrepel` 包含一种几何对象（geometry），它可以在添加标签的同时确保它们不会相互重叠。我们只需将 `geom_text` 替换为 `geom_text_repaint` 即可。

### 8.12 整合在一起

既然我们正在进行测试，我们可以编写一段代码，从零开始生成我们所需的图表。
```r
library(ggthemes)
library(ggrepel)
```

```r
r <- murders %>%
  summarize(rate = sum(total) / sum(population) * 10^6) %>%
  pull(rate)
murders %>% ggplot(aes(population/10^6, total, label = abb)) + 
  geom_line(intercept = log10(r), lty = 2, color = "darkgrey") + 
  geom_point(aes(col=region), size = 3) + 
  geom_text_repaint() + 
  scale_x_log10() + 
  scale_y_log10() + 
  xlab("Populations in millions (log scale)") + 
  ylab("Total number of murders (log scale)") + 
  ggtitle("2010年美国枪击杀案") + 
  scale_color_discrete(name = "Region") + 
  theme_economist()
```

## 2010年美国枪击杀案

![](img/276727cd0f1f6fea60002e6d839d370a_121_0.png)

## 8.13 使用 qplot 快速绘图

我们已经学习了使用 `ggplot` 生成可视化内容的强大方法。然而，在某些情况下，我们只是想快速绘制一个图，例如，向量中值的直方图、两个向量中值的散点图，或者按分类和数值向量绘制箱线图。我们已经演示了如何使用 `hist`、`plot` 和 `boxplot` 来生成这些图表。但是，如果我们想保持与 `ggplot` 风格一致，可以使用 `qplot` 函数。

如果我们有两个向量中的值，例如：

```r
data(murders)
x <- log10(murders$population)
y <- murders$total
```

并且我们想用 `ggplot` 绘制一个散点图，我们必须输入类似代码：

```r
data.frame(x = x, y = y) %>%
ggplot(aes(x, y)) +
  geom_point()
```

对于这样一个简单的图表来说，这似乎代码太多了。`qplot` 函数牺牲了 `ggplot` 方法提供的灵活性，但允许我们快速生成图表。

```r
qplot(x, y)
```
