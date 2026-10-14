

## Linux 菜谱：日常使用技巧与诀窍

```
$ factor 2000 RET
2000: 2 2 2 2 5 5 5
$
```

> 注意：如果未给出数字，factor 会从标准输入读取数字；数字应以空格、制表符或换行符分隔。

## 29.5 数字转换

以下方法介绍如何进行各种数字转换。

- 29.5.1 在度量单位之间转换数值
- 29.5.2 将阿拉伯数字转换为英文

转换度量单位。

将阿拉伯数字转换为文本。

### 29.5.1 在度量单位之间转换数值

```
@sf(Debian): `units`
@sf(WWW): http://www.gnu.org/software/units/units.html
```

使用 units 工具在度量单位之间进行换算。给出两个带引号的参数：当前单位的数量和名称，以及目标单位的名称。它会输出两个值：换算后目标单位的数量，以及一个目标单位相当于多少你指定的当前单位数量。

- 要输出 50 克等于多少盎司，请输入：

```
$ units '50 grams' 'ounces' RET
* 1.7636981
/ 0.56699046
$
```

在此示例中，输出表明 50 克约等于 1.7636981 盎司；反过来，1 盎司约等于 50 克的 0.56699046 倍。

units 工具支持许多不同类型的单位——从摄氏度、华氏度到磅、公顷、光速，乃至“面包师的一打”（baker's dozen，即 13 个）。所有支持的单位都保存在一个文本文件数据库中；使用 `-V` 选项可以输出该数据库在系统上的位置，随后你可以翻阅或搜索该文件，查看你的版本支持哪些单位。

- 要确定 units 数据库的位置，请输入：

```
$ units -V RET
units version 1.55 with readline, units database in
/usr/share/misc/units.dat
$
```

在此示例中，units 数据库位于文件 `/usr/share/misc/units.dat` 中，这是一个可以翻阅以列出所有单位数据的文件。

### 29.5.2 将阿拉伯数字转换为英文

@sf{Debian}: 'bsdgames'

使用 number 命令将阿拉伯数字转换为英文文本。将一个数字作为参数传入；如果不带参数，number 会从标准输入读取数字。

- 要输出 100,000 对应的英文文本，请输入：

```
$ number 100000 RET
```

## 29.6 其他数学工具

下表列出了 Linux 可用的其他一些数学工具。这绝不是一份完整的列表。

| 工具 | 描述 |
|------|-------------|
| calc | calc 是一款用于 Emacs 的科学计算器工具。{@sf{Debian}: 'calc'} |
| dc | 与 bc 类似，dc 是一种任意精度计算器语言，但它是一种逆波兰计算器，数字被压入堆栈。当你给出算术运算符时，dc 会从堆栈中弹出操作数，然后将计算结果压入堆栈。{@sf{Debian}}: `dc` |
| dome | Richard J. Bono 的 dome 是一个用于计算测地线穹顶对称三角形特性的测地数学工具——它可以计算各种穹顶类型的弦因子、顶点坐标和拓扑丰度，包括“巴基球”结构和椭圆测地线。{@sf{Debian}}: `dome` {@sf{WWW}}: http://www.cris.com/~rj bono/html/domes.html |
| gnucash | GnuCash 是一款直观的个人理财应用程序。用它来管理财务，包括银行账户、股票、收入和支出；它“基于专业会计原则”，以确保计算和报告的准确性。{@sf{Debian}}: `gnucash` {@sf{WWW}}: http://www.gnucash.org/ |
| gnumeric | Gnumeric 是 GNOME 电子表格应用程序。它功能强大，有些让人想起 Excel。{@sf{Debian}}: `gnumeric` {@sf{WWW}}: http://www.gnu.org/software/gnumeric/gnumeric.html |
| gnuplot | gnuplot 工具可用于数据可视化、制作二维和三维图形以及绘制函数曲线。{@sf{Debian}}: `gnuplot` {@sf{WWW}}: ftp://ftp.gnu.org/pub/gnu/gnuplot/ |
| oleo | GNU Oleo 是一款电子表格应用程序。它既可以在 X Window 环境中运行，也可以在控制台中运行，具有类似 Emacs 的键绑定，并且可以生成 PostScript 输出。{@sf{Debian}}: `oleo` {@sf{WWW}}: http://www.gnu.org/software/oleo/oleo.html |
| sc | sc 是一款在控制台中运行的小型电子表格工具；它提供公式和其他基础功能，符合对极简电子表格的预期。 |
| xcalc | xcalc 是用于 X Window System 的可视化科学计算器——它在屏幕上绘制一个计算器，你可以使用鼠标或键盘操作它。它能够模拟 TI-30 和 HP-10C 计算器。 |
| xspread | xspread 是 sc 的 X 客户端前端。{@sf{Debian}}: `xspread` |

[ < ] [ > ] [ << ] [ 向上 ] [ >> ] [ 顶部 ] [ 目录 ] [ 索引 ] [ ? ]

