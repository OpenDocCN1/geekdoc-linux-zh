
# JChemPaint：Linux 之声

| 8 | Cs | Ba | La | Ta | W | Re | Ir | Pt | Au | Hg | Tl | Pb | Bi | Po | At | Rn | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

| 9 | Fr | Ra | | | | | | | | | | | | | | | | | | | | | | |

**图 2：** 点击形似表格的按钮会显示周期表中的所有原子。

点击代表锯齿线的图标。现在按住左鼠标键并拖动线条，直到图中出现数字 16。这个数字是碳原子的数量。当你释放鼠标按钮时，你会发现自己在几次扫动中画了 16 个碳原子。

脂肪酸的其余部分包含不饱和基团 `COO-`（羧酸）。除了氧键外，它还带有负电荷。你需要移除 `JChemPaint` 自动插入的氢原子，为负电荷留出空间。

代表氧原子的 `C` 双击，然后使用左鼠标键并从该原子开始画一条线。`JChemPaint` 随后将其替换为双键和两个氢原子（图 1）。继续画，直到你画出该化学化合物的结构式。

包含原子较少的化学化合物也可以表示，但它们所需的原子并不容易找到。按下底部工具栏上的周期表图标，会显示周期表中包含的所有原子（图 2）。与之前一样，你可以单击即可将这些原子转移到绘图中。此时值得提到，`JChemPaint` 中的绘图不是黑白的。原子遵循公认的标准。例如，氧原子显示为红色，而氯原子具有绿色背景。

多链碳在有机化学中是不寻常的。例如，具有 16 个原子的脂肪酸（如棕榈酸）必须绘制棕榈酸的分子式 `CH3(CH2)14CO-`；无需费力，首先选择带有 `C` 的图标，然后……

**图 1：** 得益于自动补全功能，创建化学化合物时没有任何错误风险。

## 绘制分子

在 `JChemPaint` 中创建图形有两种方法。要表示化学化合物……

**列表 1：** 设置 `JChemPaint`

```
$ wget http://github.com/downloads/JChemPaint/jchempaint-jchempaint-<Version>.jar
$ java -jar jchempaint-<Version>.jar
```

## 选择一个元素...

### 氢 (H)

原子序数 1，第 1 族，第 1 周期

| | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | H | | | | | | | | | | | | | | | | | He |
| 2 | Li | Be | | | | | | | | | | | | | | | | Ne |
| 3 | Na | Mg | | | | | | | | | | | | | | | | Ar |
| 4 | K | Ca | Sc | Ti | V | Cr | Mn | Fe | Co | Ni | Cu | Zn | Ga | Ge | As | Se | Br | Kr |
| 5 | Rb | Sr | Y | Zr | Nb | Mo | Tc | Ru | Rh | Pd | Ag | Cd | In | Sn | Sb | Te | I | Xe |
| 6 | Cs | Ba | La | Hf | Ta | W | Re | Os | Ir | Pt | Au | Hg | Tl | Pb | Bi | Po | At | Rn |
| 7 | Fr | Ra | Ac | Rf | Db | Sg | Bh | Hs | Mt | Ds | Rg | Cn | Nh | Fl | Mc | Lv | Ts | Og |
| 8 | | | | | | | | | | | | | | | | | | | |
| 9 | | | | | | | | | | | | | | | | | | | |

**图 2：** 点击形似表格的按钮会显示周期表中的所有原子。

## 结论

`JChemPaint` 的独特之处在于，在 Linux 上或通用的免费软件中，没有更好的替代品。某些常用格式允许你检索其他在线服务的绘图信息。但此程序仍处于开发的早期阶段。在我们的实验室中，我们无法绘制带有内部圆形的环。不过，这些结构以模板的形式可用。此外，由于未处理上述 `JChemPaint` 的错误，某些操作会导致糟糕的 Java 异常。`JChemPaint` 是一个非常有用的编辑器，可以创建化学化合物的漂亮 2D 视图。

通过选择“文件 | 另存为图像”绘制 `PNG`、`BMP` 或 `SVG` 图形。或者，你也可以通过选择“工具 | 创建 SMILES”输出绘图的 `SMILES` 字符串。这意味着你可以通过一个或多个服务（如 `Molinspiration` [6]）携带用表示的化学化合物。

`JChemPaint` 可以从“文件 (SDF)” 格式导入结构 [7]，这是一种以 `.sdf` 结尾的常用文件格式，用于交换化学信息。此外，各种化合物还以 `IUPAC` 国际化学标识符（`InChI`）数字 [8] 显示，它是以字符串形式表示的分子（与 `SMILES` 不同），或者以抽象结构服务（`CAS`）编号 [9] 显示，这是由美国化学会在数据库中管理的每个分子的唯一标识符。这两种表示法都与 `SMILES` 竞争。

> **作者**
>
> Anjela Minosi 在 Fiverr 上以 `pczenminosi` 的昵称提供 IT 服务。她提供的服务包括清理、分析和数据可视化。

## 信息

- [1] `JChemPaint`: https://jchempaint.github.io
- [2] `VSEPR`: https://en.wikipedia.org/wiki/VSEPR_theory
- [3] `SMILES`: https://en.wikipedia.org/wiki/Simplified_molecular_input_line_entry_system
- [4] `CML`: https://en.wikipedia.org/wiki/Chemical_Markup_Language
- [5] `MDL MOL`: https://en.wikipedia.org/wiki/Chemical_table_file
- [6] `Molinspiration`: https://www.molinspiration.com/cgi-bin/properties
- [7] `SDF`: https://file.info/extension/sdf
- [8] `InChI`: https://iupac.org/who-we-are/divisions/division-details/inchi/
- [9] `CAS Registry Number`: https://www.cas.org/support/documentation/chemical-substances/facts

**图 7：** 在插入原子时，你可以让它们吸附到位置。这意味着它们会紧挨在一起。

---

# Figma：易于设计

**作者：GRAHAM MORRISON**

有些人聚在一起。他们想要一些简单的东西来帮助他们反复迭代用户界面。他们尝试了 `Figma`，正因为它的绘图与它的社交功能（包括备注和白板）并存。

当 `Adobe` 宣布将以 200 亿美元收购 `Figma`（设计师的首选工具）时，最初是震惊，随后是冲去寻找替代品，这并不是一项简单的任务。坦率地说，有几个替代品。最强大的是 `Penpot`，它是一个优秀的设计工具，但只能通过浏览器运行。这就是 `Akira` 派上用场的地方。`Akira` 是一个处于开发初期的开源 Linux 工具。还有许多工作需要完成，该项目明确指出不应在生产环境中使用。`Akira` 已经具备功能，并能够很好地支持可能来自新用户涌入的更多资源。界面会让 `Figma` 的用户感到熟悉。使用 `GTK` 的感觉很熟悉。

- 添加：圆形
- 填充：椭圆、矩形
- 交互：文本
- 布局：画布
- 顺序：层级
- 图层：文本
- 颜色：圆、矩形
- 文本：圆形

---

# 通过特版书籍提升你的技能！

从我们的特版书籍库中了解 `Shell`、`LibreOffice`、`Linux` 等内容。

`Linux Magazine` 团队创建了一系列单本书籍，让你深入研究你感兴趣的话题。提供纸质或数字格式供选择。

查看完整库！
shop.linuxnewmedia.com
