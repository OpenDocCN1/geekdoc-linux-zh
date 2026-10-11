
`/Intro_to_UNIX/chap08$ fig2dev -eps network_present.fig`

```
```

图 8.20 将文件转换为 Postscript。

### 为 LaTeX 创建图表和图形

你可以通过多种方法为 LaTeX 文档创建图表和图形。一种方法是你可以使用 `xfig` 绘制点和线。例如，你可以使用线条模式绘制轴、绘制单个点并绘制线条。如果你想绘制曲线或插值图线，可以使用样条模式。当需要在图中区分多条线条时，可以使用不同的线条样式，如实线、虚线、点线。轴标签可以使用文本输入模式创建。

另一种创建数据图表和图形的方法涉及 `gnuplot` 工具。`gnuplot` 可以处理数据列表或文件并绘制简单到复杂的二维或三维图表和图形。此外，`gnuplot` 提供了快速创建和格式化图表或图形的机制。对于大型数据集来说，这是非常有用的。下面介绍了了一些 `gnuplot` 基础知识，演示了上述的一些功能。表 8.8 总结了常用的 `gnuplot` 命令。

#### 表 8.8 常用 gnuplot 命令

| 命令 | 目的 |
|------|
| `plot` | 绘制给定的数据文件；可以指定是否使用线条 |
| `set xrange` | 指定轴的范围或范围 |
| `set ylabel` | 设置图形的标题 |
| `set xlabel` | 设置轴的描述 |
| `show ylabel` | |
| `Set xtics` | 设置轴的描述 |
| `set xdtics` | |
| `set xmtics` | |
| `set yticks` | |
| `set ytics` | 指定替代或自定义轴 |
| `set terminal` | 指定输出格式 |
| `set output` | 指定输出文件名 |

### 文本格式–创建和查看排版文档 269

| 命令 | 用途 |
|---|---|
| `replot` | 将图表重绘到屏幕或输出文件 |
| `save` | 保存为 gnuplot 格式的文件 |
| `load` | 加载 gnuplot 格式的文件 |
| `help` | 获取 gnuplot 命令帮助或文档 |

在本节讨论中，我们将使用 `gnuplot` 直接从文件中读取数据值。如果数据是由另一个程序生成并保存到文件中，那么这种方法将特别有用。数据文件的格式可能各不相同，但为了简单起见，你通常希望每行包含一个数据点的值。在这个示例中，你的数据文件将由一系列单独坐标组成，每行一个，代表每分钟获取的往返时间。你将使用 `gnuplot` 将这些数字作为沿递增 x 轴的 y 坐标进行绘图。或者，数据文件的每行也可能包含多个值，表示二维或三维坐标，指定数据点的所有坐标。通过额外的规格，`gnuplot` 可以解释来自其他数据文件内容的数据值，这在数据值嵌入在其他符号、单词或数字中是非常有用的。

要使用 `gnuplot` 创建网络数据的图表，你将通过输入不带参数的命令启动 `gnuplot`，如图 8.21 所示。

```
/Intro_to_UNIX/chap08$ gnuplot []
```

图 8.21 启动 `gnuplot`。

你将看到一些版权和版本信息，随后是一个提示符，如图 8.22 所示。通过这个提示符，你将输入命令来根据需求生成并格式化图表。

```
gnuplot> []
```

图 8.22 `gnuplot` 提示符。

你将输入的第一个命令（见图 8.23）是用于生成数据文件图表的 `plot` 命令。该命令由动作 `plot` 组成，后面跟着双引号中的数据文件名。该命令中包含 `with lines` 短语，用于指定你希望以连接的方式绘制数据点。如果缺少 `with lines` 短语，则指示 `gnuplot` 单独绘制点。图 8.23 所示的 `plot` 命令将产生一个新窗口，其中包含图 8.24 所示的图表。

### UNIX/Linux 简介

```
gnuplot> plot 'internal_rtt.dat' with lines
```

**图 8.23** 指定数据文件的绘图。

![](img/e3ac56d195b48617d5ae42cd57458af3_281_0.png)

**图 8.24** 格式化之前的初始图表。

