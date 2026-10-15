
# 310 第四部分 部分布局

列表 15.3 中的字母 A 的字符定义由三个线段组成。图 15.3 阐了组成每个线段的向量的方向。

## 图 15.3

定义简单矢量字体中 A 的线段表示。

![](img/786ba9bd5cd671beb490264fd2e6aae1_332_0.png)

如图 15.3 所示，此矢量字体集中定义字符的图形原点位于单元格中心。由于此原点与 X 图形原理使用的原点不同，文本对象数据结构的定义必须通过跟踪字符字符串的位置来正确放置文本。

回顾你现在对矢量字体的了解是非常重要的。

单个字符由由多个点组成的多个线段组成。换句话说，点数组形成一个线段，而线段数组（点数组数组）定义一个字符。

将这些结合起来，我们可以说点数组的数组数组形成了一个字符。因此，整个字体集（即所有字符定义）是字符的数组，它是点数组的数组的数组。整个字体集表示为

```
XPoint **plain_simple[] = {
char32, char33, char34, char35, char36, char37,
char38, char39, char40, char41, char42, char43,
char44, char45, char46, char47, char48, char49,
char50, char51, char52, char53, char54, char55,
char56, char57, char58, char59, char60, char61,
char62, char63, char64, char65, char66, char67,
char68, char69, char70, char71, char72, char73,
char74, char75, char76, char77, char78, char79,
char80, char81, char82, char83, char84, char85,
char86, char87, char88, char89, char90, char91,
char92, char93, char94, char95, char96, char97,
```

# 通用对象定义 第15章 311

```
char98, char99, char100, char102, char103
char104, char105, char106, char107, char108, char109
char110, char111, char112, char113, char114, char115
char115, char116, char117, char118, char119, char120
char121, char122, char123, char124, char125, char126;
;
```

`plain_simple` 集的元素是字符定义。定义每个字符的线段数组将在第 24 章“矢量文本对象”中给出。对我们目前的讨论重要的是，字体集由一个数组组成，其中每个元素都是一个数组，而这些数组进一步包含点数组。

`GXFont` 类型已经在 Graphics Editor 项目中定义，用于表示字体集。

```
typedef XPoint ***GXFont;
```

`GXFont` 中每个数组的长度都很重要。为了跟踪这个长度，定义了第二个数组：

```
typedef int **GXFontArray;
```

`GXFontArray` `int` 元素，每个元素对应 `GXFont` 类型中的一个长度值。这两个数组的使用紧密相关，并遵循以下片段：

```
static void GXDrawText(GXTextPtr text, GC gc) {
  char *txt = text;
  int c, nsegs, num_pts;
  for(c = 0; c < text->len; c++) {
    char chr = *txt - ' ';
    nsegs = 0;
    while (text->chr[nsegs] != NULL ) {
      num_pts = text->font[chr][nsegs];
      if(num_pts > 0) {
        XtDrawLines(GxDrawArea), XtWindow(GxDrawArea), gc, text->vpts[c][nsegs], num_pts,
      }
      nsegs++;
    }
  }
}
```
![](img/786ba9bd5cd671beb490264fd2e6aae1_333_0.png) 此片段是用于绘制 `GXText` 中包含的字符串的实际代码。它在第 24 章引入，但在这里是为了是为了如何使用矢量字体。首先从 `GXText` 结构中提取文本字符串：

```
char *txt = text->txt;
```

然后文本字符串中的每个字符通过减去要绘制的字体中的空格十进制值来计算索引：

```
for (int c = 0; c < text->len; c++)
chr = *txt - ' ';
```

这是因为字体集中的字符顺序与图 15.4 所示的 ASCII 表相同。

## 图 15.4

ASCII 表

| Dec | Char | Dec | Char | Dec | Char |
|---|---|---|---|---|---|

| 32 | sp | 64 | @ | 96 | a |
| 33 | | 65 | A | 97 | b |
| 34 | | 66 | B | 98 | c |
| 35 | # | 67 | C | 99 | d |
| 36 | $ | 68 | D | 100 | e |
| 37 | % | 69 | E | 101 | f |
| 38 | & | 70 | F | 102 | g |
| 39 | | 71 | G | 103 | h |
| 40 | | 72 | H | 104 | i |
| 41 | | 73 | I | 105 | j |
| 42 | | 74 | J | 106 | k |
| 43 | | 75 | K | 107 | l |
| 44 | | 76 | L | 108 | m |
| 45 | | 77 | M | 109 | n |
| 46 | | 78 | N | 110 | o |
| 47 | | 79 | O | 111 | p |
| 48 | | 80 | P | 112 | q |
| 49 | | 81 | Q | 113 | r |
| 50 | | 82 | R | 114 | s |
| 51 | | 83 | S | 115 | t |
| 52 | | 84 | T | 116 | u |
| 53 | | 85 | U | 117 | v |
| 54 | | 86 | V | 118 | w |
| 55 | | 87 | W | 119 | x |
| 56 | | 88 | X | 120 | y |
| 57 | | 89 | Y | 121 | z |
| 58 | | 90 | Z | 122 | { |
| 59 | | 91 | [ | 123 | | |
| 60 | | 92 | ] | 124 | | |
| 61 | | 93 | ^ | 125 | } |
| 62 | | 94 | | 126 | | |
| 63 | | 95 | | | |

