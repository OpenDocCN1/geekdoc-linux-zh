
27: `gx_add_obj`( `obj` );

列表 24.18 显示了 `create_text` 函数使用的 `copy_gxtext` 函数的内容。

# 列表 24.18 copy_gxtext 函数

```
static GXTextPtr copy_gxtext(GXTextPtr text, int off_x, int off_y)
{
GXTextPtr text_data;
int i, c, chr_pts, nsegs;
char *txt;

text_data = 
create_gxtext(text->text, text->x + off_x, text->y + off_y,
text->font, text->font);

text_data->dx = text->dx;
text_data->dy = text->dy;

txt = text_data->text;
for( c = 0; c < text_data->len; c++, txt++) {
chr = *txt - ' ';

nsegs = 0;
while( text_data->chr[nsegs] != NULL )
```

```
num_pts = text_data->fontp[chr][nsegs];

for (i = 0; i < num_pts; i++) {

text_data->vpts[c][nsegs][i].x =
text->vpts[c][nsegs][i].x + off_x;
text_data->vpts[c][nsegs][i].y =
text->vpts[c][nsegs][i].y + off_y;
}
nsegs++;
 }
}

return text_data;
)
```

`copy_gxtext` 函数首先创建一个新的 `GXText` 结构，其原点在 `Text` 结构基础上增加了 x 和 y 分量的偏移量：

```
text_data =
create_gxtext(text->text, text->x + off_x, text->y + off_y,
text->font, text->fontp);
```

该函数遍历了 `vpts` 数组中的所有点，并相应地增加了它们的值：

```
text_data->vpts[c][nsegs][i].x =
text->vpts[c][nsegs][i].x + off_x;
text_data->vpts[c][nsegs][i].y =
text->vpts[c][nsegs][i].y + off_y;
```

最后返回带有偏移值的 `GXText` 结构拷贝：

```
return text_data;
```

`create_text` 函数为所创建拷贝的偏移值指定为 0：

```
obj->data = copy_gxtext(text, 0, 0);
```

然而，此函数将用于 `text_copy` 方法的定义。

被创建的对象不再通过 GC 的交互式橡皮带绘制，而是通过调用对象的 `draw` 方法。

本节介绍了从绘图区域绘制和擦除 `Text` 对象的方法。

# 绘制和擦除文本对象

在图形编辑器中绘制或擦除对象的区别在于对为请求创建的瓦片（tile）字段 `GC` 处理。

# 第五部分 向编辑器中添加对象

注意列表 24.19 中的第 17 行和 25 行，`draw` 和 `erase` 方法的区别在于传递给 `draw_erase` 函数作为第二个参数的 `tile` 标志位的值。（同样请注意，`erase` 方法负责移除屏幕上可能存在的对象句柄）。

# 列表 24.19 绘制和擦除文本对象

```
static void draw_erase( GXObjPtr text, Boolean tile )
{
GC gc;

gc = gx_allocate_gc( text, tile );
GXDrawText((GXTextPtr)text->data, gc );

XtReleaseGC( GXArea, gc );
}

/*
* text_draw
*/
static void text_draw( GXObjPtr obj )
{
draw_erase(obj, False );
}

/*
* text_erase
*/
static void text_erase( GXObjPtr obj )
{
draw_erase(obj, True );
}
```

`draw_erase` 函数首先创建一个用于 `GXDrawText` 函数的图形上下文：

```
gc = gx_allocate_gc( text, tile );
```

创建图形上下文的关键在于为第 17 章“创建图形上下文”部分第 347 页中介绍的 `gx_allocate_gc` 函数指定 `tile` 标志。

如果你还记得，此标志指示了 `GXArea` 的位图是否被分配给 `GC` 的 `tile` 字段。分配给图形上下文的值会导致擦除动作。

## 24.22 为文本对象创建句柄
