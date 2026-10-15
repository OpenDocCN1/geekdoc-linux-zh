
# 列表 24.8 双引号定义

```
1: static XPoint seg0_717 = {
2: {-4,-12}, {-4,-5};
3: };
4: 
5: static XPoint seg1_717 = {
6: {4,-12}, {4,-5};
7: };
8: 
9: static XPoint *char717 = {
10: seg0_717, seg1_717,
11: NULL,
12: };
13: 
14: static int char_p717 = {
15: XtNumber(seg0_717), XtNumber(seg1_717,
16: };
```

通过这些示例，字体如 `plain_simplex`（所有字符的定义）与单个字符（由 `XPoints` 组成的段定义）之间的关系应该是清晰的。此外，`plain_simplex_p` 数组的作用是提供每个段的点数。在理解字体集的基础上，请注意列表 24.9 中引入的 `create_gtext` 函数。

# 列表 24.9 create_gtext 函数

```
1: GXTextPtr create_gtext(char *text,
2:      int x, int y,
3:      GXFont fnt, GXFontP fntp)
4: {
5:     GXTextPtr text_data;
6:     int c, chr, s, num_pts, nsegs;
7:
8:     text_data = (GXText *)XtNew(GXText);
9:     text_data->x = x;
10:    text_data->y = y;
11:
12:
13:    text_data->dx = 0;
14:    text_data->dy = 0;
15:
16:    text_data->text = XtNewString( text);
17:    text_data->len = strlen( text );
18:
19:    text_data->font = fnt;
20:    text_data->fontp = fntp;
21:
22:    text_data->vpts = (XPoint **);
23:    XtMalloc(sizeof(XPoint **) * text_data->len);
24:
25:    for (c = 0; c < text_data->len; c++, text++) {
26:        chr = *text++ ' ';
27:
28:
29:        nsegs = 0;
30:        while(fntp[chr][nsegs] != NULL ) {
31:            nsegs++;
32:        }
33:
34:    text_data->vpts[c] = (XPoint *);
35:    XtMalloc(sizeof(XPoint *) * nsegs);
36:
37:    for (s = 0; s < nsegs; s++) {
38:        num_pts = fntp[chr][s];
39:
40:        text_data->vpts[c][s] = (XPoint *)
41:        XtMalloc(sizeof(XPoint *) * num_pts);
42:    }
43:
44:    reset_pts(text_data,
45:               text_data->x, text_data->y,
46:               text_data->dx, text_data->dy);
47:
48:    return text_data;
49:}
```

`create_gtext` 函数首先分配一个新的 `GXText` 结构体实例：

```
0: text_data = (void *)XtNew( GXText );
```

接着初始化 `GXText` 结构的静态字段。`x` 和 `y` 字段跟踪 Text 对象的起点，并应用于加载到 `GXText` 结构中的字体集中的所有点。这些字段的初始值将是事件点的坐标：

```
10: text_data->x = x;
11: text_data->y = y;
```

`dx` 和 `dy` 字段管理应用于此 Text 对象创建的 x轴和y轴缩放因子。它们的用处很快就会体现，但在创建时还没有请求任何缩放增量，它们的初始值为：

```
13: text_data->dx = 0;
14: text_data->dy = 0;
```

构成新对象的字符串副本被存储在 `GXText` 结构中，同时包含字符串的长度：

```
16: text_data->text = XtNewString( text );
17: text_data->len = strlen( text );
```

最后，为了支持动态指定应用于单个 Text 对象的字体集的扩展，将该对象的特定字体分配给 `GXText` 结构。同样被分配的还有控制数组，用于跟踪字体集所理解的各种字符段中的点数：

```
19: text_data->font = fnt;
20: text_data->fontp = fnt;
```

该函数随后创建空间来存储文本字符串的向量字符，并逐个字符地遍历字符串：

```
22: text_data->vpts = (XPoint ***)
23: Xtalloc(sizeof(XPoint **)) * text_data->len);
```

```
25: for( c = 0; c < text_data->len; c++, text++) {
```

由于任何字体集理解的第一个字符都是空格，因此所有字符都将减去空格的十进制值，以确保字体集的索引与当前字符正确对齐：

```
26: chr = *text - ' '
```

## 第五部分 向编辑器添加对象

使用该字符，通过一个 `while` 循环确定使用字体集定义它所需的段数：

```
nseg = 0;
while( fnt[chr][nseg] != NULL ) {
  nseg++;
}
```

知道所需的段数允许我们分配分配足够的空间来存储它们：

```
text_data->vpts[c] = (XPoint **)
XtMalloc( sizeof( XPoint *) * nsegs );
```

最后，利用标识每个段点数的控制数组，在点相对于起点进行转置后分配足够的空间：

```
for( s = 0; s < nsegs; s++ )
num_pts = fnt[chr][s];

text_data->vpts[s] = (XPoint *)
Malloc( sizeof( XPoint ) * num_pts );
```

在为定义新 `GXText` 结构的字符串预留了适当空间后，使用 `reset_pts` 函数来转置字符串中字符段的点：

```
reset_pts( text_data,
  text_data->x, text_data->y,
  text_data->dx, text_data->dy );
```

在嵌套 `reset_pts` 函数之前，已为分配到 `GXText` 结构的字符串中的每个字符执行了分配。

`GXText` 结构是一个内存密集型构造，因为它需要为各个段内转置后的点分配内存。实际的分配次数取决于段的数量，而段数受字体复杂性的影响。

因此，对该内存进行适当管理并在应用程序不再使用它时将其归堆是非常关重要的。出于此原因，定义了列表 24.10 中的 `freeGXText` 函数。

## 列表 24.10 释放由 create_gxtext 函数部分配的内存

```
static freeGXText( GXTextPtr text_data )
{
  int c, chr, nsegs;
  char *text = text_data->text;

5: for ( c = 0; c < text_data->len; c++, text++) {
6: chr = *text - ' ';
7:
8: nsegs = 0;
9: while (text_data->font[nsegs] != NULL) {
10: XtfFree((char *)text_data->vptcs[nsegs]);
11: nsegs++;
12: }
13: XtfFree((char *)text_data->vptcs[c]);
14: }
15: XtfFree((char *)text_data->vptps);
16: XtfFree((char *)text_data->text);
17: 
```

`freeGXtext` 函数有效地通过反向操作，在 `create_gxtext` 执行分配的地方进行释放。