# 通用对象定义 第15章 313

注意在图 15.4，空格的十进制值为 32。由于字体集中定义的第一个字符是空格 (`char32`)，如果由 `GXDrawText` 渲染空格，它会从空格中减去空格 (32)，导致 `chr` 的值为 0。索引 零对应于数组的第一个元素，这实际上是空格字符的定义。

![](img/786ba9bd5cd671beb490264fd2e6aae1_335_0.png)

虽然不能绘制空格，但它在字体集的定义对于在文本字符串中使用时以适当距离分隔单词是非常重要的。

将此方法应用于字母 A (`char65`)，使得 'A' – ' ' 或 65 – 32 等于 33，对应数组的第 34 个元素，该元素是 `char65` 的字符定义。这结束了矢量字体和简单字符定义的介绍。第 25 章，“PostScript 简介”将完成该主题并提供此字体的剩余字符定义。

下一节将继续对文本对象数据结构的讨论。

## GXxText 数据结构

仔细观察图形编辑器应用程序支持的文本对象的要求，可以发现列表 15.2 中 `GXxText` 数据结构中的 `GXxText` 字段：

6: `GXxFont` `vpts`;

是用于在画布上绘制该对象的实际点。`vpts` 的值是通过将文本字符串中每个字符的字体集字符定义转置到由 `GXxText` 结构中 `x` 和 `y` 字段所引的位置而得到的。

理解 `GXxText` 数据结构和复杂的 `GXxFont` 数据类型需要一些时间。将在第 24 章对这些定义进行更详细的审查和解释。

`GXxText` 数据结构的复杂性与下一节介绍的 `GXxArc` 数据成反比关系。

## 弧对象数据结构

弧形对象是图形编辑器支持的图形对象中最简单的数据结构。图 15.5 展示了图形对象的示例。

图 15.5:

图形 Arc 对象的示例。

![](img/786ba9bd5cd677beb490264fd2e6aae1_336_0.png)

用于管理图 15.5 所示图形弧对象的结构类型可以在列表 15.4 中。

### 列表 15.4 GXArc 数据类型定义

```
1:  typedef XArc GXArc;
2:  typedef XArc *GXArcPtr;
```

幸运的是，X Window 系统提供了一个表示 Arc 对象的结构，该结构足够供图形编辑器中使用。

有了前面几节中定义和解释的各种图形对象的特定数据需求，我们准备好介绍通用对象数据结构，并演示它与特定图形对象之间的关系。

## 通用对象数据结构

图形编辑器应用程序支持的所有图形对象都需要许多信息。

这些数据字段并没有每个对象类型重复，而是包含在一个通用数据结构中，各个对象由此派生。

列表 15.5 引入了图形编辑器中所有图形对象使用的通用对象定义。

### 列表 15.5 通用对象数据结构

```
1:  typedef struct _gx_obj {
2:  /*
3:    * attributes
4:  */
5:    Pixel fg; /* foreground */
6:    Pixel bg; /* background */
7:
8:    Pixmap fs; /* fill style */
9:    int is; /* line style */
10:   int lw; /* line width */
11:
12:   Boolean selected;
13:
14:   XRectangle *handles;
15:   int num_handles;
16:
17:   void *data;
18:
19:   void (*draw) (struct _gx_obj *);
20:   void (*erase) (struct _gx_obj *);
21:
22:   XRectangle (*bounds) (struct _gx_obj *);
23:   Boolean (*find) (struct _gx_obj *, XEvent *);
24:
```

### 列表 15.5 续

```
25:   void (*select)   (struct _gx_obj *);
26:   void (*deselect) (struct _gx_obj *);
27:   void (*copy)     (struct _gx_obj *);
28:
29:   void (*move)     (struct _gx_obj *, XEvent *);
30:   void (*scale)    (struct _gx_obj *, XEvent *);
31:
32:   void (*action)   (struct _gx_obj *, XEvent *);
33:
34:   /*
35:     * link to other objects
36:   */
37:   struct _gx_obj *next;
38:
39: } GXObj, *GXObjPtr;
```
前几个字段维护分配给单个对象的属性：

