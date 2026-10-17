
```
7:   text_data =
8:   create_gxtext(text->text, text->x + off_x, text->y + off_y,
9:   text->font, text->fontp);
```

该函数遍历了 `vpts` 数组中的所有点，并相应地增加了它们的值：

```
25:   text_data->vpts[c][nsegs][i].x =
26:   text->vpts[c][nsegs][i].x + off_x;
27:   text_data->vpts[c][nsegs][i].y =
28:   text->vpts[c][nsegs][i].y + off_y;
```

最后返回带有偏移值的 GXText 结构拷贝：

```
34:   return text_data;
```

`create_text` 函数为所创建拷贝的偏移值指定为 0：

```
12:   obj->data = copy_gxtext(text, 0, 0);
```

然而，此函数将用于 `text_copy` 方法的定义。

被创建的对象不再通过 GC 的交互式橡皮带绘制，而是通过调用对象的 `draw` 方法。

本节介绍了从绘图区域绘制和擦除 Text 对象的方法。

# 绘制和擦除文本对象

在图形编辑器中绘制或擦除对象的区别在于对为请求创建的瓦片 `tile` 字段 GC 处理。

# 第五部分 向编辑器中添加对象

注意列表 24.19 中的第 17 行和 25 行，`draw` 和 `erase` 方法的区别仅在于传递给 `draw_erase` 函数第二个参数的 `tile` 标志位的值。同样请注意，`erase` 方法负责移除屏幕上可能存在的对象句柄。

# 列表 24.19 绘制和擦除文本对象

```
1: static void draw_erase( GXObjPtr text, Boolean tile )
2: {
3: GC gc;
4:
5: gc = gx_allocate_gc( text, tile );
6: GXDrawText((GXTextPtr)text->data, gc );
7: 
8: XtReleaseGC( GXArea, gc );
9: }
10:
12: /*
13: * text_draw
14: */
15: static void text_draw( GXObjPtr obj )
16: {
17: draw_erase(obj, False );
18: }
19:
20: /*
21: * text_erase
22: */
23: static void text_erase( GXObjPtr obj )
24: {
25: draw_erase(obj, True );
26: }
```

`draw_erase` 函数首先创建一个用于 `GXDrawText` 函数的图形上下文 `Graphics Context`：

```
5: gc = gx_allocate_gc( text, tile );
```

创建图形上下文的关键在于为在第 17 章“创建图形上下文”部分第 347 页中介绍的 `gx_allocate_gc` 函数指定 `tile` 标志。

如果你还记得，此标志指示了 `GXArea` 的位图是否被分配给 GC 的 `tile` 字段。分配给图形上下文的值会导致擦除动作。

由于 `GXDrawText` 函数需要图形上下文，因此在 `create_text` 函数中为所创建拷贝的偏移值指定为 0：

```
12:   obj->data = copy_gxtext(text, 0, 0);
```

然而，此函数将用于 `text_copy` 方法的定义。

被创建的对象不再通过 GC 的交互式橡皮带绘制，而是通过调用对象的 `draw` 方法。

本节介绍了从绘图区域绘制和擦除 Text 对象的方法。

## 460 第五部分 向编辑器中添加对象

此内容在第 17 章“常用对象创建”第 343 页中介绍：

```
9: obj = gx_create_obj();
```

创建例程拷贝了定义对象的 GXText 结构

```
12: obj->data = copy_gxtext( text, 0, 0 );
```

随后，分配了第 14-25 行中用于控制对象特定数据结构的对象方法和操作函数：

```
14: obj->draw = text_draw;
15: obj->erase = text_erase;
16: obj->find = text_find;
17: obj->move = text_move;
18: obj->scale = text_scale;
19:
21: obj->copy = text_copy;
22: obj->select = text_select;
23: obj->deselelect = text_deselelect;
24:
25: obj->save = text_save;
```

之后，该对象被添加到由编辑器应用程序管理的对象列表中：
