
| `kana14` | misc-fixed-medium-r-normal--14-****jixj028.1983 |
| --- | --- |
| `kanj16` | jis-fixed-medium-r-normal--16-****jixj028.1983 |
| `nil2` | misc-normal-cursor--120-75-p-16 |
| `olcursor` | sun-open-glyph--14-120-75-p-16 |
| `olglyph-14` | sun-open-glyph--14-140-75-p-16 |
| `r14` | misc-fixed-medium-r-normal--14-****jixj028.1983 |
| `r16` | sony-fixed-medium-r-normal--16-****jixj028.1983 |
| `r24` | sony-fixed-medium-r-normal--24-****jixj028.1983 |
| `rk14` | misc-fixed-medium-r-normal--14-****jixj028.1983 |
| `r16` | sony-fixed-medium-r-normal--16-****jixj028.1983 |
| `variable` | *-helvetica-bold-r-normal-****iso8859-1 |

若要在命令行中使用带有`6x10`字体的别名字体，请将其别名添加到命令行。例如，启动`xterm`时使用此命令：

```
xterm -font 6x10
```

若要为特定字体添加粗体属性，在字体别名后输入`bold`。例如，要获取粗体的`7x14`字体，使用以下命令：

```
xterm -font 7x14bold
```

由于不同的 UNIX 系统在不同的文件中存储别名，最好的办法是找到字体目录，例如：

```
cd /
find . -name fonts
```

# 第 13 章 > 运行 X 和应用程序

准备好实验。大多数 X 发版支持数百种字体。这些字体也可以非常专业。例如，Linux 支持用于科学和数学排版、占星和天文符号、汉字和俄语字符（如果你访问中国、俄罗斯或东欧网站，这些字符非常有用）。

## 关于 X 中的颜色

除了基础颜色（白、黑、红、蓝、绿），X 还支持以下颜色：

| AntiqueWhite | LightGoldenrod | RoyalBlue | cornsilk | pink |
| :--- | :--- | :--- | :--- | :--- |
| CadetBlue | LightPink | SeaGreen | cyan | plum |
| DarkGoldenrod | LightSalmon | SkyBlue | firebrick | purple |
| DarkOliveGreen | LightSkyBlue | SlateBlue | gold | red |
| DarkOrange | LightSteelBlue | SlateGray | goldenrod | salmon |
| DarkOrchid | LightYellow | SpringGreen | gray60 | seashell |
| DarkSeaGreen | Mediumchid | SteelBlue | gray70 | sienna |
| DarkSlateGray | MediumPurple | VioletRed | gray80 | snow |
| DeepPink | MistyRose | aquamarine | gray85 | tan |
| DeepSkyBlue | NavyWhite | azure | green | thistle |
| DodgerBlue | OliveDrab | bisque | honeydew | tomato |
| HotPink | OrangeRed | blue | ivory | turquoise |
| IndianRed | PaleGreen | brown | khaki | wheat |
| LavenderBlush | PaleTurquoise | burlywood | magenta | yellow |
| LemonChiffon | PaleVioletRed | chartreuse | maroon |
| LightBlue | PeachPuff | chocolate | orange |
| LightCyan | RosyBrown | coral | orchid |

每种颜色都有不同的深度。通常有四个深度级别，你通过名称进行分配。例如，DarkSlateGray 实际上只是比普通灰色深。另一方面，DarkSlateGray3 具有几乎像烟雾般的紫色调，并且非常深。

这些颜色在屏幕上的显示方式在很大程度上取决于你的颜色分辨率和深度。如果你使用的是等同于标准 VGA（8位）的显示器，可能会遇到不理想的结果。但一般来说，越基础的颜色（或与基础颜色相关的颜色）在几乎任何色彩显示器上都显示得非常漂亮。

# 第 3 部分 > 在 UNIX GUI 中工作

这些颜色可以用于绘制任何 Xterm 及其任何组件（包括其边框、标题栏、文本、背景、前景、粗体字体等）。

![](img/b0bfb2d724c393178bf462832858a65d_197_0.png)

## 关于灰度显示

自然地，在灰度显示器上，X 无法显示颜色。因此，“颜色”会以不同深浅的灰色出现。根据一般原则，在灰度显示器上设置颜色时，你应该坚持使用及其派生色。如果不这样做，可能会可能会怪异的结果，或者 X 可能会完全拒绝加载。

## 在 Xterm 窗口内运行应用程序

要在 Xterm 窗口内运行应用程序，请打开 Xterm 并从提示符运行该程序。UNIX 会在 Xterm 内部运行指定的程序。例如，要在 Xterm 中运行`pico`，请执行以下命令：

```
pico
```

`pico`将出现在 Xterm 窗口内（见下图）。

![](img/b0bfb2d724c393178bf462832858a65d_197_1.png)

这里有一个重要点需要注意：虽然 Xterm 窗口具有特殊能力（特别是剪切和粘贴），但在 Xterms 内部运行的应用程序的功能并不比它们从命令行运行时更多。换句话说，Xterms 并没有赋予普通命令行程序特殊能力。例如，你不能在 Xterm 窗口中打开`pico`并在`pico`的任何地方放置光标开始打字。你仍然被迫遵循`pico`主要基于键盘的界面。（在第 13 章 ➤ 运行 X 和 X 应用程序：另一方面，这并没有阻止你从`pico`窗口中提取文本并将其粘贴到 X 的其他地方。）

## 关于颜色、按键和其他事物

应用程序在 Xterm 中的行为与从命令行执行时相同吗？可能吧。这取决于开发者的细致程度。通常，在命令行中具有丰富颜色方案的应用程序，在通过 Xterm 运行时看起来可能非常简陋。

此外，命令行应用程序具有奇特的按键绑定（即控制功能键作用的规则）。这些按键绑定在通过 Xterm 传输时可能无法工作。这有几个原因：最常见的原因是应用程序的键绑定与基础 X 绑定冲突。在这种情况下，X 绑定将自然获得优先级。如果键绑定对程序的运行至关重要（且 X 不支持它们），最好从 shell 运行应用程序，而不是在 X 中。

## 从 Xterm 启动应用程序

在 X 中运行应用程序的另一种方法是从 Xterm 启动它们。这很简单。打开 Xterm 并执行应用程序。例如，从 Xterm 启动`ftptool`，打开 Xterm 并在 Xterm shell 提示符处执行`ftptool`命令，如下：

```
ftptool
```

作为响应，X 将启动`ftptool`。（见下图。）

![](img/b0bfb2d724c393178bf462832858a65d_198_0.png)

大多数 X 应用程序都支持自己的命令行选项。这些选项帮助你控制它们的行为。然而，除了这些命令行选项外，还有几个适用于几乎所有 X 应用程序的选项。让我们现在简单查看这些。

## 通用 X 选项

如前所述，大多数 X 应用程序的行为方式相似。与此一致，大多数 X 应用程序也接受基本的命令行选项。这些选项允许你调整应用程序的外观和感觉。这些选项在表 13.3 中简要总结。

## 表 13.3. 通用 X 选项

| 选项 | 用途 |
| :--- | :--- |
| `-bg color` | 使用`-bg`选项设置指定应用程序的背景颜色。例如，使用灰色启动`tetris`，执行命令 `tetris -bg gray`。谨慎使用此选项。例如，在设置背景颜色之前，先对应用程序进行测试运行。确保不要将背景颜色设置为与前景相同的颜色。否则，你将完全看不到前景。（例如，Xterms 的文本通常具有黑色前景。如果你将背景颜色设置为黑色，你将无法看到文本。） |