```
5:   Pixel fg; /* foreground */
6:   Pixel bg; /* background */
7:
8:   Pixmap fs; /* fill style */
9:   int is; /* line style */
10:  int lw; /* line width */
```
这些字段将用于创建绘图上下文 (`GC`)。后续是管理对象是否选中的字段：

```
12:  Boolean selected;
```

以及反映活动状态的句柄：

```
14:  XRectangle *handles;
15:  int num_handles;
```

当对象被选中时，`selected` 字段设置为 `True`，否则设置为 `False`。

当对象被选中（或活动）时，会绘制句柄以反映这种状态，并指示用于更改尺寸的方向。当对象处于活动状态时，它可以被缩放、移动、复制或从屏幕删除。通用对象数据结构中的 `next` 字段用于存储编辑器理解的各种图形对象类型的特定数据结构：

```
17:  void *data;
```
`data` 字段可以指向早期引入的表示编辑器特定要求的任何结构。将 `data` 字段分配有效的 `GXLinePtr`、`GXTextPtr` 或 `GXArcPtr` 数据结构可以唯一标识该对象。以下方法通过其名称解释：

19: `void (*draw) (struct _gx_obj *);`

20: `void (*erase) (struct _gx_obj *);`

21:

22: `XRectangle (*bounds) (struct _gx_obj *);`

23: `Boolean (*find) (struct _gx_obj *, XEvent *);`

24:

25: `void (*select) (struct _gx_obj *);`

26: `void (*deselect) (struct _gx_obj *);`

27: `void (*copy) (struct _gx_obj *);`

28:

29: `void (*move) (struct _gx_obj *, XEvent *);`

30: `void (*scale) (struct _gx_obj *, XEvent *);`

31:

32: `void (*action) (struct _gx_obj *, XEvent *);`

用于管理图 15.5 所示图形弧对象的结构类型可以在列表 15.4 中。幸运的是，X Window 系统提供了一个表示 Arc 对象的结构，该结构足够供图形编辑器中使用。有了前面几节中定义和解释的各种图形对象的特定数据需求，我们准备好介绍通用对象数据结构，并演示它与特定图形对象之间的关系。通用对象数据结构提供的链表用于维护在编辑器中创建的对象。图形编辑器创建的所有对象将附加到上一个对象的 `next` 字段上，由第一个对象定义列表头。当对象被选中时，`selected` 字段设置为 `True`，否则设置为 `False`。当对象被选中（或活动）时，会绘制句柄以反映这种状态，并指示用于更改尺寸的方向。当对象处于活动状态时，它可以被缩放、移动、复制或从屏幕删除。通用对象数据结构中的 `next` 字段用于存储编辑器理解的各种图形对象类型的特定数据结构：`data` 字段可以指向早期引入的表示编辑器对象特定要求的结构。将 `data` 字段分配有效的 `GXLinePtr`、`GXTextPtr` 或 `GXArcPtr` 数据结构可以唯一标识该对象。用于管理图 15.5 所示图形弧对象的结构类型可以在列表 15.4 中。（等等，查看文本流……）以下方法通过其名称解释：

19: `void (*draw) (struct _gx_obj *);`

20: `void (*erase) (struct _gx_obj *);`

21:

22: `XRectangle (*bounds) (struct _gx_obj *);`

23: `Boolean (*find) (struct _gx_obj *, XEvent *);`

24:

25: `void (*select) (struct _gx_obj *);`

26: `void (*deselect) (struct _gx_obj *);`

27: `void (*copy) (struct _gx_obj *);`

28:

29: `void (*move) (struct _gx_obj *, XEvent *);`

30: `void (*scale) (struct _gx_obj *, XEvent *);`

31:

32: `void (*action) (struct _gx_obj *, XEvent *);`

通用对象数据结构的最后一个字段

```
37: struct _gx_obj *next; /* entire list of all objects */
```

用于创建链表。

## 递归

### 什么是链表？

链表是一种编程结构，允许通过 `next` 节点将节点（数据结构）连接在一起：

```
node (head) -> node -> node -> node -> NULL
```

链表的用在于它可以包含未知数量的节点。这与在定义或分配数组时确定有限数量元素的数组形成对比。

在使用链表结构时，细致地维护头（或列表开头）是非常重要的。如果丢失对列表开头的任何引用，整个列表也将丢失。如此之前的链表所示，`NULL` 指针标记了列表中的节点。