`gnuplot` 将自动确定 x 轴和 y 轴的值范围。x 值的范围取决于数据文件中值的数量，因为示例数据文件每行只包含一个数据点。由于示例数据文件每个有 1080 个数据值，因此 x 轴上会有 1080 个值。y 值的范围取决于数据值本身。由于数据文件 `internal-rtt.dat` 中的数据值范围在 0 到 100 之间，因此 `gplot` 为 y 轴选择了该范围。

如果你想格式化图表以具有与自动选择不同的 x 轴范围，可以通过 `gnuplot` 的 `set xrange` 命令来实现。例如，图 8.24 中的图表的 x 轴范围为 0 到 1200（1200 是为了匹配实际数值的估计大范围）。要将 x 轴范围设置为 0 到 1079 以表示这 1080 个值，可以使用图 8.25 所示的 `gnuplot set xrange` 命令。通过 `set xrange`，你指定 x 轴的新下限和上限，所有内容包含在 `[]` 括号内，中间用冒号分隔。你同样可以可以使用 `gnuplot set xrange` 命令格式化 y 轴的下限和上限。随后使用 `replot` 命令用新更改重绘图表。

### 文本格式–创建和查看排版文档 271

```
gnuplot> set xrange[0:1080]

gnuplot> replot[]
```

图 8.25 格式化 x 轴范围。

你可以使用 `gnuplot` 命令 `set title` 指定出现在绘图图表上的标题或描述。该命令接受一个参数，即双引号内的标题文本。图 8.26 展示了如何指定图表标题为 Internal Roundtrip Time（内部往返时间）。同样，随后使用 `replot` 命令用新更改重绘图表。

```
gnuplot> set title "Internal Roundtrip Time"

gnuplot> replot[]
```

图 8.26 指定图表标题或描述。

你还可以为图表中的轴提供描述。要为 x 轴提供描述，你可以使用 `gnuplot` 命令 `set xlabel`，后跟一对双引号内的文本描述。图 8.27 显示了如何将 x 轴描述设置为 Time of day（一天中的时间）。图 8.27 还演示了使用 `show xlabel`，让你看到 x 轴的当前描述。你同样可以使用 `gnuplot` 命令 `set ylabel` 和 `show ylabel` 分别指定 y 轴的文本描述。

```
gnuplot> set xlabel "Time of day"

gnuplot> show xlabel

gnuplot> replot
```

图 8.27 为 x 轴指定描述。

在某些情况下，特别是涉及时间时，轴与默认设置并不匹配。为了更清晰地格式化轴，你可以使用 `xtics` 命令。例如，你可以指定刻度位置为：6am 处 0，9am 处 180，12pm 处 360，3pm 处 540，6pm 处 720，9pm 处 900，以及 12am 处 1080。

```
gnuplot> set xlabel "Time of day"

gnuplot> set xtics("6am" 0, "9am" 180, "12pm" 360, "3pm" 540, "6pm" 720, "9pm" 900, "12am" 1080)

gnuplot> replot[]
```

图 8.28 自定义 x 轴。

### UNIX/Linux 简介

要重新定义 y 轴的刻度，`gnuplot` 有相应的 `ytics` 和 `yticks` 命令。

### gnuplot 中保存和打开

在任何点，你都可以将当前图表及其设置（标签、刻度等）保存为 `gnuplot` 格式，以便在 `gnuplot` 中打开。注意 `gnuplot` 格式不是 Postscript。以 Postscript 格式保存图表用于 LaTeX 是另一种方式实现的，稍后描述。

在 `gnuplot` 中保存和打开图表涉及 `save` 和 `load` 命令，每个命令都接受一对单引号内的文件名作为单个参数。图 8.29 显示了你如何将当前图表及其设置保存到文件名 `internal-rtt.gnu`，其中 `.gnu` 扩展名代表 `gnuplot` 文件格式。

```
gnuplot> save 'internal_rtt.gnu' []
```

图 8.29 在 `gnuplot` 中保存图表。

### 文本格式——创建和查看排版文档 273

图 8.30 显示了如何打开之前保存的 `gnuplot` 文件。

```
gnuplot> load 'internal_rtt.gnu' []
```
