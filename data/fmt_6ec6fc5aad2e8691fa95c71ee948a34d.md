
## 用特辑版精进你的技能！

从我们的特辑库中了解 Shell、LibreOffice、Linux 等。

![](img/9114a5c8af7098772983e86dad17c99b_66_0.png)

**Linux Magazine** 团队创建了一系列单本书籍，让你深入研究你感兴趣的话题。提供纸质或数字版格式。

## 查看完整库！

shop.linuxnewmedia.com

![](img/9114a5c8af7098772983e86dad17c99b_66_1.png)

![](img/9114a5c8af7098772983e86dad17c99b_66_2.png)

![](img/9114a5c8af7098772983e86dad17c99b_66_3.png)

![](img/9114a5c8af7098772983e86dad17c99b_66_4.png)

![](img/9114a5c8af7098772983e86dad17c99b_66_5.png)

## MAKERSPACE SMath

## MakerSpace

适用于 Linux 的免费 MathCAD 替代方案

## 计算能力

在 SMath 中通过中间步骤、图形、图表和结果展示复杂的方程。作者：Brooke Metcalfe。

工程专业的大学学生经常有这样的作业：他们必须逐步展示他们的计算步骤。虽然 Excel 和 Python 对高级计算很有用，但它们无法正式地展示复杂方程。MathCAD [1] 是一个编写工程报告的良好软件包。该工具提供了工作簿界面，允许你以可读的格式输入复杂方程，并带有丰富的函数库、编程接口、图形和图表。遗憾的是，MathCAD 不支持 Linux，而且通常超出了学生或普通用户的预算。作为替代方案，SMath 是一个非常好的免费选择，可以在 Linux、macOS 和 Windows 上运行。

SMath 有一个包含常用函数和符号的侧边栏（图 1）。所有函数都列在插入 (`fn`) 对话框中。

图 1：常用函数面板。

68 2023年4月 第 269 期 LINUX-MAGAZINE.COM

## 创建和编辑大型表达式

```
$$\frac{5+3}{1} = \frac{8}{3} = 2.8471$$
$\ln\frac{3}{4} + \exp\frac{1}{10}$
```

在本文中我介绍了 SMath 并向你展示了我在学期中使用所有很棒的功能。我还查看了 SMath 如何解决典型的高中或大一数学问题。

## 方程、变量和单位

使用方向键移动到方程的部分，然后进行编辑。SMath 允许你通过侧边栏（图 1）和快捷键创建复杂的计算。可以使用方向键修改方程以移动光标元素（图 2）。

## 入门

SMath 表格从上到下排列，因此在使用变量之前定义它至关重要。变量用 `:` 定义，计算值的结果用 `=` 显示。

图 2：编辑和查看计算。

![](img/9114a5c8af7098772983e86dad17c99b_68_0.png)

要添加单位，请在输入单位前使用单引号 (`'`)，或从单位列表中选择（图 3）。如果一个计算具有混合单位，SMath 会自动管理转换（图 4）。

## 使用单位

```
length1 = 2 m
length2 = 10 in
```

```
sudo apt install mono-dev
```

下一步，将 SMath 安装文件复制到你的位置并运行 SMath 桌面版：

图 3：插入单位。

```
## 运行 SMath Desktop
./smathudio_desktop_mono
```

## 简单二次方程

| 动态更改变量 |
| --- |
| 显示图表 |
| 寻找 X 轴距 |
| 寻找面积截距 |

使用滑块 (`Sliders`) 检查 `a` 和 `b`

```
length1 + length2 = 2.254
```

## 默认公制单位

```
1127
568
- 2
2.54-10
```

| 符号 |
| --- |
| 单位转换 |
| 显示输入数据 |
| 分数形式 |
| 数值 |

数值

![](img/9114a5c8af7098772983e86dad17c99b_68_1.png)

## 定义方程常数和变量

```
f(x) = a*x^2 + b + c
```

```
length3 = 88, 742 in
```

图 6：使用界面小部件定义。

图 4：插入单位。

| 文件 编辑 视图 插入 计算 工具 页面 帮助 |
| --- |
| 矩阵... |
| 操作... |
| 字段... |
| 背景、页眉和页脚 |
| 控制 |
| 图片 |
| 区域 |
| 公式 |
| 公式 |
| 分隔符 Ctrl+Return |
| 复选框 |
| 连接 |
| 数学块 |
| 文本区域 |

向工作表中添加用户界面

| Ctrl+ |
| --- |
| Ctrl+E |
| Ctrl+W |

```
length1 = 2 m
length2 = 10
```

向工作表中添加界面

| 动态更改变量 |
| --- |
| 显示图表 |
| 寻找 X 轴距 |
| 寻找面积截距 |

使用滑块检查 `a` 和 `b`

```
length1 + length2 = 2.254
```

## Summary

Spreadsheets like Excel are great tools, but they are weak at clearly presenting equations. SMath, on the other hand, presents equations in conventional forms and has worksheets with customizable layouts.

As university student, I spent lot of the past, I used static tools such as LaTeX [3] or the Microsoft Word Editor to build calculations. Now I find the dynamic presentation of calculations in SMath can be a huge time saver.
